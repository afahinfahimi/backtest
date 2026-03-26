ID Engine Additionas March 2026

---

# AI ASSESSMENT (AA V12)

**Lovable Trade V12 - "Research Layer" Edition**
**Updated: February 2, 2026**

---

## Overview

AI Assessment is the qualitative research layer. It does **not** produce a score. It generates:

1. An **AI Dot** (visual health indicator) based on fundamental flag analysis
2. **Bulls / Bears** thesis points for each stock
3. **Buy Ideas / If Owned** recommendations (account-aware)
4. **MC Commentary** for the market condition expansion card

**Principle:** SA/MC scores are objective and data-driven. AA provides subjective, research-based context that scores cannot capture.

---

## 1. AI DOT (Visual Health Indicator)

The AI Dot displays in the Analyzer table's AI column. It summarizes the net direction of fundamental flags and research findings.

### Calculation

Count positive and negative signals from Fundamental Flags (FLAGS V12 Section 5) and the Research Checklist below.

**Positive signals:** Guidance Raised, EPS Revised Up, Analyst Upgrade, Insider Buying, outperforming sector, positive news sentiment, strong moat, upcoming catalyst

**Negative signals:** Guidance Cut, EPS Revised Down, Analyst Downgrade, Insider Selling, Sector Lag, Event Risk, negative news sentiment, valuation concern

### Dot Assignment

| Dot | Color | Condition |
|-----|-------|-----------|
| 🟢 | Green-M | Net positive: positives exceed negatives by 2+ |
| 🟡 | Yellow-M | Mixed: difference between positives and negatives ≤ 1 |
| 🔴 | Red-M | Net negative: negatives exceed positives by 2+ |
| ⚫ | Gray-D | No data: research not yet run |

### Rules
- Dot updates when AI research is triggered (manual or on-analyze)
- Kill Switch flags (SEC/Fraud, Critical Volatility) force 🔴 regardless of count
- Dot is non-scoring — display only

---

## 2. RESEARCH CHECKLIST

AI must check all items before generating Bulls/Bears content. Use web search, FMP API, and news sources.

### Required Checks

| # | Check | Source | Flag Trigger |
|---|-------|--------|-------------|
| 1 | Guidance trend (raised/lowered) | Earnings calls, press releases | Guidance Raised / Cut |
| 2 | EPS revision trend (up/down, 90 days) | FMP analyst estimates | EPS Revised Up / Down |
| 3 | Analyst rating changes (30 days) | FMP upgrades/downgrades | Upgrade / Downgrade |
| 4 | Insider activity (6 months) | FMP insider trading | Insider Buying / Selling |
| 5 | Relative strength vs sector (1M) | Compare 1M vs sector ETF | Sector Lag |
| 6 | Recent events/news (7 days) | Web search | Event Risk |
| 7 | Short interest level & trend | FMP, Barchart | Short Squeeze Risk flag |
| 8 | Competitive moat assessment | Web search, analyst reports | — (Bulls/Bears content) |
| 9 | Valuation vs peers | FMP stock peers, P/E, P/S, EV/EBITDA | — (Bulls/Bears content) |
| 10 | Upcoming catalysts (30 days) | Earnings calendar, news | — (Bulls/Bears content) |

### Research Priority
- Items 1-7 trigger Fundamental Flags (FLAGS V12) and feed AI Dot calculation
- Items 8-10 are content-only — they inform Bulls/Bears but don't trigger flags

---

## 3. OUTPUT SECTIONS

### 3A. Stock Expansion Card

Displays when a stock row is expanded in the Analyzer.

#### Bulls 🟢

Positive thesis points. 3-5 bullets covering:
- Growth drivers and sustainability
- Competitive moat / pricing power
- Tailwinds (secular trends, policy, macro)
- Management execution / capital allocation
- Upcoming positive catalysts

**Format:** `• [Point] — [brief explanation]`

#### Bears 🔴

Risk factors and concerns. 3-5 bullets covering:
- Headwinds (regulatory, competitive, macro)
- Valuation concerns vs peers
- Execution risks
- Negative catalysts or event risk
- Balance sheet / cash burn issues

**Format:** `• [Point] — [brief explanation]`

Use ⚠️ prefix for significant items:
- `⚠️ FDA rejection — binary event risk`
- `⚠️ Raised guidance + beat — strong signal`

#### Buy Ideas

Entry strategies with specific numbers. Account-aware.

**Content:**
1. Primary entry (market or limit with price)
2. Secondary entry (pullback level with price)
3. Position size based on tier

**Account Logic:**
- **Investment:** Conservative. Emphasize limit orders, dollar-cost averaging
- **Active:** Standard. Market orders acceptable, use ATR for sizing
- **IRA:** Tax-aware. Avoid frequent trading, prefer larger positions held longer

**Shares vs Options toggle:** Generate share-based or options-based ideas depending on user selection.

#### If Owned

Recommendations for existing positions.

**Content:**
1. Hold/add/trim guidance based on current SA score
2. Stop loss recommendation (price level)
3. Profit-taking level if applicable

**Must reference:**
- Current SA score trend (improving/declining)
- Current gain/loss from entry (if known)
- Tier-appropriate profit targets (+25% T1 / +20% T2 / +30% T3)

---

### 3B. MC Expansion Card

Displays when the Market Conditions bar is expanded.

#### MC Summary

One-line market assessment:
- `"Market is [condition]. [Action recommendation]."`

#### Bulls 🟢 / Bears 🔴

3-4 bullets each on market-level thesis points:
- Technical position (QQQ trend, RSI, MACD)
- Macro signals (GDP proxy, yield curve, fed policy)
- Breadth (small-cap, equal-weight, transports)
- Risk appetite (VIX, credit, dollar)

#### Buy Ideas (QQQ-specific)

When MC signals opportunity:
- QQQ entry strategy
- Leveraged alternatives (TQQQ) with caveats
- Position size

#### If Owned (QQQ-specific)

When QQQ position is held:
- Hold/trim/exit guidance
- VIX-based exit triggers
- Profit-taking levels

#### Upcoming Events

List high-impact events within 7 days:
- Fed meetings / FOMC
- Jobs report (NFP)
- CPI / PPI
- Earnings season dates
- Geopolitical events

**Format:** `📅 [Event] ([Date]) — [Impact level: High/Medium/Low]`

---

## 4. GENERATION RULES

### Timing
- AI content generates when the Analyze button is clicked
- AI Dot can be refreshed independently (AI 🔄 button in table header)
- Content is date-stamped and cached until next analysis

### Quality Standards
- Be decisive — give clear verdicts, not hedged non-answers
- Use specific numbers (prices, percentages, dates)
- Reference SA score and tier in Buy Ideas
- Reference MC score and zone in market commentary
- Acknowledge uncertainty when data is stale or missing
- Never fabricate data — if a check returns nothing, state "No recent data"

### What AI Must NOT Do
- Override SA/MC scores
- Contradict MS Zone Table signals (e.g., don't say "buy" when MC 60+ = no new buys)
- Generate recommendations for AVOID/Veto stocks without clearly stating the veto
- Provide specific options strike/expiry without user requesting options mode

---

**End of AI Assessment V12**

---
---
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
