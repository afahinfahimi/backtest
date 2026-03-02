# Module-2 - Analysis

**Lovable Trade V19 Hybrid - Updated 3/2/2026**

## Stock Analysis (SA) Score Overview

- Score each stock provided by the user (via CSV or direct entry).
- Answer each question below and find the points that apply.
- Add all points to calculate the Raw Score. **No normalization needed — Raw Score = Final Score.**
- Pull the data from connected FMP API (`/stable` endpoints).

**Missing Data Handling:** If data unavailable for any question, do not estimate, follow the rules to assign points:
- For questions with positive-only answers (e.g., 0 to 14): assign middle value (e.g., 7)
- For questions with negative-only answer range: assign 0
- For questions with both positive and negative answer range (e.g., -3 to +4): assign 0
- For penalty questions (max 0): assign 0 (no penalty)

**V19 Hybrid Changes from V17:**
- Q1 (Sales Growth): 2× weight → max 14 (was 6)
- Q3 (Cash Flow Growth): 2× weight → max 14 (was 6)
- Q31 (Trend Deterioration): penalty increased → -10 (was -3)
- All other positive-point questions: proportionally scaled to reach max 95
- All penalties (except Q31): unchanged from V17
- Normalization: removed — raw score IS the final score

---

## API Endpoint Reference

| Alias Used Below | Full Endpoint |
|-----------------|---------------|
| `financial-growth(annual)` | `/stable/financial-growth?symbol={}&period=annual` |
| `financial-growth(quarter)` | `/stable/financial-growth?symbol={}&period=quarter` |
| `ratios-ttm` | `/stable/ratios-ttm?symbol={}` |
| `key-metrics-ttm` | `/stable/key-metrics-ttm?symbol={}` |
| `stock-price-change` | `/stable/stock-price-change?symbol={}` |
| `quote` | `/stable/quote?symbol={}` |
| `profile` | `/stable/profile?symbol={}` |
| `shares-float` | `/stable/shares-float?symbol={}` |
| `grades-consensus` | `/stable/grades-consensus?symbol={}` |
| `income-statement(quarter)` | `/stable/income-statement?symbol={}&period=quarter` |
| `cash-flow-statement(quarter)` | `/stable/cash-flow-statement?symbol={}&period=quarter` |
| `historical-price-eod` | `/stable/historical-price-eod/full?symbol={}` |
| `sma(20)` | `/stable/technical-indicators/sma?symbol={}&periodLength=20&timeframe=1day` |
| `sma(50)` | `/stable/technical-indicators/sma?symbol={}&periodLength=50&timeframe=1day` |
| `standarddeviation(20)` | `/stable/technical-indicators/standarddeviation?symbol={}&periodLength=20&timeframe=1day` |
| `institutional-ownership` | `/stable/institutional-ownership/symbol-positions-summary?symbol={}` |

**Computed Fields (not native FMP):**
- `10dChangePercent` → Compute from `historical-price-eod`: `(close[today] - close[10 trading days ago]) / close[10 trading days ago] × 100`
- `5dChangePercent` → `stock-price-change.5D`
- `bollingerPercentB` → Compute: `(quote.price - lowerBand) / (upperBand - lowerBand) × 100` where `upperBand = sma(20) + 2×standarddeviation(20)`, `lowerBand = sma(20) - 2×standarddeviation(20)`
- `analystCount` → `grades-consensus.strongBuy + buy + hold + sell + strongSell`
- `institutionalOwnershipPct` → Compute from `institutional-ownership` reported shares vs `shares-float.outstandingShares`
- `shortPercentFloat` → External data source (not native FMP)
- `sectorAvg1M` → Compute from sector peers or use `/stable/historical-sector-performance`

---

## Stock Analysis Score Questions

### Growth Metrics

**Q1: Sales Growth** ★ DOUBLE WEIGHTED
- **Endpoints:** `financial-growth(annual).revenueGrowth`, `financial-growth(quarter).revenueGrowth`
- **Description:** Revenue growth %. Full SA logic uses both annual & quarterly acceleration. DOUBLE WEIGHTED — primary alpha driver.
- Max Points: 14 | Min Points: 0

