# Stock Analysis (SA) App – Master Plan

## 1. Core Goal & Philosophy

Build a swing-trading stock analysis app that:

- **Scores stocks 0–100** on "Quality/Holdability" (3–12 month horizon).
- **Uses Financial Modeling Prep (FMP)** for:
  - Fundamentals (statements, TTM ratios, key metrics).
  - Market data (historical prices, indexes like QQQ, VIX).
- **Supports:**
  - Daily screening & scoring.
  - History runs (per-day scores over years).
  - Backtesting (forward 1‑month returns & alpha vs QQQ).
  - Iteration by editing config JSON, not code.
- **Style:**
  - Quality & financial health first, valuation second, technicals light.
  - Size floor: allow ≥ 300M market cap; small caps must "earn" their place with strong fundamentals.
  - Avoid "chart rockets with garbage fundamentals".

---

## 2. Data Layers & Architecture

### 2.1 Fundamentals Layer (Already Built)

**Data model:** `FinancialReportV1` (versioned).

- **Metadata:** symbol, currency, period (start, end, type).
- **Income statement:** revenue, operatingIncome, netIncome, etc.
- **Balance sheet:** totalAssets, totalLiabilities, totalEquity, current/non‑current splits.
- **Cash flow:** operatingCashFlow, endingCashBalance, etc.
- **Basic metrics:** gross/operating/net margins, ROA, ROE.
- **extensions:** free-form namespace for future add‑ons.

**Storage:**

- Table: `financial_reports_v1` with JSONB payload.
- Unique: `(symbol, period_start_date, period_type, version)`.

**FMP Integration:**

- Edge function `financial-reports-fetch`:
  - Calls FMP income/balance/cash flow endpoints in bulk per symbol.
  - Uses `fmpMapper.ts` to build `FinancialReportV1`.
  - Upserts into `financial_reports_v1`.
- `financial-reports-query` reads stored reports.

### 2.2 Metrics Layer – TTM Ratios & Key Metrics

**Goal:** Centralize all derived metrics needed for scoring & filters.

**Data model:** `MetricsSnapshotV1` (conceptually):

- `symbol`, `asOfDate`.
- **metrics:**
  - **Profitability:**
    - FCF margin (TTM)
    - Operating margin (TTM)
    - Net margin (TTM)
    - ROE, ROIC (TTM)
  - **Growth:**
    - Revenue growth (TTM vs prior)
    - EPS growth (TTM vs prior)
    - Growth consistency flags (e.g., last 3 years)
  - **Balance sheet:**
    - Debt-to-equity
    - Interest coverage
    - Current ratio
    - Net debt / equity
    - Change in leverage & liquidity vs prior year
  - **Valuation:**
    - PE (TTM)
    - Price-to-sales (TTM)
    - EV/EBITDA (TTM)
    - FCF yield (TTM)
    - Sector-relative valuations (optional)
  - **Size & liquidity:**
    - Market cap
    - Shares outstanding
    - Average daily dollar volume (e.g., 20D)
  - **Technical:**
    - ATR% (20D)
    - Realized volatility (20D)
    - Price vs MA50 / MA200
    - Past returns (1D, 10D, 1M, 3M)
  - **extensions** for future metrics.

**Storage:**

- Table: `metrics_snapshots_v1` with JSONB payload.
- Unique: `(symbol, as_of_date, version)`.

**FMP Endpoints:**

- Bulk TTM ratios
- Bulk TTM key metrics
- Bulk historical market data (stocks, QQQ, VIX)

**Edge function:** `metrics-snapshots-fetch`:

- Input: date + symbols.
- Calls bulk endpoints for all symbols.
- Computes ATR, realized vol, avg dollar volume from price history.
- Stores one `MetricsSnapshotV1` per symbol/date.

---

## 3. Scoring System (0–100 "Quality/Holdability")

### 3.1 Block Weights

| Block | Points |
|-------|--------|
| Profitability quality | 25 pts |
| Growth & stability | 15 pts |
| Balance sheet strength | 20 pts |
| Valuation sanity | 20 pts |
| Technical / trading profile | 5 pts |
| Bonus / penalties | ±10 pts |

