# V19 Hybrid — Stock Analysis Scoring System
## Max Raw Score: 95 | Reserve: 5 pts for future (→ 100)
## No normalization. Raw Score = Final Score.

### Changes from V17:
- Q1 (Sales Growth): doubled then scaled → max 14
- Q3 (Cash Flow Growth): doubled then scaled → max 14
- Q31 (Trend Deterioration): penalty increased → -12
- All questions proportionally scaled (×1.16) to reach max 95
- Q11, Q18, Q30 received +1 bonus point (rounded up)

---

## Q1 — Sales Growth
- **Question Name:** Sales Growth
- **Field Expression:** revenueGrowth
- **Description:** Revenue growth %. Full SA logic uses both annual & quarterly acceleration. DOUBLE WEIGHTED.
- **Max Points:** 14 | **Min Points:** 0

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | >= | 50 | 14 | Exceptional |
| B | >= | 20 | 9 | Strong |
| C | >= | 1 | 5 | Growing |
| D | >= | 0 | 2 | Stalling |
| E | else | — | 0 | Declining |

---

## Q2 — Operating Income Growth
- **Question Name:** Op Income Growth
- **Field Expression:** operatingIncomeGrowth
- **Description:** Operating income growth %. Full SA logic uses both annual & quarterly.
- **Max Points:** 7 | **Min Points:** 0

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | >= | 50 | 7 | Exceptional |
| B | >= | 20 | 5 | Strong |
| C | >= | 1 | 2 | Growing |
| D | >= | 0 | 1 | Stalling |
| E | else | — | 0 | Declining |

---

## Q3 — Cash Flow Growth
- **Question Name:** Cash Flow Growth
- **Field Expression:** operatingCashFlowGrowth
- **Description:** Operating cash flow growth %. Full SA logic uses both annual & quarterly. DOUBLE WEIGHTED.
- **Max Points:** 14 | **Min Points:** 0

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | >= | 50 | 14 | Exceptional |
| B | >= | 20 | 9 | Strong |
| C | >= | 1 | 5 | Growing |
| D | >= | 0 | 2 | Stalling |
| E | else | — | 0 | Declining |

---

## Q4 — Net Profit Margin
- **Question Name:** Net Profit Margin
- **Field Expression:** netProfitMargin
- **Description:** Net Income / Revenue (TTM).
- **Max Points:** 6 | **Min Points:** 0

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | >= | 30 | 6 | Exceptional |
| B | >= | 20 | 5 | Strong |
| C | >= | 15 | 3 | Good |
| D | >= | 10 | 2 | Moderate |
| E | >= | 5 | 1 | Low |
| F | else | — | 0 | None |

---

## Q5 — 1-Month Price Change
- **Question Name:** 1-Month Price Change
- **Field Expression:** priceChange1M
- **Description:** 1-month price change %.
- **Max Points:** 5 | **Min Points:** 0

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | >= | 20 | 5 | Explosive |
| B | >= | 10 | 3 | Strong |
| C | >= | 5 | 2 | Moderate |
| D | > | 0 | 1 | Positive |
| E | else | — | 0 | Flat/Down |

---

## Q6 — 10-Day Price Change
- **Question Name:** 10-Day Price Change
- **Field Expression:** priceChange10D
- **Description:** 10-day price change %.
- **Max Points:** 3 | **Min Points:** 0

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | >= | 15 | 3 | Strong |
| B | >= | 10 | 2 | Moderate |
| C | >= | 5 | 1 | Mild |
| D | else | — | 0 | Weak |

---

## Q7 — Average Volume
- **Question Name:** 20-Day Average Volume
- **Field Expression:** avgVolume20D
- **Description:** 20-day average trading volume.
- **Max Points:** 3 | **Min Points:** 0

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | >= | 1000000 | 3 | High Liquidity |
| B | >= | 500000 | 2 | Moderate |
| C | >= | 200000 | 1 | Low |
| D | else | — | 0 | Illiquid |

---

## Q8 — Ownership & Coverage
- **Question Name:** Ownership & Coverage
- **Field Expression:** institutionalOwnership, analystCount
- **Description:** Conditional: +1 if Inst Ownership > 0%, +1 if Analyst Ratings > 0.
- **Max Points:** 2 | **Min Points:** 0

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | Inst Own > | 0 | +1 | Institutional |
| B | Analysts > | 0 | +1 | Covered |
| — | else | — | 0 | No Coverage |