| Cond | Conditions | Pts | Label |
|------|-----------|-----|-------|
| A | `financial-growth(annual).revenueGrowth` >= 0.50 AND `financial-growth(quarter).revenueGrowth` > `financial-growth(annual).revenueGrowth` | 14 | Accelerating Exceptional |
| B | `financial-growth(annual).revenueGrowth` >= 0.50 AND `financial-growth(quarter).revenueGrowth` > 0 AND `financial-growth(quarter).revenueGrowth` <= `financial-growth(annual).revenueGrowth` | 12 | Steady Exceptional |
| C | `financial-growth(annual).revenueGrowth` >= 0.20 AND `financial-growth(annual).revenueGrowth` < 0.50 AND `financial-growth(quarter).revenueGrowth` > `financial-growth(annual).revenueGrowth` | 12 | Accelerating Strong |
| D | `financial-growth(annual).revenueGrowth` >= 0.20 AND `financial-growth(annual).revenueGrowth` < 0.50 AND `financial-growth(quarter).revenueGrowth` > 0 AND `financial-growth(quarter).revenueGrowth` <= `financial-growth(annual).revenueGrowth` | 9 | Steady Strong |
| E | `financial-growth(annual).revenueGrowth` >= 0.01 AND `financial-growth(annual).revenueGrowth` < 0.20 AND `financial-growth(quarter).revenueGrowth` > 0 | 5 | Growing |
| F | `financial-growth(annual).revenueGrowth` >= 0 AND `financial-growth(quarter).revenueGrowth` <= 0 | 2 | Stalling |
| G | `financial-growth(annual).revenueGrowth` < 0 AND `financial-growth(quarter).revenueGrowth` > 0 | 2 | Recovering |
| H | else | 0 | Declining |

---

**Q2: Operating Income Growth**
- **Endpoints:** `financial-growth(annual).operatingIncomeGrowth`, `financial-growth(quarter).operatingIncomeGrowth`
- **Description:** Operating income growth %. Full SA logic uses both annual & quarterly acceleration.
- Max Points: 7 | Min Points: 0

| Cond | Conditions | Pts | Label |
|------|-----------|-----|-------|
| A | `financial-growth(annual).operatingIncomeGrowth` >= 0.50 AND `financial-growth(quarter).operatingIncomeGrowth` > `financial-growth(annual).operatingIncomeGrowth` | 7 | Accelerating Exceptional |
| B | `financial-growth(annual).operatingIncomeGrowth` >= 0.50 AND `financial-growth(quarter).operatingIncomeGrowth` > 0 AND `financial-growth(quarter).operatingIncomeGrowth` <= `financial-growth(annual).operatingIncomeGrowth` | 6 | Steady Exceptional |
| C | `financial-growth(annual).operatingIncomeGrowth` >= 0.20 AND `financial-growth(annual).operatingIncomeGrowth` < 0.50 AND `financial-growth(quarter).operatingIncomeGrowth` > `financial-growth(annual).operatingIncomeGrowth` | 6 | Accelerating Strong |
| D | `financial-growth(annual).operatingIncomeGrowth` >= 0.20 AND `financial-growth(annual).operatingIncomeGrowth` < 0.50 AND `financial-growth(quarter).operatingIncomeGrowth` > 0 AND `financial-growth(quarter).operatingIncomeGrowth` <= `financial-growth(annual).operatingIncomeGrowth` | 5 | Steady Strong |
| E | `financial-growth(annual).operatingIncomeGrowth` >= 0.01 AND `financial-growth(annual).operatingIncomeGrowth` < 0.20 AND `financial-growth(quarter).operatingIncomeGrowth` > 0 | 2 | Growing |
| F | `financial-growth(annual).operatingIncomeGrowth` >= 0 AND `financial-growth(quarter).operatingIncomeGrowth` <= 0 | 1 | Stalling |
| G | `financial-growth(annual).operatingIncomeGrowth` < 0 AND `financial-growth(quarter).operatingIncomeGrowth` > 0 | 1 | Recovering |
| H | else | 0 | Declining |

---

**Q3: Cash Flow Growth** ★ DOUBLE WEIGHTED
- **Endpoints:** `financial-growth(annual).operatingCashFlowGrowth`, `financial-growth(quarter).operatingCashFlowGrowth`
- **Description:** Operating cash flow growth %. Full SA logic uses both annual & quarterly acceleration. DOUBLE WEIGHTED — risk shield.
- Max Points: 14 | Min Points: 0

