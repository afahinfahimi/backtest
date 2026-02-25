# Module-4 — Signals
**Lovable Trade V17 — Updated 2/23/2026**

This module consolidates all color coding, grading, alerts, and action signals in one place.
Modules 1 (Analysis) and 2 (Market) focus solely on calculating scores. This module interprets them.

---

## Required Input Data

| Field | Source | Description |
|-------|--------|-------------|
| **SA Score** | Module 1 (Analysis) — Normalized Score | `((Raw Score + 50) / 125) * 100`. Range: 0–100 |
| **MC Score** | Module 2 (Market) — Normalized Score | `((Raw Score + 40) / 92) * 100`. Range: 0–100 |
| **VIX Level** | FMP API — `^VIX` Current Price (Level) | CBOE Volatility Index spot value |
| **Net Profit Margin** | Module 1 Q4 / FMP API — `Net Income ÷ Revenue (TTM)` | Used for Tier profitability check |
| **Market Cap** | FMP API — `/api/v3/profile/{symbol}` → `mktCap` | Full raw number (e.g., 50,000,000,000 = $50B) |
| **Annual Revenue Growth %** | Module 1 Q1 / FMP API | Used for Tier T3 "growth" condition |

---

# Part 1 — Score Grades (Display Only)

Score Grades are **informational labels and colors** applied to SA and MC scores for display purposes.
They help contextualize the Master Signals but do not drive any actions on their own.

## SA Score Grades

| SA Score | Grade | Color |
|----------|-------|-------|
| 80 to 99 | Elite | t-green |
| 70 to 79 | Solid | t-teal |
| 60 to 69 | Potential | t-yellow |
| 50 to 59 | In Transition | t-orange |
| 40 to 49 | Weak | t-red |
| < 40 | Avoid | t-red-2 |

## MC Score Grades

| MC Score | Grade | Color |
|----------|-------|-------|
| ≥ 76 | Overheated | t-red |
| 61 to 75 | Heated | t-yellow |
| 40 to 60 | Normal | t-green |
| 30 to 39 | Sub-Normal | t-yellow |
| 10 to 29 | Weak | t-orange |
| < 10 | Very Weak | t-red |

## VIX Score Grades
| VIX Score | Color |
|-----------|-------|
| > 30 | t-green |
| 25-29 | t-teal |
| 20-24 | t-blue |
| 15-20 | t-blue |
| < 15 | t-orange |

---

# Part 2 — Alerts (Display Only) - For Stocks

Alerts are **non-scoring** visual indicators that provide context beyond scores.
They do not modify scores. They appear in tables, cards, and icons based on instructions.
Source from FMP API when available. Yahoo and Google Finance and web search otherwise.
Search the sources above to find any of the situations below; if found, add the Alert message
from the tables below. Accompany the message with the related color.

## Alert Display Rules
The alert bell icon appears to the left of symbols. Show the same icon when alerts exist. 
The color of icon is selected based on the categories below.
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

### Market Level Alerts

In the MC bar results, show an alert for important upcoming events or news headlines that may/have/can affect the market.
Use the same data sources you use for stock alerts above. Including API, Google and Yahoo finance, other reliable financial and company publications.
Alert for events are only triffered when the event is happening within the next three days. .

These are some examples:
Consumer Price Index (CPI) [HIGH] (Sat, Jan 10) — Inflation over 2% can hurt the market significantly.
FOMC Meeting [HIGH] (Wed, Jan 28) — Rate decision expected. Over correction can move the market significantly.
Earnings Season Peak [MEDIUM] (Mid-Jan) — Elevated single-stock volatility

#### How to display
Show a large alert icon with a vertical separator in front of the 'Signal' and when clicked on display it in an extension panel.
**Format:** Event Name [HIGH/MEDIUM/LOW] (Date) — One-line description

---

# Part 3 — Action Signals for Stocks

Stock Signals are the **final action signals**. Actions are based on these signals.
They are determined by the relationship between SA, MC, and VIX using conditional logic.

Signals for stocks and market condition are determined separately.
Market Signal is displayed in the top MC bar.
Stock Action Signal is displayed in the main analysis table in eash stock's row. 

---

## Signal Determination

### Market Signal
- Determine Active Condition. Select Market Signal.
- **Fields:** VIX Level (`^VIX` Price from FMP), MC Score (From Module 2 Normalized)
- Place the Market Signal to the right of VIX number

| Priority | Signal | Trigger |
|----------|-----------|---------|
| 1 | VIX Override - Max Fear - Aggressive Buy (Include QQQ) | VIX ≥ 30 |
| 1 | VIX Override - High Fear - Confident Buy (Include QQQ) | VIX 25-29 |
| 2 | Very Slow Market - Stay on the Sideline | MC < 20 |
| 3 | Over-Heated Market - Only Great Stocks | MC > 80 |
| 4 | Normal Market - Buy Quality Stocks | MC 40-60 |
| 5 | Heated Market - Buy Carefuly | MC 60-80 |
| 6 | Slow Market - Monitor | MC 20-39 |

---

### Stock Signal 
1. Based on the Normalized Score of Module-1 or SA Test Score.
2. Each stock gets its own signal
3. If VIX and MC Override don't superceed the action find the signal for the stock below

