# Module-4 — Signals
**Lovable Trade V18 — Updated 2/26/2026**

* This module consolidates all color coding, grading, alerts, and action signals in one place.
* There are multiple signals and alerts to cummunicates action suggestions ke modifiers
**Market Signal:** The master signals communicatong the overall market condition. they appear on the MC top bar.
**Action Signals:** This is the main buy or sell signal based on SA score and combination of it with MC and VIX. They appear in Signals column in Stock analysis table.
**Alerts:** The supplemental information about subjective events, changes or news articles, they sppear as on icon next to the symbol with an extension panel.
**Matrix Signals:** These signals are issued based on review of SA patterns and wqhat they mean as a secondary signal. They are displayed in the Chart columns.
**Holding Signals:** Both the main stock signals and SA chart pattern signals also offer advice for those who are holding the stock. they appear in the Hold column in two lines.

---

## Required Input Data

| Field | Source | Description |
|-------|--------|-------------|
| **SA Score** | Module 2 (Analysis) — Normalized Score | 
| **MC Score** | Module 3 (Market) — Normalized Score | 
| **VIX Level** | FMP API — `^VIX` Current Price (Level) | CBOE Volatility Index spot value |
| **Net Profit Margin** | Module 1 Q4 / FMP API — `Net Income ÷ Revenue (TTM)` | Used for Tier profitability check |
| **Market Cap** | FMP API — `/api/v3/profile/{symbol}` → `mktCap` | Full raw number (e.g., 50,000,000,000 = $50B) |
| **Annual Revenue Growth %** | Module2 Q1 / FMP API | Used for Tier T3 "growth" condition |

---

# Part 1 — Score Grades (Display Only)

Score Grades are **informational labels and colors** applied to SA and MC scores for display purposes.
They help contextualize the Master Signals but do not drive any actions on their own.

## SA Score Grades

| SA Score | Title | Color |
|----------|-------|-------|
| 80 to 99 | Elite Stock | t-green |
| 70 to 79 | Solid Stock | t-teal |
| 60 to 69 | With Potential | t-yellow |
| 50 to 59 | Monitor Worthy | t-orange |
| 40 to 49 | Weak Stock | t-red |
| < 40 | Avoid This Stock | t-red-2 |

## MC Score Grades

| MC Score | Title | Color |
|----------|-------|-------|
| ≥ 76 | Overheated Market | t-red |
| 61 to 75 | Heated Market | t-yellow |
| 40 to 60 | Normal Market | t-green |
| 30 to 39 | Sub-Normal Market | t-yellow |
| 10 to 29 | Weak Market | t-orange |
| < 10 | Frozen Market | t-red |

## VIX Score Grades
High VIX = elevated fear = historically a buying opportunity. Colors reflect opportunity level, not danger level.

| VIX Level | Title | Color |
|-----------|-------|-------|
| > 30 | Extreme Fear — Great Buying Opportunity | t-green |
| 25–29 | High Fear — Buying Opportunity | t-teal |
| 20–24 | Elevated Worry | t-blue |
| 15–20 | Normal Fluctuation | t-blue |
| < 15 | Traders Discoraged | t-orange |

---

# Part 2 — Alerts (Display Only)

Alerts are **non-scoring** visual indicators that provide context beyond scores.
They do not modify scores. They appear in tables, cards, and icons based on instructions.
Source from FMP API when available. Yahoo and Google Finance and web search otherwise.
Search the sources above to find any of the situations below; if found, add the Alert message
from the tables below. Accompany the message with the related color.

## Alert Display Rules
The alert bell icon appears to the left of symbols. Show the same icon when alerts exist.
The color of the icon is selected based on the categories below.
Clicking on an alert icon opens an extension panel with the content of the Alert below.

## Red Alerts (Negative / Risk)
**Color: t-red**

| Alert | Trigger |
|-------|---------|
| SEC Investigation | Active SEC investigation, fraud, restatement |
| Legal Issues | Lawsuit, hearing, investigation, ruling news about the company or top executives |
| Forward Guidance Shows Decline | Forward guidance lowered by the company |
| Downgraded by Analysts | Analyst downgraded the stock within the last 30 days |

## Yellow Alerts (Caution / Neutral)
**Color: t-yellow**