**Total score:**

- Base = sum of blocks (Profitability + Growth + Balance sheet + Valuation + Technical).
- Final = base + bonus/penalty, clipped to **0–100**.

### 3.2 Size Philosophy

- **Minimum market cap:** 300M.
- **Size buckets:**
  - Small: 300M–1B
  - Mid: 1B–10B
  - Large: >10B
- **Design rules:**
  - Small caps may receive a small size penalty (e.g., −3 to −5 pts).
  - Small + bad health (high leverage, negative FCF) is heavily penalized or excluded.

---

## 4. Detailed Scoring Blocks & Questions

### 4.1 Profitability Block (25 pts)

**Metrics:** FCF margin, operating margin, net margin, ROE/ROIC, margin stability.

#### Q1 – FCF Margin (TTM) – 8 pts

**Metric:** FCF margin = FCF_TTM / revenue_TTM.

| Condition | Points |
|-----------|--------|
| ≥ 15% | +8 |
| 10–15% | +6 |
| 5–10% | +4 |
| 0–5% | +1 |
| < 0% | −5 |

#### Q2 – Operating Margin (TTM) – 6 pts

**Metric:** operating margin = operating_income_TTM / revenue_TTM.

| Condition | Points |
|-----------|--------|
| ≥ 20% | +6 |
| 10–20% | +4 |
| 5–10% | +2 |
| 0–5% | 0 |
| < 0% | −3 |

#### Q3 – Net Margin (TTM) – 4 pts

**Metric:** net margin = net_income_TTM / revenue_TTM.

| Condition | Points |
|-----------|--------|
| ≥ 15% | +4 |
| 8–15% | +3 |
| 3–8% | +2 |
| 0–3% | 0 |
| < 0% | −3 |

#### Q4 – ROE / ROIC (TTM) – 4 pts

**Metric:** ROE or ROIC (TTM).

| Condition | Points |
|-----------|--------|
| ≥ 20% | +4 |
| 10–20% | +3 |
| 5–10% | +2 |
| 0–5% | 0 |
| < 0% | −2 |

#### Q5 – Profitability Stability vs Prior Year – 3 pts

**Metric:** Change in net margin (or operating margin) vs prior year.

| Condition | Points |
|-----------|--------|
| Positive both years, drop < 5 percentage points | +3 |
| Positive both years, drop 5–10 points | +1 |
| Negative → positive | +1 |
| Positive → negative | −4 |
| Negative both years | −2 |

> **Profitability score** = sum of Q1–Q5, clipped to **0–25**.

---

### 4.2 Balance Sheet Strength Block (20 pts)

**Metrics:** debt-to-equity, interest coverage, current ratio, net debt, leverage/liquidity trend.

#### Q1 – Debt-to-Equity – 6 pts

**Metric:** total_debt / total_equity.

| Condition | Points |
|-----------|--------|
| ≤ 0.3 | +6 |
| 0.3–0.6 | +4 |
| 0.6–1.0 | +2 |
| 1.0–2.0 | 0 |
| > 2.0 | −4 |

#### Q2 – Interest Coverage – 5 pts

**Metric:** EBIT_TTM / interest_expense_TTM.

| Condition | Points |
|-----------|--------|
| ≥ 8 | +5 |
| 4–8 | +3 |
| 2–4 | +1 |
| 1–2 | −2 |
| < 1 | −5 |

#### Q3 – Current Ratio – 4 pts

**Metric:** current_assets / current_liabilities.

| Condition | Points |
|-----------|--------|
| 1.5–3.0 | +4 |
| 1.2–1.5 | +3 |
| 1.0–1.2 | +1 |
| 0.8–1.0 | −2 |
| < 0.8 | −4 |

#### Q4 – Net Debt vs Equity – 3 pts

**Metric:** net_debt = total_debt − cash; net_debt_to_equity = net_debt / equity.

| Condition | Points |
|-----------|--------|
| net debt < 0 (net cash) | +3 |
| 0–25% | +2 |
| 25–50% | 0 |
| 50–100% | −2 |
| > 100% | −4 |

#### Q5 – Leverage & Liquidity Trend – 2 pts