| Cond | Conditions | Pts | Label |
|------|-----------|-----|-------|
| A | `financial-growth(annual).operatingCashFlowGrowth` >= 0.50 AND `financial-growth(quarter).operatingCashFlowGrowth` > `financial-growth(annual).operatingCashFlowGrowth` | 14 | Accelerating Exceptional |
| B | `financial-growth(annual).operatingCashFlowGrowth` >= 0.50 AND `financial-growth(quarter).operatingCashFlowGrowth` > 0 AND `financial-growth(quarter).operatingCashFlowGrowth` <= `financial-growth(annual).operatingCashFlowGrowth` | 12 | Steady Exceptional |
| C | `financial-growth(annual).operatingCashFlowGrowth` >= 0.20 AND `financial-growth(annual).operatingCashFlowGrowth` < 0.50 AND `financial-growth(quarter).operatingCashFlowGrowth` > `financial-growth(annual).operatingCashFlowGrowth` | 12 | Accelerating Strong |
| D | `financial-growth(annual).operatingCashFlowGrowth` >= 0.20 AND `financial-growth(annual).operatingCashFlowGrowth` < 0.50 AND `financial-growth(quarter).operatingCashFlowGrowth` > 0 AND `financial-growth(quarter).operatingCashFlowGrowth` <= `financial-growth(annual).operatingCashFlowGrowth` | 9 | Steady Strong |
| E | `financial-growth(annual).operatingCashFlowGrowth` >= 0.01 AND `financial-growth(annual).operatingCashFlowGrowth` < 0.20 AND `financial-growth(quarter).operatingCashFlowGrowth` > 0 | 5 | Growing |
| F | `financial-growth(annual).operatingCashFlowGrowth` >= 0 AND `financial-growth(quarter).operatingCashFlowGrowth` <= 0 | 2 | Stalling |
| G | `financial-growth(annual).operatingCashFlowGrowth` < 0 AND `financial-growth(quarter).operatingCashFlowGrowth` > 0 | 2 | Recovering |
| H | else | 0 | Declining |

---

### Cyclical Sector Cap

**Applies to:** `profile.sector` in [Basic Materials, Energy] OR symbol in Mining list
**Rule:** Q1, Q2, Q3 capped at **4 points** each.
**⚠️ DECISION NEEDED:** Cap kept at 4 from V17 — now only 29% of Q1/Q3 max (14). See end of document.
**Exception:** If Q21 = "Breakout" (5 pts), cap is lifted.

---

### Profitability

**Q4: Net Profit Margin**
- **Endpoint:** `ratios-ttm.netProfitMarginTTM`
- **Description:** Net Income ÷ Revenue (TTM). FMP returns as decimal (e.g., 0.30 = 30%).
- Max Points: 6 | Min Points: 0

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `ratios-ttm.netProfitMarginTTM` >= 0.30 | 6 | Exceptional |
| B | `ratios-ttm.netProfitMarginTTM` >= 0.20 | 5 | Strong |
| C | `ratios-ttm.netProfitMarginTTM` >= 0.15 | 4 | Good |
| D | `ratios-ttm.netProfitMarginTTM` >= 0.10 | 2 | Moderate |
| E | `ratios-ttm.netProfitMarginTTM` >= 0.05 | 1 | Low |
| F | else | 0 | None |

---

### Momentum

**Q5: 1-Month Price Change**
- **Endpoint:** `stock-price-change.1M`
- **Description:** 1-month price change %. FMP returns as percentage number (e.g., 20 = 20%).
- Max Points: 5 | Min Points: 0

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `stock-price-change.1M` >= 20 | 5 | Explosive |
| B | `stock-price-change.1M` >= 10 | 4 | Strong |
| C | `stock-price-change.1M` >= 5 | 2 | Moderate |
| D | `stock-price-change.1M` > 0 | 1 | Positive |
| E | else | 0 | Flat/Down |

---

**Q6: 10-Day Price Change**
- **Endpoint:** Computed `10dChangePercent` from `historical-price-eod`
- **Description:** 10-day price change %. Compute: `(close[0] - close[10]) / close[10] × 100`.
- Max Points: 4 | Min Points: 0

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `10dChangePercent` >= 15 | 4 | Strong |
| B | `10dChangePercent` >= 10 | 3 | Moderate |
| C | `10dChangePercent` >= 5 | 1 | Mild |
| D | else | 0 | Weak |