| Alert | Trigger |
|-------|---------|
| Earning Date Close | Earnings date is within the next 7 days |
| IPO (New Company) | Company's IPO was listed within the last 7 days |
| Healthcare / Binary Event Risk | Sector is Healthcare, Medical, Pharma, Pharmaceutical, Biotechnology, Medical Devices, Drug Manufacturers, Health Care, Diagnostics & Research, Medical Instruments & Supplies, Pharmaceutical Retailers, or Health Information Services. Rationale: exposed to FDA decisions, clinical trials, patent cliffs. |

## Green Alerts (Positive / Opportunity)
**Color: t-green**

| Alert | Trigger |
|-------|---------|
| Positive Guidance | Forward guidance is raised |
| Upgrade by Analysts | Analysts upgraded the stock within the last month |

---

### Market Level Signal

In the MC bar results, show an alert for important upcoming events or news headlines that may/have/can affect the market.
Use the same data sources you use sources Including API, Google and Yahoo Finance, and other reliable financial and company publications.
Alerts for events are only triggered when the event is happening within the next three days.

These are some examples:
Consumer Price Index (CPI) [HIGH] (Sat, Jan 10) — Inflation over 2% can hurt the market significantly.
FOMC Meeting [HIGH] (Wed, Jan 28) — Rate decision expected. Over correction can move the market significantly.
Earnings Season Peak [MEDIUM] (Mid-Jan) — Elevated single-stock volatility.

#### How to display
Show a large alert icon with a vertical separator in front of the 'Signal' and when clicked on display it in an extension panel.
**Format:** Event Name [HIGH/MEDIUM/LOW] — One-line description (date)

---

# Part 3 — Action Signals for Stocks

Stock Signals are the **final action signals**. Actions are based on these signals.
They are determined by the relationship between SA, MC, and VIX using conditional logic.

Signals for stocks and market condition are determined separately.
Market Signal is displayed in the top MC bar.
Stock Action Signal is displayed in the main analysis table in each stock's row in the Signals column.

## Table Columns — Signal Display
Each stock row displays two signal-related columns:
- **Signals** — The main action signal determined by SA score, MC, and VIX logic (this file).
- **Chart** — Secondary score-movement confirmations based on SA history (see Matrix Movement Confirmations). Displayed alongside Signal in Chart column. Both columns are always visible. They may occasionally differ — this is intentional.

---

## Signal Determination

### Market Signal
- Determine Active Condition. Select Market Signal.
- **Fields:** VIX Level (`^VIX` Price from FMP), MC Score (From Module 2 Normalized)
- Place the Market Signal to the right of VIX number

| Priority | Signal | Holding Signal | Condition | Color |
|----------|--------|---------|-------|
| 1 | VIX Override — Max Fear — Aggressive Buy (Including QQQ) | Hold snd Add | VIX ≥ 30 | t-green |
| 1 | VIX Override — High Fear — Confident Buy (Including QQQ) | Hold and Add | VIX 25–29 | t-teal
| 2 | Very Weak Market Wait for Opportunity | Consider Exit Positions | MC < 20 | t-orange |
| 3 | Slow Market — Be Careful | Reduce Risk | MC 20–39 | t-yellow |
| 4 | Over-Heated Market — Only Great Stocks | Exit Risky Positions | MC ≥ 81 | t-blue |
| 5 | Heated Market — Buy Carefully | Hold with Stops | MC 61–80 | t-orange |
| 6 | Normal Market — Buy Quality Stocks | Hold Quality Stocks | MC 40–60 | t-green |

---

### Stock Signal
1. Based on the Normalized Score of Module 2 or SA Test Score.
2. Each stock gets its own signal.
3. If VIX and MC Override don't superseed the action, find and display the signal for the stock below as well. 

| SA Score Condition | Signal | Holding Signal | Color |
|--------------------|--------|----------------|-------|
| ≥ 80 | Buy in Good Market | Hold and Add if Tier Allows | t-green |
| 75–79 | Buy if Stable | Hold and Add if Tier Allows | t-teal |
| 70–74 | Consider Buying | Consider Selling — Add 10% Trailing Stop Loss | t-blue |
| 60–69 | Monitor | Sell Low Quality. Add tight Stops | t-yellow |
| 35–59 | Find a Better Stock | Sell Them | t-orange |
| < 35 | Avoid the Stock | Sell All t-red |