**Metrics:** delta_debt_to_equity, delta_current_ratio vs prior year.

| Condition | Points |
|-----------|--------|
| Leverage stable or down AND liquidity not worse | +2 |
| Leverage up moderately, liquidity stable or better | 0 |
| Leverage up significantly AND liquidity down | −3 |
| High leverage both years and rising | −4 |

> **Balance sheet score** = sum of Q1–Q5, clipped to **0–20**.

---

### 4.3 Growth & Stability Block (15 pts)

**Metrics:** revenue growth, EPS growth, growth consistency.

#### Q1 – Revenue Growth – 6 pts

**Metric:** (revenue_TTM − revenue_prev_TTM) / revenue_prev_TTM.

| Condition | Points |
|-----------|--------|
| ≥ 20% | +6 |
| 10–20% | +4 |
| 5–10% | +2 |
| 0–5% | 0 |
| < 0% | −3 |

#### Q2 – EPS Growth – 5 pts

**Metric:** (EPS_TTM − EPS_prev_TTM) / EPS_prev_TTM.

| Condition | Points |
|-----------|--------|
| ≥ 20% | +5 |
| 10–20% | +3 |
| 5–10% | +1 |
| 0–5% | 0 |
| < 0% | −3 |

#### Q3 – Growth Consistency – 2 pts

**Metric:** Count of positive revenue growth years in last 3.

| Condition | Points |
|-----------|--------|
| 3/3 positive | +2 |
| 2/3 positive | +1 |
| 1 or 0 | 0 |
| ≥ 2 negative years | −2 |

#### Q4 – Growth + Profitability Combo – 2 pts

**Metrics:** revenue_growth_TTM, operating_margin_TTM.

| Condition | Points |
|-----------|--------|
| growth ≥ 10% AND operating margin ≥ 10% | +2 |
| either growth ≥ 10% OR operating margin ≥ 10% | +1 |
| neither | 0 |

> **Growth score** = sum of Q1–Q4, clipped to **0–15**.

---

### 4.4 Valuation Block (20 pts)

**Metrics:** PE, PS, EV/EBITDA, FCF yield, sector-relative valuations.

#### Q1 – PE (TTM) – 5 pts

**Metric:** price / EPS_TTM.

| Condition | Points |
|-----------|--------|
| 5–15 | +5 |
| 15–25 | +3 |
| 25–40 | +1 |
| < 5 | 0 |
| > 40 | −3 |

#### Q2 – Price-to-Sales (TTM) – 4 pts

**Metric:** price / (revenue_TTM per share).

| Condition | Points |
|-----------|--------|
| < 2 | +4 |
| 2–4 | +2 |
| 4–8 | 0 |
| > 8 | −3 |

#### Q3 – EV/EBITDA (TTM) – 4 pts

**Metric:** EV / EBITDA_TTM.

| Condition | Points |
|-----------|--------|
| 5–10 | +4 |
| 10–15 | +2 |
| 15–25 | 0 |
| < 5 | 0 |
| > 25 | −3 |

#### Q4 – FCF Yield (TTM) – 5 pts

**Metric:** FCF_TTM / market_cap.

| Condition | Points |
|-----------|--------|
| ≥ 8% | +5 |
| 5–8% | +3 |
| 2–5% | +1 |
| 0–2% | 0 |
| < 0% | −4 |

#### Q5 – Relative Valuation vs Sector – 2 pts

**Metric:** stock PE vs sector median PE (ratio).

| Condition | Points |
|-----------|--------|
| ≤ 0.8 (≥ 20% cheaper) | +2 |
| 0.8–1.2 | 0 |
| > 1.2 | −2 |

> **Valuation score** = sum of Q1–Q5, clipped to **0–20**.

---

### 4.5 Technical / Trading Profile Block (5 pts)

**Metrics:** price vs MAs, ATR%.

#### Q1 – Trend vs MA50 / MA200 – 3 pts

| Condition | Points |
|-----------|--------|
| Price > MA50 AND price > MA200 | +3 |
| Price > MA200 but ≤ MA50 | +1 |
| Price ≤ MA200 | 0 |