| SA Score | Signal | Current Holdings Actions | Color |
|--------------|--------|--------------------------|-------|
| > 80 | Buy in Good Market | Hold and Add if Tier Allows | t-green |
| 75-79 | Buy if Stable | Hold and Add if Tier Allows | t-teal |
| 70-74 | Consider Buying | Consider Selling - Add 10% Trailing Stop Loss | t-blue |
| 60-70 | Monitor | Sell if Holding | t-yellow |
| 35-59 | Find a Better Stock | Sell if Holding | t-orange |
| < 35 | Avoid the Stock | Sell if holding | t-red |

**Exceptions**
1: VIX Override: - **Trigger:** VIX Level (FMP `^VIX` Price) ≥ 25

---

## Filters and Exceptions
These filters do not apply to non buy signals. only changes signals that include 'buy' in the signal.

### 1. Crypto Filter
- **Applies to:** IREN, MARA, CLSK, RIOT, BITF, WULF, HUT, CIFR, COIN, MSTR, CORZ, BTBT, HIVE, BTDR
- **Trigger:** Any Buy-type signal

| Condition | Signal Override | Color |
|-----------|-----------------|-------|
| Symbol is in crypto list AND signal is Buy-type | No Buy (Crypto) | t-red |
| Otherwise | No change | — |

### 2. Basic Materials Sector Cap (Max 2)
- **Applies to Sectors:** Basic Materials, Mining
- **Trigger:** 3 or more stocks in these sectors qualify for buy signals in the same scan

| Condition | Signal Override | Color |
|-----------|-----------------|-------|
| Top 2 by SA score (tiebreak: higher Net Profit Margin) | No change | — |
| 3rd stock and beyond | No Buy (Sector Cap) | t-yellow |

### 3. Unprofitable Stock Override
- **Trigger:** Net Profit Margin < 0%
- **Applies to signals:** Buy, Selective Buy, Aggressive Buy, Careful Buy

| Condition | Signal Override | Color |
|-----------|-----------------|-------|
| Net Profit Margin < 0% AND signal is Buy-type | Append "(Unprofitable)" to signal label | t-yellow |
| Otherwise | No change | — |

---

## Part 4 — Tiers (Position Sizing)

- Tiers define the max position size per stock.
- **Note:** Tiers are risk caps, not quality rankings. Score determines quality; tier determines maximum position size based on risk profile.

### Tier Field Definitions

| Field | Source | Definition |
|-------|--------|------------|
| SA Score | Module 1 Normalized Score | `((Raw Score + 42) / 112) * 100` |
| Profitable | FMP API — Net Profit Margin (TTM) | Net Profit Margin ≥ 0% (from Module 1 Q4 field: `Net Income ÷ Revenue`) |
| Market Cap | FMP API — `/api/v3/profile/{symbol}` → `mktCap` | Full raw number. $50B = 50,000,000,000. $2B = 2,000,000,000. $100M = 100,000,000 |
| Growth | FMP API — Annual Revenue Growth % | Annual Revenue Growth % > 0% (from Module 1 Q1 field) |
| Small Profitable | FMP API — Net Profit Margin (TTM) | Net Profit Margin > 0% AND Market Cap ≤ $2B |

## Portfolio Concentration Limits

| Tier | SA Condition | Company Condition | Max Position Size | Color |
|------|-------------|-------------------|-------------------|-------|
| T1 | ≥ 65 | Profitable (Net Profit Margin ≥ 0%) + Market Cap > $50B | $100,000 | t-green |
| T2 | ≥ 65 | Profitable (Net Profit Margin ≥ 0%) + Market Cap > $2B | $50,000 | t-blue-2 |
| T3 | ≥ 65 | Market Cap > $100M + (Growth: Annual Revenue Growth > 0% OR Small Profitable: Net Profit Margin > 0% AND Market Cap ≤ $2B) | $20,000 | t-yellow |
| SELL | Does not qualify for any tier | $0 — Do not buy | t-red |

---

## MC Zone Penalty — SA Score Adjustment

**Applies to: Module 1 (Stock Analysis) final score**

---

## Overview

After calculating the SA Score (Module 1) and MC Score (Module 2), apply a penalty to the SA Score based on how far the MC Score is from the neutral zone.

---

## MC Score Grades

| MC Score | Penalty Points | Color |
|----------|----------------|-------|
| ≥ 76 | -10 | t-red |
| 61 to 75 | -5 | t-yellow |
| 40 to 60 | 0 | t-green |
| 30 to 39 | -5 | t-yellow |
| 10 to 29 | -10 | t-orange |
| > 15 | -15 | t-red

---

## Calculation Rules

1. **Calculate SA Score first** (Module 1, normalized).
2. **Calculate MC Score** (Module 2, normalized).
3. **Apply penalty** to produce the Adjusted SA Score.
4. **Use Adjusted SA Score** for all downstream logic and to Signals (Module 4), Tiers, and display.
5. The original (unadjusted) SA Score is preserved and displayed in score extension panel along with the penalty points.
6. Add a white border around the SA sccore when penaalty is applied.


---


**End of Signals Instructions**


















