# Module-4 — Signals
**Lovable Trade V18 — Updated 2/25/2026**

This module consolidates all color coding, grading, alerts, and action signals in one place.
Modules 1 (Analysis) and 2 (Market) focus solely on calculating scores. This module interprets them.

---

## Required Input Data

| Field | Source | Description |
|-------|--------|-------------|
| **SA Score** | Module 1 (Analysis) — Normalized Score | `((Raw Score + 50) / 123) * 100`. Range: 0–100 |
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
High VIX = elevated fear = historically a buying opportunity. Colors reflect opportunity level, not danger level.

| VIX Level | Grade | Color |
|-----------|-------|-------|
| > 30 | Extreme Fear — Strong Buy Opportunity | t-green |
| 25–29 | High Fear — Buy Opportunity | t-teal |
| 20–24 | Elevated | t-blue |
| 15–20 | Normal | t-blue |
| < 15 | Complacent | t-orange |

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
| Healthcare / Binary Event Risk | Sector is Healthcare, Medical, Pharma, Pharmaceutical, Biotechnology, Medical Devices, Drug Manufacturers, Health Care, Diagnostics & Research, Medical Instruments & Supplies, Pharm