#### Q2 – Volatility Band (ATR%) – 2 pts

**Metric:** ATR_20D / price.

| Condition | Points |
|-----------|--------|
| ATR% between 2% and 6% | +2 |
| ATR% < 2% | 0 |
| ATR% > 6% | 0 (or treat as alert/penalty later) |

> **Technical score** = Q1 + Q2, clipped to **0–5**.

---

### 4.6 Bonus / Penalty Block (±10 pts)

Pattern-based adjustments applied after base score.

#### Penalty – Small, Leveraged, Negative FCF

- **Conditions:**
  - 300M ≤ market cap ≤ 500M
  - debt-to-equity > 1.5
  - FCF margin < 0
- **Penalty:** −5 to −7

#### Penalty – Profitability Crash

- net margin > 10% prior year and < 0% current → **−3/−4**

#### Penalty – Repeated Negative FCF & High Leverage

- FCF margin < 0 two years in a row AND debt-to-equity > 1 → **−5**

#### Bonus – All-Round Excellence

- **Conditions:**
  - Profitability ≥ 80% of max (≥ 20/25)
  - Balance sheet ≥ 80% of max (≥ 16/20)
  - Valuation ≥ 60% of max (≥ 12/20)
- **Bonus:** +3 to +5

#### Bonus – Net Cash & Strong FCF

- net debt < 0 AND FCF margin ≥ 10% → **+2/+3**

> Sum all applicable adjustments and clip between **−10 and +10**.
>
> **Final total score** = base score + bonus/penalty, clipped to **0–100**.

---

## 5. Filters Page (Dynamic Universe Builder)

### 5.1 Purpose

Interactive Filters page that:

- Lets the user set filter criteria via forms + presets.
- Uses FMP Stock Screener API for broad filters.
- Uses bulk TTM ratios/metrics and market data for detailed filters.
- Shows a result table.
- Allows saving results as a watchlist or sending them to the Score page.

### 5.2 Filter Groups & Options

Each numeric field has:
- A preset dropdown (named presets).
- An "Other" option with custom min/max inputs.

**Groups:**

#### Universe & Listing

- **Exchange(s):** presets (US majors, US+Canada, All), or manual.
- **Sectors/industries:** presets + multi-select.
- **Countries:** presets + list.
- **Checkbox:** "Only actively trading stocks."

#### Size & Liquidity

- **Market cap:**
  - Presets: "Small+ (≥300M)", "Mid+ (≥1B)", "Large (≥10B)", "All (≥100M)", Other.
- **Price:**
  - Presets: "≥3", "≥5", "≥10", Other.
- **Avg daily dollar volume (20D):**
  - Presets: "≥1M", "≥5M", "≥10M", Other.

#### Profitability

- **FCF margin (TTM):** presets "≥0%", "≥5%", "≥10%", Other.
- **Operating margin:** presets "≥5%", "≥10%", "≥15%", Other.
- **Net margin:** presets "≥0%", "≥5%", "≥10%", Other.
- **ROE/ROIC:** presets "≥5%", "≥10%", "≥15%", Other.

#### Balance Sheet / Risk

- **Debt-to-equity:** presets "≤1.5", "≤1.0", "≤0.6", Other.
- **Interest coverage:** presets "≥3", "≥5", "≥8", Other.
- **Current ratio:** presets "≥1.2", "≥1.5", "≥2.0", Other.
- **Optional toggle:** "Exclude net-debt-heavy stocks (e.g., net debt > 100% equity)."

#### Growth

- **Revenue growth (TTM vs prior):** presets "≥0%", "≥5%", "≥10%", Other.
- **EPS growth:** same style.
- **Optional:** "Exclude stocks with ≥2 years negative revenue growth."

#### Valuation

- **PE:** presets "5–40", "5–25", "10–60", Other (min/max).
- **Price-to-sales:** presets "<8", "<4", "<2", Other.
- **EV/EBITDA:** presets "5–25", "5–15", Other.
- **FCF yield:** presets "≥0%", "≥2%", "≥5%", Other.

#### Technical

- **Trend:**
  - Checkboxes: "Price > 200D MA", "Price > 50D MA".
