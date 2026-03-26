ID Engine Additionas March 2026

---

# AI ASSESSMENT (AA)

I would like to add these questions to the IQ Engine. These are binary questions or can be, but the main difference between these and 
SA questions are that some of the answers need to be pulled by Web Search. So, we need to find the fields, but also define custom fields to pull
data from web search when needed. Then output can be text, or points to be counted in the total IQ sccore. 

We also need to find the best way to convert these qualitative questions/points into binary questions with numbers/points or signal text output. 
---

## Overview

AI Assessments are qualitative research layers that cover things like:

1. Visual health indicator based on fundamental flag analysis
2. **Bulls / Bears** thesis points for each stock



### Calculation

Count positive and negative signals from Fundamental Flags and the Research Checklist below.

Each can be a question with a positive one point
**Positive signals:** Guidance Raised, EPS Revised Up, Analyst Upgrade, Insider Buying, outperforming sector, positive news sentiment, strong moat, upcoming catalyst

Each can be a question with a negative point
**Negative signals:** Guidance Cut, EPS Revised Down, Analyst Downgrade, Insider Selling, Sector Lag, Event Risk, negative news sentiment, valuation concern


Penalty items
Each can be a question with -5 point
- a practical Kill Switch flags for (SEC/Fraud, Critical Volatility) 


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


Text output ideas

Positive thesis points. 3-5 bullets covering:
- Growth drivers and sustainability
- Competitive moat / pricing power
- Tailwinds (secular trends, policy, macro)
- Management execution / capital allocation
- Upcoming positive catalysts


#### Bears 🔴

Risk factors and concerns. 3-5 bullets covering:
- Headwinds (regulatory, competitive, macro)
- Valuation concerns vs peers
- Execution risks
- Negative catalysts or event risk
- Balance sheet / cash burn issues

FDA rejection — binary event risk
Raised guidance + beat — strong signal




#### Bulls 🟢 / Bears 🔴

3-4 bullets each on market-level thesis points:
- Technical position (QQQ trend, RSI, MACD)
- Macro signals (GDP proxy, yield curve, fed policy)
- Breadth (small-cap, equal-weight, transports)
- Risk appetite (VIX, credit, dollar)


---
---

# Part 2 — Alerts (Display Only)

Alerts also can be converted into binary questions. 
They appear in tables, cards, and icons based on instructions.
Source from FMP API when available. Yahoo and Google Finance and web search otherwise.
Search the sources above to find any of the situations below; if found, add the Alert message
from the tables below. Accompany the message with the related color.


## Red Alerts (Negative / Risk) (-3 penalties)
**Color: t-red**

| Alert | Trigger |
|-------|---------|
| SEC Investigation | Active SEC investigation, fraud, restatement |
| Legal Issues | Lawsuit, hearing, investigation, ruling news about the company or top executives |
| Forward Guidance Shows Decline | Forward guidance lowered by the company |
| Downgraded by Analysts | Analyst downgraded the stock within the last 30 days |

## Yellow Alerts (Caution / Neutral) (-2 penalties)
**Color: t-yellow**

| Alert | Trigger |
|-------|---------|
| Earning Date Close | Earnings date is within the next 7 days |
| IPO (New Company) | Company's IPO was listed within the last 7 days |
| Healthcare / Binary Event Risk | Sector is Healthcare, Medical, Pharma, Pharmaceutical, Biotechnology, Medical Devices, Drug Manufacturers, Health Care, Diagnostics & Research, Medical Instruments & Supplies, Pharmaceutical Retailers, or Health Information Services. Rationale: exposed to FDA decisions, clinical trials, patent cliffs. |

## Green Alerts (Positive / Opportunity) +1 Bonus
**Color: t-green**

| Alert | Trigger |
|-------|---------|
| Positive Guidance | Forward guidance is raised |
| Upgrade by Analysts | Analysts upgraded the stock within the last month |

---