---

## Q9 — Price vs Moving Averages
- **Question Name:** Price vs Moving Averages
- **Field Expression:** priceVsMA
- **Description:** Current Price vs 20-Day SMA and 50-Day SMA.
- **Max Points:** 5 | **Min Points:** 0

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | above | both 20D & 50D | 5 | Full Alignment |
| B | above | 50D only | 4 | Above Trend |
| C | above | 20D only | 2 | Short-term Only |
| D | else | — | 0 | Below Both |

---

## Q10 — Debt-to-Equity Ratio
- **Question Name:** Debt-to-Equity
- **Field Expression:** debtToEquity
- **Description:** Total Debt / Total Equity. Evaluate in order, stop at first match.
- **Max Points:** 3 | **Min Points:** -3

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | == | negative equity | -3 | Danger |
| B | < | 0.5 | 3 | Excellent |
| C | < | 1.0 | 2 | Good |
| D | < | 2.0 | 1 | Acceptable |
| E | else | — | 0 | High Debt |

---

## Q11 — Momentum Magnitude
- **Question Name:** Momentum Magnitude
- **Field Expression:** momentumMagnitude
- **Description:** 52-Week %Chg + 3-Month %Chg. Bumped +1 from scaling.
- **Max Points:** 4 | **Min Points:** 0

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | > | 150 | 4 | Extreme |
| B | > | 100 | 2 | Strong |
| C | > | 50 | 1 | Moderate |
| D | else | — | 0 | Weak |

---

## Q12 — EPS Growth
- **Question Name:** EPS Growth (Prior Year)
- **Field Expression:** epsGrowth
- **Description:** EPS Growth % (Prior Fiscal Year).
- **Max Points:** 5 | **Min Points:** 0

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | >= | 100 | 5 | Exceptional |
| B | >= | 50 | 4 | Strong |
| C | >= | 25 | 2 | Good |
| D | > | 0 | 1 | Positive |
| E | else | — | 0 | Negative |

---

## Q13 — Return on Equity
- **Question Name:** Return on Equity
- **Field Expression:** roe
- **Description:** Return on Equity (TTM).
- **Max Points:** 2 | **Min Points:** 0

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | >= | 20 | 2 | Strong |
| B | >= | 10 | 1 | Moderate |
| C | else | — | 0 | Weak |

---

## Q14 — Return on Assets
- **Question Name:** Return on Assets
- **Field Expression:** roa
- **Description:** Return on Assets (TTM).
- **Max Points:** 3 | **Min Points:** 0

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | >= | 15 | 3 | Excellent |
| B | >= | 10 | 2 | Good |
| C | >= | 5 | 1 | Moderate |
| D | else | — | 0 | Low |

---

## Q15 — Country
- **Question Name:** Country
- **Field Expression:** country
- **Description:** Company domicile.
- **Max Points:** 1 | **Min Points:** -2

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | == | US | 1 | USA |
| B | in | CA,UK,NL,DE,FR,JP,AU,TW,KR,CH,IE,IL | 0 | Developed |
| C | else | — | -2 | China/EM |

---

## Q16 — Cash Burn Risk
- **Question Name:** Cash Burn Risk
- **Field Expression:** cashBurnRisk
- **Description:** Unprofitable + negative CF + small cap. Combined cap with Q17: max -5.
- **Max Points:** 0 | **Min Points:** -3

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | NPM >= | 0 | 0 | Profitable |
| B | OpCF >= | 0 | 0 | CF Positive |
| C | MCap >= | 10000000000 | 0 | Large Cap Shield |
| D | else | — | -3 | Cash Burn |

---

## Q17 — Deterioration Risk
- **Question Name:** Deterioration Risk
- **Field Expression:** deteriorationRisk
- **Description:** Revenue, OpInc, CF all declining QoQ. Combined cap with Q16: max -5.
- **Max Points:** 0 | **Min Points:** -3

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | trigger | Rev<q-4 AND OpInc<q-4 AND CF<q-4 | -3 | Triple Decline |
| B | else | — | 0 | OK |

---