---

### Liquidity

**Q7: 20-Day Average Volume**
- **Endpoint:** `quote.avgVolume`
- **Description:** 20-day average trading volume.
- Max Points: 4 | Min Points: 0

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `quote.avgVolume` >= 1000000 | 4 | High Liquidity |
| B | `quote.avgVolume` >= 500000 | 3 | Moderate |
| C | `quote.avgVolume` >= 200000 | 1 | Low |
| D | else | 0 | Illiquid |

---

### Analyst & Institutions

**Q8: Ownership & Coverage**
- **Endpoints:** Computed `institutionalOwnershipPct` from `institutional-ownership`, Computed `analystCount` from `grades-consensus`
- **Description:** Conditional — +1 if institutional ownership > 0%, +1 if analyst ratings > 0. Points stack.
- Max Points: 2 | Min Points: 0

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `institutionalOwnershipPct` > 0 | +1 | Institutional |
| B | `analystCount` > 0 | +1 | Covered |
| — | Neither | 0 | No Coverage |

---

### Technical

**Q9: Price vs Moving Averages**
- **Endpoints:** `quote.price`, `sma(20).sma`, `sma(50).sma`
- **Description:** Current price vs 20-Day SMA and 50-Day SMA alignment.
- Max Points: 5 | Min Points: 0

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `quote.price` > `sma(20).sma` AND `quote.price` > `sma(50).sma` | 5 | Full Alignment |
| B | `quote.price` > `sma(50).sma` AND `quote.price` <= `sma(20).sma` | 4 | Above Trend |
| C | `quote.price` > `sma(20).sma` AND `quote.price` <= `sma(50).sma` | 2 | Short-term Only |
| D | else | 0 | Below Both |

---

### Financial Health

**Q10: Debt-to-Equity Ratio**
- **Endpoint:** `ratios-ttm.debtToEquityRatioTTM`
- **Description:** Total Debt / Total Equity. Evaluate in order — stop at first match.
- Max Points: 4 | Min Points: -3

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `ratios-ttm.debtToEquityRatioTTM` < 0 (negative equity) | -3 | Danger |
| B | `ratios-ttm.debtToEquityRatioTTM` < 0.5 | 4 | Excellent |
| C | `ratios-ttm.debtToEquityRatioTTM` < 1.0 | 3 | Good |
| D | `ratios-ttm.debtToEquityRatioTTM` < 2.0 | 1 | Acceptable |
| E | else | 0 | High Debt |

---

### Weighted Momentum

**Q11: Momentum Magnitude**
- **Endpoints:** `stock-price-change.1Y`, `stock-price-change.3M`
- **Description:** Formula: `stock-price-change.1Y` + `stock-price-change.3M`.
- Max Points: 3 | Min Points: 0

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | (`stock-price-change.1Y` + `stock-price-change.3M`) > 150 | 3 | Extreme |
| B | (`stock-price-change.1Y` + `stock-price-change.3M`) > 100 | 2 | Strong |
| C | (`stock-price-change.1Y` + `stock-price-change.3M`) > 50 | 1 | Moderate |
| D | else | 0 | Weak |

---

### EPS Growth

**Q12: EPS Growth Prior Year**
- **Endpoint:** `financial-growth(annual).epsgrowth`
- **Description:** EPS Growth % (most recent prior fiscal year). FMP returns as decimal (e.g., 1.0 = 100%).
- Max Points: 5 | Min Points: 0

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `financial-growth(annual).epsgrowth` >= 1.00 | 5 | Exceptional |
| B | `financial-growth(annual).epsgrowth` >= 0.50 | 4 | Strong |
| C | `financial-growth(annual).epsgrowth` >= 0.25 | 2 | Good |
| D | `financial-growth(annual).epsgrowth` > 0 | 1 | Positive |
| E | else | 0 | Negative |

---

### Returns

**Q13: Return on Equity (ROE)**
- **Endpoint:** `key-metrics-ttm.returnOnEquityTTM`
- **Description:** Return on Equity (TTM). FMP returns as decimal.
- Max Points: 2 | Min Points: 0

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `key-metrics-ttm.returnOnEquityTTM` >= 0.20 | 2 | Strong |
| B | `key-metrics-ttm.returnOnEquityTTM` >= 0.10 | 1 | Moderate |
| C | else | 0 | Weak |