- **3‑month return:**
  - Presets: "≥0%", "≥10%", "−10% to +50%", Other.
- **Volatility (ATR% or realized vol):**
  - Presets: "2–6% ATR", "Other".
- **Optional:** exclude extreme 1‑day moves (e.g., >40%).

### 5.3 Preset Profiles

At the top, provide presets that auto-fill filters:

- **"Quality Core (Conservative)"**
- **"Quality Growth (Aggressive)"**
- **"Dividend & Stability"** (future)
- **"Custom / Other"**

Each profile sets default values; user can tweak per field.

### 5.4 Result Table

**Columns:**

- Symbol, name, sector
- Market cap, price
- FCF margin, net margin, ROE
- Debt-to-equity, interest coverage
- PE, PS, FCF yield
- 3‑month return, price vs 200D MA

**Actions:**

- **Save as Watchlist** (name + description).
- **Analyze with Scoring:** sends symbol list to Score page.

---

## 6. Watchlists

**Tables:**

- `watchlists` (id, name, description, created_by, created_at).
- `watchlist_symbols` (watchlist_id, symbol).

**Features:**

- Add/edit/delete watchlists.
- Add/remove symbols.

**Integration:**

- Filters result → new watchlist.
- Score page & History runs can choose:
  - Manual symbol list.
  - Watchlist as universe.

---

## 7. Score Page (Daily Snapshot)

### 7.1 Inputs

- **asOfDate** (default today).
- **Symbols:**
  - Entered manually.
  - Or selected watchlist.
- **Scoring config version** (e.g., "v1.0" or active).

### 7.2 Behavior

- Ensure `MetricsSnapshotV1` exists for each symbol/date (fetch if needed).
- Apply scoring blocks + bonus/penalty.
- Fetch prices, returns, MAs, QQQ, VIX.

### 7.3 Table Columns

**Per symbol:**

- Symbol
- Final score (0–100)
- Block scores: Profitability, Growth, Balance sheet, Valuation, Technical
- Bonus/penalty
- Alerts
- Price
- % change: 1D, 10D, 1M, 3M, pre‑market, after‑hours (if available)
- Market cap, liquidity, volatility buckets

**Top bar:**

- QQQ price
- QQQ 1M & 3M trailing returns
- VIX level
- (In backtest view) QQQ forward 1M return and simple regime tag

---

## 8. History Runs & Backtesting

### 8.1 History Run Definition

A history run has:

- **Name**
- **Scoring config version**
- **Date range** (start, end)
- **Universe type:**
  - Manual symbols
  - Watchlist
- **Universe details**
- **Note**

### 8.2 Per-Day History Table

For each (symbol, date):

- Date (analysis date)
- Symbol
- Final score
- Block scores
- Bonus/penalty
- Price
- Backward returns (1D, 10D, 1M, 3M)
- Forward 1M return (T → T+30 days)
- Alpha vs QQQ (forward)
- Buckets (size, liquidity, volatility)
- Alerts
- Note

### 8.3 Summary Metrics Per Run

**Compute:**

- **Win rate:**
  - % of rows where forward 1M return > 0 (or > threshold).
- **Average forward 1M return.**
- **Average alpha vs QQQ.**
- **Optionally:**
  - Volatility and max drawdown for a simple "top N by score" strategy.

**UI:**

- List of runs with summary metrics.
- Click to detail view (history table + CSV download).

---

## 9. Config-Driven Scoring & Versioning

- The scoring system is encoded in a **ScoringConfig** (blocks, questions, bands, points, patterns).
- You maintain multiple versions: v1.0, v1.1, etc.
- One config is "active" for live scoring.
- History runs can specify which config version to use.

**When you want to change the model:**

1. Clone config → modify weights/bands/questions → save as new version.
2. Run new history tests and compare performance.

**Role of AI:**

- You paste the current config or describe the change.
- AI generates the new version with updated bands/points.

---

> *This markdown is your single source-of-truth blueprint for the app and the scoring system. You can now slice it into implementation prompts (for Lovable or code) block by block, without losing the big picture.*





**End of Comet SA Scoring version**