## Q18 — Financial Strength
- **Question Name:** Financial Strength
- **Field Expression:** financialStrength
- **Description:** Composite: NPM + ROE + D/E. Bumped +1 from scaling.
- **Max Points:** 4 | **Min Points:** 0

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | meets | NPM>=20 AND ROE>=20 AND D/E<0.5 | 4 | Fortress |
| B | meets | NPM>=10 AND ROE>=10 AND D/E<1.5 | 2 | Solid |
| C | meets | NPM>=0 AND ROE>=5 AND D/E<3.0 | 1 | Adequate |
| D | else | — | 0 | Weak |

---

## Q19 — Momentum Divergence
- **Question Name:** Momentum Divergence
- **Field Expression:** momentumDivergence
- **Description:** 52W>0 but 3M, 1M, 10D all negative.
- **Max Points:** 0 | **Min Points:** -3

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | trigger | 52W>0 AND 3M<0 AND 1M<0 AND 10D<0 | -3 | Fading |
| B | else | — | 0 | OK |

---

## Q20 — Sector Preference
- **Question Name:** Sector Preference
- **Field Expression:** sector
- **Description:** Sector tilt. See notes for Crypto/Mining classifications.
- **Max Points:** 2 | **Min Points:** -5

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | in | Tech, Finance, Business Svc, Aerospace, Defence | 2 | Favored |
| B | in | Consumer, Auto, Retail, Industrial, Transport, Utilities, Construction | 1 | Neutral+ |
| C | in | Energy, Basic Materials | 0 | Neutral |
| D | in | Crypto, Mining, Pharma, Biotech, Medical | -5 | Penalized |

---

## Q21 — Bollinger %B Position
- **Question Name:** %B Position
- **Field Expression:** bollingerPercentB
- **Description:** Bollinger Bands %B (20, 2). Also lifts Cyclical Sector Cap on Q1-Q3.
- **Max Points:** 5 | **Min Points:** 0

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | > | 100 | 5 | Breakout |
| B | > | 95 | 4 | Near Top |
| C | >= | 80 | 2 | Upper Zone |
| D | >= | 20 | 1 | Mid-Range |
| E | else | — | 0 | Buy Zone |

---

## Q22 — Momentum Quality
- **Question Name:** Momentum Quality
- **Field Expression:** momentumQuality
- **Description:** Pattern check. Evaluate in order, stop at first match.
- **Max Points:** 2 | **Min Points:** -1

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | trigger | 10D>20% AND 1M<10% | -1 | Spike Risk |
| B | trigger | 52W>3M>1M>10D all positive | 2 | Smooth |
| C | trigger | 3M>0 AND (3M×4)>52W | 1 | Accelerating |
| D | else | — | 0 | Other |

---

## Q23 — High P/E Momentum Trap
- **Question Name:** High P/E Trap
- **Field Expression:** peTrap
- **Description:** Overvalued + declining price.
- **Max Points:** 0 | **Min Points:** -5

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | trigger | P/E>50 AND 10D<-5% | -5 | Trap |
| B | else | — | 0 | OK |

---

## Q24 — Biotech Binary Event
- **Question Name:** Biotech Binary
- **Field Expression:** biotechBinary
- **Description:** Medical/Pharma with sudden spike.
- **Max Points:** 0 | **Min Points:** -3

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | trigger | Sector=Medical/Pharma AND 10D>15% | -3 | Binary Risk |
| B | else | — | 0 | OK |

---

## Q25 — Sustained Downtrend
- **Question Name:** Sustained Downtrend
- **Field Expression:** sustainedDowntrend
- **Description:** All timeframes negative.
- **Max Points:** 0 | **Min Points:** -3

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | trigger | 1D<0 AND 5D<0 AND 1M<0 | -3 | Downtrend |
| B | else | — | 0 | OK |

---

## Q26 — Sudden Drop / Slide
- **Question Name:** Sudden Drop
- **Field Expression:** maxDailyDrop
- **Description:** Worst single-day drop in last 3 days or 5D cumulative. Highest tier only.
- **Max Points:** 0 | **Min Points:** -7

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | any 1D drop >= | 15% | -7 | Critical |
| B | any 1D drop >= | 10% | -2 | Severe |
| C | any 1D drop >= 7% OR 5D <= | -10% | -1 | Caution |
| D | else | — | 0 | OK |

---

## Q27 — Short Interest Risk
- **Question Name:** Short Interest
- **Field Expression:** shortPercentFloat
- **Description:** Short % of float.
- **Max Points:** 0 | **Min Points:** -1

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | > | 20 | -1 | High Short |
| B | else | — | 0 | OK |