**Exception — VIX Override**
**Trigger:** VIX Level (FMP `^VIX` Price) ≥ 25.
- **Signal column:** Overwritten with the VIX Override signal (Max Fear or High Fear).
- **Chart column:** VIX Override alert is added alongside the existing Pattern message.
- The Chart signal is not replaced — both are shown so the user can see the score movement context during the override.

---

## Filters and Exceptions
These filters apply only to buy-type signals. Non-buy signals are not affected.
the signals below take over and replace the regular signals.

### 1. Crypto Filter
- **Applies to:** IREN, MARA, CLSK, RIOT, BITF, WULF, HUT, CIFR, COIN, MSTR, CORZ, BTBT, HIVE, BTDR
- **Trigger:** Any Buy-type signal

| Condition | Replacement Signal | Color |
|-----------|--------------------|-------|
| Symbol is in crypto list AND signal is Buy-type | Don't Buy (Crypto) | t-red |
| Otherwise | No change | — |

### 2. Basic Materials Sector Cap (Max 2)
- **Applies to Sectors:** Basic Materials, Mining
- **Trigger:** 3 or more stocks in these sectors qualify for buy signals in the same scan

| Condition | Replacement Signal | Color |
|-----------|--------------------|-------|
| Top 2 by SA score (tiebreak: higher Net Profit Margin) | No change | — |
| 3rd stock and beyond | Don't Buy (Sector Cap) | t-yellow |

### 3. Unprofitable Stock Override
- **Trigger:** Net Profit Margin < 0%
- **Applies to signals:** Buy in Good Market, Buy if Stable, Consider Buying

| Condition |Replacement Signal | Color |
|-----------|-------------------|-------|
| Net Profit Margin < 0% AND signal is Buy-type | Append "(Unprofitable)" to signal label | t-yellow |
| Otherwise | No change | — |

### 4. Healthcare / Binary Event Risk
- **Trigger:** Stock's sector is Healthcare, Medical, or Pharma.
- **Impact:** Warns that healthcare stocks carry binary event risk from FDA decisions, clinical trial results, drug approvals/rejections, and patent cliffs.

| Condition | Replacemlent Signal | Color |
|-----------|---------------------|-------|
| Sector is Healthcare, Medical, Pharma, Biotech, Drug Manufacturers | Append "(Medical)" to Signal Label | t-yellow |

---

# Part 4 — Tiers (Position Sizing)

- Tiers define the max position size per stock.
- **Note:** Tiers are risk caps, not quality rankings. Score determines quality; tier determines maximum position size based on risk profile.

### Tier Field Definitions

| Field | Source | Definition |
|-------|--------|------------|
| SA Score | Module 2 Normalized Score | `((Raw Score + 50) / 123) * 100` |
| Profitable | FMP API — Net Profit Margin (TTM) | Net Profit Margin ≥ 0% |
| Market Cap | FMP API — `/api/v3/profile/{symbol}` → `mktCap` | Full raw number. $50B = 50,000,000,000 |
| Growth | FMP API — Annual Revenue Growth % | Annual Revenue Growth % > 0% |
| Small Profitable | FMP API — Net Profit Margin (TTM) | Net Profit Margin > 0% AND Market Cap ≤ $2B |

## Portfolio Concentration Limits

| Tier | SA Condition | Company Condition | Max Position Size | Color |
|------|--------------|-------------------|-------------------|-------|
| T1 | ≥ 65 | Profitable (Net Profit Margin ≥ 0%) + Market Cap > $50B | $100,000 | t-green |
| T2 | ≥ 65 | Profitable (Net Profit Margin ≥ 0%) + Market Cap > $2B | $50,000 | t-blue-2 |
| T3 | ≥ 65 | Market Cap > $100M + (Growth > 0% OR Small Profitable) | $20,000 | t-yellow |
| SELL | Does not qualify for any tier | $0 — Do not buy | t-red |

---

## Star Rating (1–5 ★)
The rating is purely informational and independent of the SA scoring engine.
Displayed in the **Stars** column in the main stock table. A visual guide only — one point per criterion met.