---

**Q14: Return on Assets (ROA)**
- **Endpoint:** `key-metrics-ttm.returnOnAssetsTTM`
- **Description:** Return on Assets (TTM). FMP returns as decimal.
- Max Points: 3 | Min Points: 0

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `key-metrics-ttm.returnOnAssetsTTM` >= 0.15 | 3 | Excellent |
| B | `key-metrics-ttm.returnOnAssetsTTM` >= 0.10 | 2 | Good |
| C | `key-metrics-ttm.returnOnAssetsTTM` >= 0.05 | 1 | Moderate |
| D | else | 0 | Low |

---

### Country

**Q15: Country**
- **Endpoint:** `profile.country`
- **Description:** Company domicile from FMP profile.
- Max Points: 1 | Min Points: -2

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `profile.country` == "US" | 1 | USA |
| B | `profile.country` in ["CA","GB","NL","DE","FR","JP","AU","TW","KR","CH","IE","IL"] | 0 | Developed |
| C | else | -2 | China/EM |

---

### Risk Penalties

**Q16: Cash Burn Risk**
- **Endpoints:** `ratios-ttm.netProfitMarginTTM`, `cash-flow-statement(quarter).operatingCashFlow` (most recent), `quote.marketCap`
- **Description:** Evaluate in order — stop at first match. Combined cap with Q17: max total penalty -4.
- Max Points: 0 | Min Points: -3

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `ratios-ttm.netProfitMarginTTM` >= 0 | 0 | Profitable |
| B | `cash-flow-statement(quarter).operatingCashFlow` >= 0 | 0 | CF Positive |
| C | `quote.marketCap` >= 10000000000 | 0 | Large Cap Shield |
| D | else | -3 | Cash Burn |

**Note:** FMP returns `marketCap` as full raw number (e.g., 10000000000 for $10B). Do not treat as thousands.

---

**Q17: Deterioration Risk**
- **Endpoints:** `income-statement(quarter)` — compare most recent quarter vs same quarter prior year (offset 4 quarters)
- **Fields compared:** `income-statement(quarter)[0].revenue` vs `income-statement(quarter)[4].revenue`, `income-statement(quarter)[0].operatingIncome` vs `income-statement(quarter)[4].operatingIncome`, `cash-flow-statement(quarter)[0].operatingCashFlow` vs `cash-flow-statement(quarter)[4].operatingCashFlow`
- **Description:** All three declining vs same quarter prior year.
- Max Points: 0 | Min Points: -3

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `income-statement(quarter)[0].revenue` < `income-statement(quarter)[4].revenue` AND `income-statement(quarter)[0].operatingIncome` < `income-statement(quarter)[4].operatingIncome` AND `cash-flow-statement(quarter)[0].operatingCashFlow` < `cash-flow-statement(quarter)[4].operatingCashFlow` | -3 | Triple Decline |
| B | else | 0 | OK |

**Combined Penalty Cap (Q16+Q17):** If both trigger, apply **-4 total** (not -6).

---

### Trend & Strength

**Q18: Financial Strength**
- **Endpoints:** `ratios-ttm.netProfitMarginTTM`, `key-metrics-ttm.returnOnEquityTTM`, `ratios-ttm.debtToEquityRatioTTM`
- **Description:** Composite check. Evaluate in order — stop at first match.
- Max Points: 3 | Min Points: 0

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `ratios-ttm.netProfitMarginTTM` >= 0.20 AND `key-metrics-ttm.returnOnEquityTTM` >= 0.20 AND `ratios-ttm.debtToEquityRatioTTM` < 0.5 | 3 | Fortress |
| B | `ratios-ttm.netProfitMarginTTM` >= 0.10 AND `key-metrics-ttm.returnOnEquityTTM` >= 0.10 AND `ratios-ttm.debtToEquityRatioTTM` < 1.5 | 2 | Solid |
| C | `ratios-ttm.netProfitMarginTTM` >= 0 AND `key-metrics-ttm.returnOnEquityTTM` >= 0.05 AND `ratios-ttm.debtToEquityRatioTTM` < 3.0 | 1 | Adequate |
| D | else | 0 | Weak |