---

## Q28 — Low Float Risk
- **Question Name:** Low Float Risk
- **Field Expression:** floatShares
- **Description:** Float shares count.
- **Max Points:** 0 | **Min Points:** -1

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | < | 20000000 | -1 | Low Float |
| B | else | — | 0 | OK |

---

## Q29 — Sector vs Peers
- **Question Name:** Sector vs Peers
- **Field Expression:** sectorRelativePerf
- **Description:** Stock 1M return vs sector average 1M return.
- **Max Points:** 1 | **Min Points:** -1

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | outperforms by > | 10% | 1 | Leader |
| B | within | ±10% | 0 | In-Line |
| C | underperforms by > | 10% | -1 | Laggard |

---

## Q30 — 5-Day Relative Strength
- **Question Name:** 5-Day Relative Strength
- **Field Expression:** fiveDayAlpha
- **Description:** Stock 5D % minus QQQ 5D %. Evaluate in order. Bumped +1 from scaling.
- **Max Points:** 4 | **Min Points:** -3

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | trigger | Stock UP & Market DOWN | 4 | True Alpha |
| B | alpha >= | 5 | 2 | Beating Market |
| C | alpha >= | 0 | 1 | Keeping Pace |
| D | alpha >= | -5 | 0 | Slight Lag |
| E | alpha < | -5 | -2 | Badly Lagging |
| F | trigger | Stock DOWN & Market UP | -3 | Stock Problem |

---

## Q31 — Trend Deterioration
- **Question Name:** Trend Deterioration
- **Field Expression:** lowerHighsLowerLows
- **Description:** Lower highs AND lower lows (30 days). PENALTY 4x from V17. Primary risk filter.
- **Max Points:** 0 | **Min Points:** -12

| Cond | Operator | Threshold | Pts | Label |
|------|----------|-----------|-----|-------|
| A | trigger | LH + LL (2+ swing points each) | -12 | Structural Downtrend |
| B | else | — | 0 | OK |

---

## Cyclical Sector Cap (Rule)
**Applies to:** Basic Materials, Energy, Mining
**Rule:** Q1, Q2, Q3 capped at 5 pts each.
**Exception:** Q21 = Breakout (5 pts) lifts cap.

---

## Action Signals

| Score | Signal |
|-------|--------|
| 80 – 95 | Strong Buy |
| 68 – 79 | Buy / Add Position |
| 55 – 67 | Hold / Watch |
| Below 55 | Avoid / Sell |

---

## Quick Reference: Max Points

| Q | Name | Max | Min |
|---|------|-----|-----|
| 1 | Sales Growth | **14** | 0 |
| 2 | OpInc Growth | 7 | 0 |
| 3 | Cash Flow Growth | **14** | 0 |
| 4 | Net Profit Margin | 6 | 0 |
| 5 | 1M Price Change | 5 | 0 |
| 6 | 10D Price Change | 3 | 0 |
| 7 | Volume | 3 | 0 |
| 8 | Ownership | 2 | 0 |
| 9 | Price vs MAs | 5 | 0 |
| 10 | Debt/Equity | 3 | -3 |
| 11 | Momentum Mag | **4** | 0 |
| 12 | EPS Growth | 5 | 0 |
| 13 | ROE | 2 | 0 |
| 14 | ROA | 3 | 0 |
| 15 | Country | 1 | -2 |
| 16 | Cash Burn | 0 | -3 |
| 17 | Deterioration | 0 | -3 |
| 18 | Financial Strength | **4** | 0 |
| 19 | Mom Divergence | 0 | -3 |
| 20 | Sector Pref | 2 | -5 |
| 21 | %B Position | 5 | 0 |
| 22 | Mom Quality | 2 | -1 |
| 23 | P/E Trap | 0 | -5 |
| 24 | Biotech Binary | 0 | -3 |
| 25 | Downtrend | 0 | -3 |
| 26 | Sudden Drop | 0 | -7 |
| 27 | Short Interest | 0 | -1 |
| 28 | Low Float | 0 | -1 |
| 29 | Sector vs Peers | 1 | -1 |
| 30 | 5D Rel Strength | **4** | -3 |
| 31 | Trend Deterioration | 0 | **-12** |
| | **TOTAL** | **95** | **-55** |
