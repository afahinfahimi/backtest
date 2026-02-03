# FLAGS & ALERTS (FLAGS V12)

**Lovable Trade V13 - "Alert Layer" Edition**
**Updated: February 3, 2026**

---

## Overview

Flags are **non-scoring** visual indicators that provide context beyond SA/MC scores. They do not modify scores. They surface on the Analyzer table, stock detail cards, and alert panels.
**Time Period Shorthand:** 5D = 5 trading days, 10D = 10 trading days, 1M = 1 calendar month, 52W = 52 weeks.
**Data Sources:** Flags read from SA fields, MC fields, MS outputs, and external data (news, filings).

---

## 1. KILL SWITCHES (Immediate Action Required)

These override all scores. Action is mandatory.

| Flag | Icon | Trigger | Action |
|------|------|---------|--------|
| SEC/Fraud | 🚨 | Active investigation, fraud allegation, restatement | Do not buy / Exit review |
| Critical Volatility | 🔴 | Thesis-breaking news + 5D ≤ -15% | Exit review required |

---

## 2. RISK FLAGS

Surface risk factors that scores may not fully capture.

| Flag | Icon | Trigger | Color |
|------|------|---------|-------|
| Downtrend | 📉 | 5D < 0% AND 10D < 0% AND 1M < 0% | Red-D |
| Volatility | ⚡ | 5D %Chg ≥ +7% or ≤ -7% | Red-M |
| Mean Reversion | 🪃 | SA Q7 (%B) = Breakout AND MC < 60 | Red-M |
| Short Squeeze Risk | 🩳 | Short % of float > 20% + increasing | Red-M |
| Low Float | 🎯 | Float < 20M shares | Orange-M |
| Earnings Soon | ⚠️ | Earnings within 14 days | Yellow-M |

---

## 3. SECTOR FLAGS

Identify sector-specific risk profiles.

| Flag | Icon | Trigger | Color |
|------|------|---------|-------|
| Crypto | ₿ | Crypto-related business | Orange-M |
| Commodity | ⛏️ | Mining/resources sector | Yellow-D |
| Energy | 🛢️ | Oil/gas sector | Brown-M |
| Sector Cap | 🚫 | Max 2 positions per restricted sector reached | Purple-D |

**Restricted Sectors:** Pharma, Medical, Crypto, Mining, Oil/Gas, Commodities

**Rule:** Maximum 2 positions per restricted sector regardless of score.

---

## 4. OPPORTUNITY FLAGS

Highlight potential entries or special situations.

| Flag | Icon | Trigger | Color |
|------|------|---------|-------|
| Bounce Play | 🪃 | SA < 35 AND 1M < -15% | Blue-D |
| Momentum Spec | 🚀 | SA < 35 AND 1M > +15% | Green-D |
| Turtle | 🐢 | 52W ±10% AND 1M ±10% | Teal-M |
| Lottery | 🎰 | SA < 35 AND Market Cap < $500M | Olive-D |
| IPO | 🆕 | Listed less than 12 months | Blue-M |

---

## 5. FUNDAMENTAL FLAGS

Derived from earnings, analyst, and corporate data. These replaced the former AA (AI Assessment) scoring questions.

| Flag | Icon | Trigger | Source | Color |
|------|------|---------|--------|-------|
| Guidance Raised | 📈📢 | Company raised forward guidance | Earnings calls, press releases | Green-M |
| Guidance Cut | 📉📢 | Company lowered forward guidance | Earnings calls, press releases | Red-L |
| EPS Revised Up | 📈💵 | Consensus EPS estimates raised > 5% (90 days) | FMP analyst estimates | Green-M |
| EPS Revised Down | 📉💵 | Consensus EPS estimates cut > 5% (90 days) | FMP analyst estimates | Pink-M |
| Analyst Upgrade | ⬆️ | Net upgrades last 30 days | FMP upgrades/downgrades | Green-M |
| Analyst Downgrade | ⬇️ | Net downgrades last 30 days | FMP upgrades/downgrades | Red-M |
| Insider Buying | 🟢👤 | Net insider buying last 6 months | FMP insider trading | Green-M |
| Insider Selling | 🔴👤 | Net insider selling last 6 months | FMP insider trading | Red-M |
| Event Risk | ⚠️📰 | Negative surprise (miss, investigation, guidance withdrawn) | News, SEC filings | Brown-M |
| Sector Lag | 📊⬇️ | Underperforming sector ETF by > 5% (1M) | Compare 1M vs sector ETF | Navy-M |

---

## 6. VOLATILITY ALERT PROTOCOL


**Trigger:** 5D %Chg ≥ +7% or ≤ -7%
When triggered, research and classify:

### Catalyst Types
- Company KPI
- Earnings
- Analyst
- Regulatory
- Macro
- Technical

### Severity Levels

| Level | Icon | Criteria | Action |
|-------|------|----------|--------|
| Critical | 🔴 | Thesis broken, fraud, major miss | Exit review required |
| High | 🟠 | Material near-term impact | Suspend adds, trim review |
| Medium | 🟡 | Temporary sentiment shift | Monitor only |
| Low | 🟢 | Noise, overreaction | Potential add opportunity |

### Rules
- Non-scoring — flag only
- Position flagged until manually cleared
- Auto-expires after 5 trading days
- Positive alerts (🟢) may signal add opportunity if under-allocated

---


## 7. FLAG DISPLAY

### Analyzer Table
Flags display as icons in the ALERTS column, ordered: Kill Switch → Risk → Sector → Fundamental → Opportunity

### Example

| Symbol | Score | Alerts | Tier |
|--------|-------|--------|------|
| NVDA | 74 | ⚠️ | T1 |
| SMCI | 55 | 🚨 ⚡ | T2 |
| MARA | 48 | ₿ 🩳 | T3 |
| MU | 81 | 📈📢 ⬆️ | T1 |

---

**End of Flags V12**