---

### Risk Detection

**Q19: Momentum Divergence Penalty**
- **Endpoints:** `stock-price-change.1Y`, `stock-price-change.3M`, `stock-price-change.1M`, computed `10dChangePercent`
- **Description:** Long-term up but all short-term periods negative = fading.
- Max Points: 0 | Min Points: -3

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `stock-price-change.1Y` > 0 AND `stock-price-change.3M` < 0 AND `stock-price-change.1M` < 0 AND `10dChangePercent` < 0 | -3 | Fading |
| B | else | 0 | OK |

---

**Q20: Sector Preference**
- **Endpoint:** `profile.sector`
- **Description:** Sector classification tilt. See Sector Classification Notes.
- Max Points: 2 | Min Points: -4

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `profile.sector` in ["Technology","Financial Services","Business Services","Industrials (Aerospace/Defence subset)"] | 2 | Favored |
| B | `profile.sector` in ["Consumer Defensive","Consumer Cyclical","Auto-Tires-Trucks","Retail","Industrial Products","Transportation","Utilities","Construction"] | 1 | Neutral+ |
| C | `profile.sector` in ["Energy","Basic Materials"] | 0 | Neutral |
| D | `profile.sector` in ["Crypto","Mining","Healthcare (Pharma/Biotech/Medical subset)"] | -4 | Penalized |

**Sector Classification Notes (hardcoded ticker overrides):**
- **Gold/Mining includes:** NEM, GFI, KGC, AU, HMY, CDE, HL, NGD, CGAU, AEM, GOLD, AG
- **Crypto includes:** IREN, MARA, CLSK, RIOT, BITF, WULF, HUT, CIFR, COIN, MSTR, CORZ, BTBT, HIVE, BTDR

---

### Range Position

**Q21: %B Position (Bollinger Bands — Momentum)**
- **Endpoint:** Computed `bollingerPercentB` from `quote.price`, `sma(20).sma`, `standarddeviation(20).standardDeviation`
- **Formula:** `upperBand = sma(20) + 2 × stddev(20)`, `lowerBand = sma(20) - 2 × stddev(20)`, `%B = (price - lowerBand) / (upperBand - lowerBand) × 100`
- **Description:** Bollinger Bands %B (Period 20, StdDev 2). Breakout also lifts Cyclical Sector Cap on Q1-Q3.
- Max Points: 5 | Min Points: 0

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `bollingerPercentB` > 100 | 5 | Breakout |
| B | `bollingerPercentB` > 95 | 4 | Near Top |
| C | `bollingerPercentB` >= 80 | 2 | Upper Zone |
| D | `bollingerPercentB` >= 20 | 1 | Mid-Range |
| E | else | 0 | Buy Zone |

---

### Momentum Quality

**Q22: Momentum Quality**
- **Endpoints:** `stock-price-change.1Y`, `stock-price-change.3M`, `stock-price-change.1M`, computed `10dChangePercent`
- **Description:** Pattern detection across timeframes. Evaluate in order — stop at first match.
- Max Points: 2 | Min Points: -1

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `10dChangePercent` > 20 AND `stock-price-change.1M` < 10 | -1 | Spike Risk |
| B | `stock-price-change.1Y` > 0 AND `stock-price-change.3M` > 0 AND `stock-price-change.1M` > 0 AND `stock-price-change.1Y` > `stock-price-change.3M` AND `stock-price-change.3M` > `stock-price-change.1M` AND `stock-price-change.1M` > `10dChangePercent` | +2 | Smooth |
| C | `stock-price-change.3M` > 0 AND (`stock-price-change.3M` × 4) > `stock-price-change.1Y` | +1 | Accelerating |
| D | else | 0 | Other |

---

### Risk Detection - Part 2

**Q23: High P/E Momentum Trap**
- **Endpoints:** `quote.pe`, computed `10dChangePercent`
- **Description:** Overvalued stock with declining price = value trap.
- Max Points: 0 | Min Points: -4

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `quote.pe` > 50 AND `10dChangePercent` < -5 | -4 | Trap |
| B | else | 0 | OK |

---

