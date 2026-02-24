# Module-4 — Signals
**Lovable Trade V17 — Updated 2/23/2026**

This module consolidates all color coding, grading, alerts, and action signals in one place.
Modules 1 (Analysis) and 2 (Market) focus solely on calculating scores. This module interprets them.

---

## Required Input Data

| Field | Source | Description |
|-------|--------|-------------|
| **SA Score** | Module 1 (Analysis) — Normalized Score | `((Raw Score + 42) / 112) * 100`. Range: 0–100 |
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
| ≥ 70 | Too Strong | a-green |
| 55 to 70 | Strong | t-green |
| 30 to 54 | Normal | t-blue |
| 10 to 29 | Weak | t-yellow |
| < 10 | Very Weak | t-red |

---

# Part 2 — Alerts (Display Only) - For Stocks

Alerts are **non-scoring** visual indicators that provide context beyond scores.
They do not modify scores. They appear in tables, cards, and icons based on instructions.
Source from FMP API when available. Yahoo and Google Finance and web search otherwise.
Search the sources above to find any of the situations below; if found, add the Alert message
from the tables below. Accompany the message with the related color.

## Alert Display Rules
The alert columns show the same icon when alerts exist. They just show different color.
Clicking on an alert opens a toggle box with the content of the Alert below.

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
Use the same data sources you use for stock alerts above. The timing for event is when the event is within the next two weeks.
Search both the API and web search of any reliable financial news source.

These are some examples:
Consumer Price Index (CPI) [HIGH] (Sat, Jan 10) — Core inflation trending toward 2%
FOMC Meeting [HIGH] (Wed, Jan 28) — Rate decision expected
Earnings Season Peak [MEDIUM] (Mid-Jan) — Elevated single-stock volatility

#### How to display
Show a large alert icon with a vertical separator in front of the 'Signal' and when clicked on it display it as a box added to the MC details panel.
**Format:** Event Name [HIGH/MEDIUM/LOW] (Date) — One-line description

---

# Part 3 — Master Signals (Action Signals)

Master Signals are the **final action signals**. Actions are based on these signals.
They are determined by the relationship between SA, MC, and VIX using conditional logic.

Signals are determined separately for the **Market** (one result, displayed in the top bar) and for each **Stock** (per row in the results table).

---

## Signal Evaluation Logic

### Step 1: Determine Active Condition
- **Fields:** VIX Level (`^VIX` Price from FMP), MC Score (Module 2 Normalized)
- Evaluate in order — stop at first match:

| Priority | Condition | Trigger |
|----------|-----------|---------|
| 1 | VIX Override | VIX ≥ 25 |
| 2 | MC Override | VIX < 25 AND (MC < 15 OR MC > 80) |
| 3 | Regular Market | VIX < 25 AND MC 15–80 |

### Step 2: Issue Market Signal
- Use the **Market Signals** table from the active condition (Step 1).
- Displayed once in the top bar alongside QQQ price, MC Score, and VIX.

### Step 3: Issue Stock Signal (per stock row)
1. **Universal Rule first** — if SA < 59 → apply Universal Rule. Done. Skip to next stock.
2. **If SA ≥ 59** — use the **Stock Signals** table from the active condition (Step 1).

---

## Universal Rule (Stock Signal Override)
- **Fields:** SA Score (Module 1 Normalized Score)
- **Applies to:** Every stock row, in ALL conditions, checked before condition-specific stock signals.

| SA Condition | Signal | Current Holdings Actions | Color |
|--------------|--------|--------------------------|-------|
| 35 to 59 | Find Better | Sell if Holding | t-yellow |
| < 35 | Avoid | Sell if holding | t-red |

---

## CONDITION 1: VIX Override
- **Trigger:** VIX Level (FMP `^VIX` Price) ≥ 25
- **Fields:** VIX Level, MC Score (Module 2 Normalized), SA Score (Module 1 Normalized)

### Market Signals

| VIX Condition | MC Condition | Signal | Signal Details | Cash at Hand | Color |
|---------------|--------------|--------|----------------|--------------|-------|
| VIX ≥ 30 | Any | Aggressive Buy | Fear is maximized, great buying opportunity | 5% | a-green |
| VIX 25 to 29 | Any | Confident Buy | Market panic drop, buy including QQQ positions | 20% | t-green |

### Stock Signals

| VIX Condition | MC Condition | SA Condition | Signal | Manage Holdings | Color |
|---------------|--------------|--------------|--------|-----------------|-------|
| VIX ≥ 25 | Any | ≥ 75 | Aggressive Buy | Hold if Own | t-green |
| VIX ≥ 25 | Any | 65 to 74 | Buy | Hold if Own | a-green |
| VIX ≥ 25 | Any | 59 to 64 | Monitor for improvement | Consider Selling. Tight Stop loss | t-yellow |

*Note: SA range 59–64 reflects effective floor after Universal Rule catches SA < 59 first.*

---

## CONDITION 2: Market Score Override
- **Trigger:** VIX Level (FMP `^VIX` Price) < 25 AND MC Score (Module 2 Normalized) < 15 OR > 80
- **Fields:** VIX Level, MC Score (Module 2 Normalized), SA Score (Module 1 Normalized)

### Market Signals

| VIX Condition | MC Condition | Signal | Signal Details | Cash at Hand | Color |
|---------------|--------------|--------|----------------|--------------|-------|
| < 25 | < 15 | Weak Market | No new positions | 90% | t-orange |
| < 25 | > 80 | Overheated | No new positions | 50% | t-yellow |

### Stock Signals