| Criterion | Condition |
|-----------|-----------|
| P/E Ratio | Between 0 and 25 |
| Net Profit Margin | > 15% |
| ROE | > 15% |
| D/E Ratio | Between 0 and 1 |
| Revenue Growth | > 10% |

**Total stars = count of criteria met (0–5).**

---

## Matrix Movement Confirmations

The following messages are applied to stocks based on SA score movements, price movements, and stability of changes.

**Confirmation Rule:** Day 0 = trigger fires. Day 1 = still holds. Day 2 = ACT.
Waiting 3 days filters out 39–46% of false signals with no meaningful cost to returns.

**Display:** Shown in the **Chart** column, next to the main Signal column.
The Chart column is independent — both columns are always visible so users can compare.
Chart signals are score-movement based and may occasionally differ from the main Signal column. This is intentional.

---

### 1. Fresh Cross Signals
*Score crosses a threshold for the first time — confirmed over 3 days.*
Confirmed 80+ crossings achieve 70–78% win rates vs 66% for instant entry. Confirmed exits below 65 reduce average return to -12% vs -3% unconfirmed.

#### Entry

| Message | Holding Message | Conditions | Color |
|---------|-----------------|------------|-------|
| 3D of 80+ | Continue Hiolding | SA crosses above 80, holds 3 days | t-green |
| 3D of 75+ | Continue Holding | SA crosses above 75, holds 3 days | t-teal |
| 3D of 70+ | Consider Selling | SA crosses above 70 and holds for 3 days | t-blue |

#### Exit

| Message | Holding Message | Conditions | MC Filter | Color |
|---------|-----------------|------------|-----------|-------|
| Do Not Buy | Under 65 exit | SA crosses below 65, holds 3 days | t-red |
| Wait and Monitor | Under 70 exit | SA crosses below 70, holds 3 days | t-orange |
| Reduce Position | SA crosses below 75, holds 3 days | t-orange |
| Move Under 80. Monitor | Watch Carefully | SA crosses below 80, holds 3 days | Any | t-yellow |

---

### 2. Sustained Level Signals
**Score already in a zone — confirming stability or recovery.**
Stocks that dip and recover outperform those that don't dip at all. Recovery within 3 days is a hold signal, not an exit.

| Message | Holding Message | Conditions | Color |
|---------|------------|-------|
| Good Buy Time | Drop 80 Recovery Hold |  SA drops below 80, recovers within 3 days | t-green |
| OK to Buy | Drop 75 Recovery | SA drops below 75 - Hold | recovers on the next day | t-teal |
| Ready to Buy | Drop 70 Recovery | SA drops below 70 - Consider Selling | recovers on the next day | t-yellow |

---

### 3. Gradual Decline Signals
*Score drops ≥ 5 pts over 3–4 days with no single-day recovery > 1 pt.*
Gradual declines landing above 75 produce 78–89% win rates — stronger than fresh entries. Gradual declines landing below 65 confirm deterioration and are a sell signal.

| Message | Holding Message | Conditions | MC Filter | Color |
|---------|-----------------|------------|-----------|-------|
| 6+ Drop | Consider Selling | SA score drops over 5 points (not crossing 65) within two days and stays down for two days | t-yellow |
| 6+ Drop Recovery | Watch Carefully | SA score drops 6 points or more (not crossing 65) but recovers the next day | t-yellow |

---

### 4. Key Score Boundaries

| Level | Meaning | Action |
|-------|---------|--------|
| 80 | Elite zone entry | Buy on confirmed 3-day cross |
| 75 | Secondary entry / caution exit | Entry in MC < 70 only; tighten stops if confirmed below |
| 70 | Danger zone | Confirmed drop = reduce or sell (MC 50+) |
| 65 | Exit line | Confirmed drop = sell |


---

### 5. What NOT to Act On

| Condition | Reason |
|-----------|--------|
| Score rises 5+ pts into any zone | Rising scores underperform stable ones — no predictive value |
| Drop below 80, recovers Day 1 | False alarm 33% of the time — do not exit |
| Score drops 5–10 pts, stock stays above 75 | Buy the dip — not a sell signal |
| Any exit signal when MC < 30 | Market oversold — stock typically recovers |
| Cross above 70 or lower | Signal too weak below 75 |

---

**End of Signals Instructions**