**Q24: Biotech Binary Event Burn**
- **Endpoints:** `profile.sector`, computed `10dChangePercent`
- **Description:** Medical/Pharma sectors with sudden spike = binary event risk.
- Max Points: 0 | Min Points: -3

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `profile.sector` in ["Healthcare"] AND `profile.industry` in ["Biotechnology","Drug Manufacturers","Medical Devices","Diagnostics & Research"] AND `10dChangePercent` > 15 | -3 | Binary Risk |
| B | else | 0 | OK |

---

**Q25: Sustained Downtrend**
- **Endpoints:** `stock-price-change.1D`, `stock-price-change.5D`, `stock-price-change.1M`
- **Description:** All short-term timeframes negative simultaneously.
- Max Points: 0 | Min Points: -3

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `stock-price-change.1D` < 0 AND `stock-price-change.5D` < 0 AND `stock-price-change.1M` < 0 | -3 | Downtrend |
| B | else | 0 | OK |

---

**Q26: Sudden Drop / Slide**
- **Endpoint:** `historical-price-eod` (last 5 trading days, close prices)
- **Description:** Compute daily close-to-close % drops for last 3 trading days. Also compute cumulative 5-day return. Triggered by HIGHEST matching tier only (no stacking). Self-heals when drop exits 3-day window.
- Max Points: 0 | Min Points: -6

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | Any single day `(close[d] - close[d-1]) / close[d-1]` <= -0.15 within last 3 days | -6 | Critical |
| B | Any single day `(close[d] - close[d-1]) / close[d-1]` <= -0.10 within last 3 days | -2 | Severe |
| C | Any single day `(close[d] - close[d-1]) / close[d-1]` <= -0.07 within last 3 days, OR `(close[0] - close[5]) / close[5]` <= -0.10 | -1 | Caution |
| D | else | 0 | OK |

---

**Q27: Short Interest Risk**
- **Endpoint:** External source — `shortPercentFloat` (not native FMP)
- **Description:** Short % of float. High short = amplified volatility.
- Max Points: 0 | Min Points: -1

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `shortPercentFloat` > 20 | -1 | High Short |
| B | else | 0 | OK |

---

**Q28: Low Float Risk**
- **Endpoint:** `shares-float.floatShares`
- **Description:** Float shares count. Low float = amplified price swings.
- Max Points: 0 | Min Points: -1

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `shares-float.floatShares` < 20000000 | -1 | Low Float |
| B | else | 0 | OK |

---

**Q29: Sector Performance vs Peers**
- **Endpoints:** `stock-price-change.1M`, computed `sectorAvg1M` (from sector peers or `/stable/historical-sector-performance`)
- **Description:** Stock 1M return vs sector avg 1M return.
- Max Points: +1 | Min Points: -1

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | (`stock-price-change.1M` - `sectorAvg1M`) > 10 | +1 | Leader |
| B | abs(`stock-price-change.1M` - `sectorAvg1M`) <= 10 | 0 | In-Line |
| C | (`stock-price-change.1M` - `sectorAvg1M`) < -10 | -1 | Laggard |

---

**Q30: 5-Day Relative Strength (Alpha)**
- **Endpoints:** `stock-price-change.5D` (stock), `stock-price-change.5D` for QQQ (market benchmark)
- **Formula:** `alpha = stock.5D - QQQ.5D`
- **Description:** Stock 5D % minus QQQ 5D %. Evaluate in order — stop at first match.
- Max Points: +3 | Min Points: -3

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | `stock.stock-price-change.5D` > 0 AND `QQQ.stock-price-change.5D` < 0 | +3 | True Alpha |
| B | `alpha` >= 5 | +2 | Beating Market |
| C | `alpha` >= 0 | +1 | Keeping Pace |
| D | `alpha` >= -5 | 0 | Slight Lag |
| E | `alpha` < -5 | -2 | Badly Lagging |
| F | `stock.stock-price-change.5D` < 0 AND `QQQ.stock-price-change.5D` > 0 | -3 | Stock Problem |

---

**Q31: Trend Deterioration (Lower Lows & Lower Highs)** ★ PENALTY INCREASED
- **Endpoint:** `historical-price-eod` (last 30 trading days, OHLC)
- **Description:** Computed from swing highs/lows. Penalty increased from -3 to -10. Primary risk filter.
- Max Points: 0 | Min Points: **-10** (was -3 in V17)