| VIX Condition | MC Condition | SA Condition | Signal | Manage Holdings | Color |
|---------------|--------------|--------------|--------|-----------------|-------|
| < 25 | < 15 | ≥ 69 | No New Buys | Add tight 5% trailing stop | t-orange |
| < 25 | < 15 | 59 to 68 | Sell | Sell | t-red |
| < 25 | > 80 | ≥ 70 | No New Buys | Set 10% trailing stop loss | t-yellow |
| < 25 | > 80 | 59 to 69 | No New Buys | Set 5% trailing stop loss | t-orange |

*Note: SA ranges reflect effective floor after Universal Rule catches SA < 59 first.*

---

## CONDITION 3: Regular Market
- **Trigger:** VIX Level (FMP `^VIX` Price) < 25 AND MC Score (Module 2 Normalized) 15 to 80
- **Fields:** VIX Level, MC Score (Module 2 Normalized), SA Score (Module 1 Normalized)

### Market Signals

| VIX Condition | MC Condition | Signal | Signal Details | Cash at Hand | Color |
|---------------|--------------|--------|----------------|--------------|-------|
| < 25 | 15 to 29 | Growing Market | Add quality stocks | 30% | t-teal |
| < 25 | 30 to 54 | Healthy Market | Good time to buy | 20% | t-green |
| < 25 | 55 to 69 | Selective Buy | Avoid overextended stocks | 30% | t-blue |
| < 25 | 70 to 80 | Careful Buy | Overheated market. Ride momentum carefully | 20% | t-yellow |

### Stock Signals

| VIX Condition | MC Condition | SA Condition | Signal | Manage Holdings | Color |
|---------------|--------------|--------------|--------|-----------------|-------|
| < 25 | 15 to 69 | ≥ 80 | Buy | Hold | t-green |
| < 25 | 15 to 69 | 70 to 79 | Selective Buy | Hold with 10% trailing stop | t-teal |
| < 25 | 15 to 69 | 60 to 69 | Monitor | Hold with 10% trailing stop | t-yellow |
| < 25 | 70 to 80 | ≥ 80 | Buy | Hold with 10% trailing stop | t-green |
| < 25 | 70 to 80 | 70 to 79 | Careful Buy | Hold with 10% trailing stop | t-yellow |
| < 25 | 70 to 80 | 60 to 69 | Monitor | Hold with 5% trailing stop | t-orange |

---

## Part 3B — Signal Overrides

The following overrides apply globally after condition-based signals are assigned. Evaluated in order per stock row.

---

### Override 1: Crypto Complete Filter
- **Applies to:** IREN, MARA, CLSK, RIOT, BITF, WULF, HUT, CIFR, COIN, MSTR, CORZ, BTBT, HIVE, BTDR
- **Trigger:** Any Buy-type signal

| Condition | Signal Override | Color |
|-----------|-----------------|-------|
| Symbol is in crypto list AND signal is Buy-type | No Buy (Crypto) | t-red |
| Otherwise | No change | — |

- Does not affect non-buy signals.

---

### Override 2: Basic Materials Sector Cap (Max 2)
- **Applies to Sectors:** Basic Materials, Mining
- **Trigger:** 3 or more stocks in these sectors qualify for buy signals in the same scan

| Condition | Signal Override | Color |
|-----------|-----------------|-------|
| Top 2 by SA score (tiebreak: higher Net Profit Margin) | No change | — |
| 3rd stock and beyond | No New Buys (Sector Cap) | t-yellow |

- Does not affect non-buy signals or SA scores.

---

### Override 3: Unprofitable Stock Override
- **Trigger:** Net Profit Margin < 0%
- **Applies to signals:** Buy, Selective Buy, Aggressive Buy, Careful Buy

| Condition | Signal Override | Color |
|-----------|-----------------|-------|
| Net Profit Margin < 0% AND signal is Buy-type | Append "(Unprofitable)" to signal label | t-yellow |
| Otherwise | No change | — |

- Does not affect non-buy signals or SA scores.

---

# Part 4 — Tiers (Position Sizing)

Tiers define the max position size per stock.
**Tier Precedence:** If a stock qualifies for multiple tiers, assign the highest tier.
**Note:** Tiers are risk caps, not quality rankings. Score determines quality; tier determines maximum position size based on risk profile.

## Tier Field Definitions

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
| T1 | ≥ 55 | Profitable (Net Profit Margin ≥ 0%) + Market Cap > $50B | $100,000 | t-green |
| T2 | ≥ 50 | Profitable (Net Profit Margin ≥ 0%) + Market Cap > $2B | $50,000 | t-blue |
| T3 | ≥ 50 | Market Cap > $100M + (Growth: Annual Revenue Growth > 0% OR Small Profitable: Net Profit Margin > 0% AND Market Cap ≤ $2B) | $20,000 | t-yellow |
| SELL | Does not qualify for any tier | $0 — Do not buy | t-red |

---

<!--
**Color Token Backup**
These are the colors that are used in the design. They are here just as a backup. No need to incorporate into the code.
oken	Used For
t-green	Buy, Aggressive Buy (stock), Selective Buy (stock), Confident Buy (market), Healthy Market
a-green	Aggressive Buy (market), Buy (VIX stock)
t-teal	Growing Market
t-blue	Selective Buy (market), T2 tier
t-yellow	Find Better, Monitor, Careful Buy, Overheated, No New Buys (MC>80), Unprofitable override, Sector Cap, T3 tier
t-orange	Weak Market, No New Buys (MC<15), Monitor (MC 70-80)
t-red	Avoid, Sell, No Buy (Crypto), SELL tier
Plus from your SA/MC Grade tables:

Token	Used For
a-red	SA Grade "Avoid" (< 40)
a-green	MC Grade "Too Strong" (≥ 70)

---
-->

**End of Signals Instructions**