**Calculation:**
1. From `historical-price-eod` last 30 days, extract `high` and `low` for each day
2. Find swing highs: days where `high[d]` > `high[d-2]` AND `high[d]` > `high[d-1]` AND `high[d]` > `high[d+1]` AND `high[d]` > `high[d+2]`
3. Find swing lows: days where `low[d]` < `low[d-2]` AND `low[d]` < `low[d-1]` AND `low[d]` < `low[d+1]` AND `low[d]` < `low[d+2]`
4. Compare last 2-3 swing highs: are they decreasing?
5. Compare last 2-3 swing lows: are they decreasing?
6. Both decreasing → penalty

| Cond | Condition | Pts | Label |
|------|-----------|-----|-------|
| A | Lower highs AND lower lows (2+ swing points each) | **-10** | Structural Downtrend |
| B | else | 0 | OK |

---

## Final Score Calculation
- **Raw Score** = Sum of assigned points from all questions
- **Raw Score = Final Score** (no normalization)

**Config Reference:**
- **Max Raw Score:** 95 points
- **Min Raw Score:** -49 points (with Q16+Q17 cap applied)
- **Reserve:** 5 points for future questions (→ 100 max)

---

## Quick Reference: V17 → V19 Point Changes

| Q | Name | V17 | V19 | Change |
|---|------|-----|-----|--------|
| 1 | Sales Growth | 6 | **14** | ★ 2× weight |
| 2 | OpInc Growth | 6 | **7** | scaled |
| 3 | Cash Flow Growth | 6 | **14** | ★ 2× weight |
| 4 | Net Profit Margin | 5 | **6** | scaled |
| 5 | 1M Price Change | 4 | **5** | scaled |
| 6 | 10D Price Change | 3 | **4** | scaled |
| 7 | Volume | 3 | **4** | scaled |
| 8 | Ownership | 2 | 2 | — |
| 9 | Price vs MAs | 4 | **5** | scaled |
| 10 | Debt/Equity | 3/−3 | **4**/−3 | pos scaled |
| 11 | Momentum Mag | 3 | 3 | — |
| 12 | EPS Growth | 4 | **5** | scaled |
| 13 | ROE | 2 | 2 | — |
| 14 | ROA | 3 | 3 | — |
| 15 | Country | 1/−2 | 1/−2 | — |
| 16 | Cash Burn | 0/−3 | 0/−3 | — |
| 17 | Deterioration | 0/−3 | 0/−3 | — |
| 18 | Financial Str | 3 | 3 | — |
| 19 | Mom Divergence | 0/−3 | 0/−3 | — |
| 20 | Sector Pref | 2/−4 | 2/−4 | — |
| 21 | %B Position | 4 | **5** | scaled |
| 22 | Mom Quality | 2/−1 | 2/−1 | — |
| 23 | P/E Trap | 0/−4 | 0/−4 | — |
| 24 | Biotech Binary | 0/−3 | 0/−3 | — |
| 25 | Sustained Down | 0/−3 | 0/−3 | — |
| 26 | Sudden Drop | 0/−6 | 0/−6 | — |
| 27 | Short Interest | 0/−1 | 0/−1 | — |
| 28 | Low Float | 0/−1 | 0/−1 | — |
| 29 | Sector vs Peers | 1/−1 | 1/−1 | — |
| 30 | 5D RS | 3/−3 | 3/−3 | — |
| 31 | Trend Det | 0/−3 | 0/**−10** | ★ penalty 3.3× |
| | **TOTAL POS** | **70** | **95** | |

---

## Items Requiring Your Decision

**1. Cyclical Sector Cap value:**
V17 capped Q1/Q2/Q3 at 4 pts each when max was 6 (67%). Now Q1/Q3 max is 14 and Q2 max is 7. Cap kept at 4 → only 29% of Q1/Q3 max. Options:
- Keep at 4 (more restrictive against cyclicals)
- Scale proportionally (~9 for Q1/Q3, ~5 for Q2, maintaining 67% ratio)

**2. Combined Penalty Cap (Q16+Q17):**
Kept at -4 (from V17). Confirm OK.

**3. FMP field name note — `stock-price-change.1D`:**
User confirmed `5D` field is `5dChangePercent`. Verify if `1D` field is `1dChangePercent` or `1D` in your FMP responses. Same for `1M`, `3M`, `1Y`.

---

**End of Stock Analysis Score Instructions**
