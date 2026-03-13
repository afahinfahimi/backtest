# Binary SA — Approved Questions

---

## C1: Growth

### Sales Growth
*Rewards annual and quarterly revenue growth at increasing magnitudes; acceleration bonus if quarterly exceeds annual.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C1-01 | annualRevenueGrowth | > 0% | +1 |
| C1-02 | annualRevenueGrowth | > 20% | +1 |
| C1-03 | annualRevenueGrowth | > 50% | +1 |
| C1-04 | annualRevenueGrowth | > 100% | +1 |
| C1-05 | quarterlyRevenueGrowth | > 0% | +1 |
| C1-06 | quarterlyRevenueGrowth | > 20% | +1 |
| C1-07 | quarterlyRevenueGrowth | > 50% | +1 |
| C1-08 | quarterlyRevenueGrowth | > annualRevenueGrowth | +1 |

### Operating Income Growth
*Same structure as Sales Growth — rewards annual and quarterly improvement with an acceleration bonus.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C1-09 | annualOperatingIncomeGrowth | > 0% | +1 |
| C1-10 | annualOperatingIncomeGrowth | > 20% | +1 |
| C1-11 | annualOperatingIncomeGrowth | > 50% | +1 |
| C1-12 | annualOperatingIncomeGrowth | > 100% | +1 |
| C1-13 | quarterlyOperatingIncomeGrowth | > 0% | +1 |
| C1-14 | quarterlyOperatingIncomeGrowth | > 20% | +1 |
| C1-15 | quarterlyOperatingIncomeGrowth | > 50% | +1 |
| C1-16 | quarterlyOperatingIncomeGrowth | > annualOperatingIncomeGrowth | +1 |

### Cash Flow Growth
*Same structure as Sales Growth — rewards cash flow momentum at both annual and quarterly levels.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C1-17 | annualCashFlowGrowth | > 0% | +1 |
| C1-18 | annualCashFlowGrowth | > 20% | +1 |
| C1-19 | annualCashFlowGrowth | > 50% | +1 |
| C1-20 | annualCashFlowGrowth | > 100% | +1 |
| C1-21 | quarterlyCashFlowGrowth | > 0% | +1 |
| C1-22 | quarterlyCashFlowGrowth | > 20% | +1 |
| C1-23 | quarterlyCashFlowGrowth | > 50% | +1 |
| C1-24 | quarterlyCashFlowGrowth | > annualCashFlowGrowth | +1 |

### EPS Growth Prior Year
*Rewards earnings-per-share growth vs. prior fiscal year at four magnitude tiers.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C1-25 | epsGrowthPriorYear | > 0% | +1 |
| C1-26 | epsGrowthPriorYear | > 25% | +1 |
| C1-27 | epsGrowthPriorYear | > 50% | +1 |
| C1-28 | epsGrowthPriorYear | > 100% | +1 |

### Profitability & Growth Check
*Penalizes stocks that are both unprofitable and growing slowly — the worst risk/reward combination.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C1-29 | netProfitMargin < 0% AND annualRevenueGrowth < 25% | unprofitable and slow | −2 |

### Growth Consistency
*Rewards sustained revenue acceleration; penalizes sequential deceleration across quarters.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C1-30 | revenueAcceleration | each quarter > previous | +1 |
| C1-31 | revenueAcceleration | each quarter < previous (decelerating) | −1 |

### Growth + Profitability Combo
*Awards a bonus point when both revenue growth and operating margin exceed 10% simultaneously.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C1-32 | annualRevenueGrowth + operatingMarginPct | ≥ 10% AND ≥ 10% | +1 |

### Net Income Growth
*Rewards annual and quarterly net income growth; acceleration bonus if quarterly exceeds annual.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C1-33 | annualNetIncomeGrowth | > 0% | +1 |
| C1-34 | annualNetIncomeGrowth | > 20% | +1 |
| C1-35 | annualNetIncomeGrowth | > 50% | +1 |
| C1-36 | quarterlyNetIncomeGrowth | > 0% | +1 |
| C1-37 | quarterlyNetIncomeGrowth | > annualNetIncomeGrowth | +1 |

### EPS Growth — Multi-Timeframe
*Covers EPS growth across TTM, QoQ, and YoY quarterly comparisons.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C1-38 | epsGrowthTTM | > 0% | +1 |
| C1-39 | epsGrowthTTM | > 25% | +1 |
| C1-40 | epsGrowthTTM | > 50% | +1 |
| C1-41 | epsGrowthTTM | > 100% | +1 |
| C1-42 | epsGrowthQoQ | > 0% | +1 |
| C1-43 | epsYoY (epsQ0 vs epsQ3) | > 0% | +1 |
| C1-44 | epsYoY (epsQ0 vs epsQ3) | > 25% | +1 |
| C1-45 | epsYoY (epsQ0 vs epsQ3) | > 50% | +1 |
| C1-46 | epsYoY (epsQ0 vs epsQ3) | > 100% | +1 |

---

## C2: Profitability

### Net Profit Margin
*Rewards increasing profitability at the bottom line across four magnitude tiers.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C2-01 | netProfitMargin | > 0% | +1 |
| C2-02 | netProfitMargin | > 10% | +1 |
| C2-03 | netProfitMargin | > 20% | +1 |
| C2-04 | netProfitMargin | > 30% | +1 |

### Return on Assets
*Rewards the company's efficiency in generating profit from its asset base.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C2-05 | roa | > 5% | +1 |
| C2-06 | roa | > 10% | +1 |
| C2-07 | roa | > 15% | +1 |

### Financial Strength
*Stacked composite check — rewards companies meeting combined margin, ROE, and leverage thresholds.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C2-08 | netProfitMargin ≥ 0 AND roe ≥ 5 AND debtToEquity < 3 | = true | +1 |
| C2-09 | netProfitMargin ≥ 10 AND roe ≥ 10 AND debtToEquity < 1.5 | = true | +1 |
| C2-10 | netProfitMargin ≥ 20 AND roe ≥ 20 AND debtToEquity < 0.5 | = true | +1 |

### FCF Margin TTM
*Rewards companies converting a high percentage of revenue to free cash flow; penalizes negative FCF margin.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C2-11 | fcfMarginTTM | > 0% | +1 |
| C2-12 | fcfMarginTTM | > 10% | +1 |
| C2-13 | fcfMarginTTM | > 15% | +1 |
| C2-14 | fcfMarginTTM | > 20% | +1 |
| C2-15 | fcfMarginTTM | < 0% | −1 |

### Operating Margin TTM
*Rewards operational efficiency at four profitability threshold tiers.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C2-16 | operatingMarginPct | > 5% | +1 |
| C2-17 | operatingMarginPct | > 10% | +1 |
| C2-18 | operatingMarginPct | > 15% | +1 |
| C2-19 | operatingMarginPct | > 25% | +1 |

### Gross Margin QoQ Improvement
*Awards a point when this quarter's gross margin exceeds last quarter's.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C2-20 | grossMarginQ0 | > grossMarginQ1 | +1 |

### ROE — Full 4 Tiers
*Rewards return on equity at four progressively higher magnitude thresholds.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C2-21 | roe | > 5% | +1 |
| C2-22 | roe | > 10% | +1 |
| C2-23 | roe | > 15% | +1 |
| C2-24 | roe | > 25% | +1 |

### ROIC TTM
*Rewards return on invested capital — how efficiently the company deploys its capital.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C2-25 | roicTTM | > 4% | +1 |
| C2-26 | roicTTM | > 8% | +1 |
| C2-27 | roicTTM | > 14% | +1 |
| C2-28 | roicTTM | > 20% | +1 |

### Gross Margin %
*Rewards high gross margins as a signal of pricing power and competitive moat.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C2-29 | grossMarginPct | > 40% | +1 |
| C2-30 | grossMarginPct | > 60% | +1 |

### Operating Margin QoQ Improvement
*Awards a point when this quarter's operating margin exceeds last quarter's.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C2-31 | operatingMarginQ0 | > operatingMarginQ1 | +1 |

### Capex Ratio
*Awards a point when the company generates positive FCF and capex is less than half of it.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C2-32 | FCF > 0 AND capex | < 50% of FCF | +1 |

### Revenue Per Employee
*Rewards high productivity per employee as a proxy for operational leverage.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C2-33 | revenuePerEmployee | > $500K | +1 |
| C2-34 | revenuePerEmployee | > $1M | +1 |

---

## C3: Balance Sheet & Financial Health

### Debt-to-Equity
*Rewards low leverage; penalizes negative equity which signals structural financial distress.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C3-01 | debtToEquity | < 2.0 | +1 |
| C3-02 | debtToEquity | < 1.0 | +1 |
| C3-03 | debtToEquity | < 0.5 | +1 |
| C3-04 | debtToEquity | < 0 (negative equity — overrides Q47–Q49) | −3 |

### Cash Burn Safety
*Confirms the stock is not at risk of running out of cash based on profitability, cash flow, or size.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C3-05 | netProfitMargin ≥ 0 OR operatingCashFlow ≥ 0 OR marketCap ≥ 10000000000 | any true | +1 |

### Deterioration Risk
*Penalizes absence of point when all three core metrics are simultaneously declining year-over-year.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C3-06 | NOT (revenueGrowth < 0 AND operatingIncome < 0 AND operatingCashFlow < 0) | = true | +1 |

### Interest Coverage TTM
*Rewards the company's ability to service its debt; higher coverage = lower financial risk.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C3-07 | interestCoverageTTM | > 1.5x | +1 |
| C3-08 | interestCoverageTTM | > 3x | +1 |
| C3-09 | interestCoverageTTM | > 5x | +1 |
| C3-10 | interestCoverageTTM | > 10x | +1 |

### Current Ratio
*Rewards short-term liquidity — the ability to cover near-term obligations with current assets.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C3-11 | currentRatio | > 1.0 | +1 |
| C3-12 | currentRatio | > 1.5 | +1 |
| C3-13 | currentRatio | > 2.0 | +1 |

### Net Debt Position
*Awards a point when the company holds more cash than debt — a net cash position.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C3-14 | netCashQ0 | > 0 (net cash position) | +1 |

### Leverage Trend (Deleveraging)
*Awards a point when debt-to-equity is actively improving quarter-over-quarter.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C3-15 | debtToEquityQ0 | < debtToEquityQ1 (deleveraging) | +1 |

---

## C4: Valuation

### High P/E Momentum Trap
*Penalizes high-valuation stocks showing sharp recent declines, and flags extreme valuations separately.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C4-01 | NOT (peRatio > 50 AND change10d < −5%) | = true | +1 |
| C4-02 | peRatio | > 100 (extreme valuation — penalty) | −1 |

### PE Ratio TTM
*Rewards reasonable valuations; stacked tiers progressively reward cheaper stocks.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C4-03 | peRatioTTM | > 0 (profitable) | +1 |
| C4-04 | peRatioTTM | < 100 | +1 |
| C4-05 | peRatioTTM | < 40 | +1 |
| C4-06 | peRatioTTM | < 25 | +1 |
| C4-07 | peRatioTTM | < 15 | +1 |

### Price-to-Sales TTM
*Rewards lower price-to-sales ratios, with tighter tiers rewarding more attractively valued stocks.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C4-08 | priceToSalesTTM | < 50 | +1 |
| C4-09 | priceToSalesTTM | < 8 | +1 |
| C4-10 | priceToSalesTTM | < 4 | +1 |
| C4-11 | priceToSalesTTM | < 2 | +1 |

### EV/EBITDA TTM
*Rewards enterprise value relative to earnings before interest and taxes at three threshold tiers.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C4-12 | evToEbitda | < 40 | +1 |
| C4-13 | evToEbitda | < 20 | +1 |
| C4-14 | evToEbitda | < 10 | +1 |

### FCF Yield TTM
*Rewards strong free cash flow relative to market cap; penalizes negative or severely negative FCF yield.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C4-15 | freeCashFlowYield | > 4% | +1 |
| C4-16 | freeCashFlowYield | > 8% | +1 |
| C4-17 | freeCashFlowYield | < 0% (negative FCF yield) | −1 |
| C4-18 | freeCashFlowYield | < −5% (severely negative) | −1 |

---

## C5: Technical & Momentum

### 1-Month Price Change
*Rewards recent upward price momentum across four magnitude tiers.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C5-01 | change1m | > 0% | +1 |
| C5-02 | change1m | > 5% | +1 |
| C5-03 | change1m | > 10% | +1 |
| C5-04 | change1m | > 20% | +1 |

### 10-Day Price Change
*Rewards very short-term price momentum at four magnitude tiers.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C5-05 | change10d | > 0% | +1 |
| C5-06 | change10d | ≥ 5% | +1 |
| C5-07 | change10d | ≥ 10% | +1 |
| C5-08 | change10d | ≥ 15% | +1 |

### Price vs Moving Averages
*Rewards price being above each key moving average as a proxy for trend strength.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C5-09 | price | > sma20 | +1 |
| C5-10 | price | > sma50 | +1 |
| C5-11 | price | > sma100 | +1 |
| C5-12 | price | > sma200 | +1 |

### Momentum Magnitude
*Measures the combined size of 52-week and 3-month gains as a proxy for sustained trend strength.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C5-13 | change52w + change3m | sum > 50% | +1 |
| C5-14 | change52w + change3m | sum > 100% | +1 |
| C5-15 | change52w + change3m | sum > 150% | +1 |

### Weighted Momentum
*Formula-weighted blend of annual and quarterly momentum (70/30 split), giving more importance to the longer trend.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C5-16 | (0.7 × change52w) + (0.3 × change3m) | > 40 | +1 |
| C5-17 | (0.7 × change52w) + (0.3 × change3m) | > 80 | +1 |

### Momentum Divergence
*Guards against stocks with a strong year but collapsing short-term momentum across all windows.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C5-18 | NOT (change52w > 0 AND change3m < 0 AND change1m < 0 AND change10d < 0) | = true | +1 |

### Bollinger %B
*Measures where price sits within the Bollinger Band range; rewards higher positions including breakouts.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C5-19 | bollingerPercentB | > 20% | +1 |
| C5-20 | bollingerPercentB | > 80% | +1 |
| C5-21 | bollingerPercentB | > 95% | +1 |
| C5-22 | bollingerPercentB | > 100% | +1 |

### Momentum Quality
*Rewards smooth cascading momentum; penalizes spike patterns where 10-day is detached from 1-month.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C5-23 | change52w > 0 AND change3m > 0 AND change1m > 0 AND change10d > 0 | = true | +1 |
| C5-24 | change52w > change3m AND change3m > change1m AND change1m > change10d AND all > 0 | = true | +1 |
| C5-25 | NOT (change10d > 20% AND change1m < 10%) | no spike risk | +1 |

### Sustained Downtrend
*Flags stocks declining across all three short-term timeframes simultaneously.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C5-26 | NOT (change1d < 0 AND change5d < 0 AND change1m < 0) | = true | +1 |

### Sudden Drop / Slide
*Detects abnormal single-day crashes or cumulative 5-day slides that signal acute danger.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C5-27 | worstDrop3d > −7% OR change5d > −10% | no severe slide | +1 |
| C5-28 | worstDrop3d | > −10% (no single day ≥10% drop last 3 days) | +1 |

### Trend Deterioration
*Penalizes absence of point when price is making lower highs and lower lows — structural downtrend.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C5-29 | hasLowerHighsLowerLows | = false | +1 |

### 2-Week Price Change
*Rewards positive price momentum over the 2-week window at three magnitude tiers.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C5-30 | change2w | > 0% | +1 |
| C5-31 | change2w | > 5% | +1 |
| C5-32 | change2w | > 10% | +1 |

### 3-Month Price Change
*Rewards medium-term price momentum at three magnitude tiers.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C5-33 | change3m | > 0% | +1 |
| C5-34 | change3m | > 15% | +1 |
| C5-35 | change3m | > 30% | +1 |

### 6-Month Price Change
*Rewards longer-term price momentum at three magnitude tiers.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C5-36 | change6m | > 0% | +1 |
| C5-37 | change6m | > 25% | +1 |
| C5-38 | change6m | > 50% | +1 |

### Near 52-Week High / Low
*Rewards stocks close to their yearly highs; penalizes stocks near their yearly lows.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C5-39 | price vs high52w | within 5% of 52W high | +1 |
| C5-40 | price vs low52w | within 5% of 52W low | −1 |

---

## C6: Relative Strength

### Sector Performance vs SPY
*Measures whether the stock is outperforming or underperforming the S&P 500 over 1 month.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C6-01 | change1m − spyChange1m | > 0% | +1 |
| C6-02 | change1m − spyChange1m | > 10% | +1 |
| C6-03 | change1m − spyChange1m | < −10% | −1 |

### 5-Day Relative Strength vs QQQ
*Measures alpha vs. QQQ over 5 days; rewards stocks leading the market and penalizes laggards.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C6-04 | change5d − qqqChange5d | ≥ 0% | +1 |
| C6-05 | change5d − qqqChange5d | ≥ 5% | +1 |
| C6-06 | change5d > 0 AND qqqChange5d < 0 | stock up while market down | +1 |
| C6-07 | change5d < 0 AND qqqChange5d > 0 AND alpha ≤ −5% | = true | −3 |
| C6-08 | change5d − qqqChange5d < −5% AND NOT (change5d < 0 AND qqqChange5d > 0) | = true | −2 |

### 3-Month Relative Strength vs SPY
*Rewards stocks outperforming the S&P 500 over 3 months at three magnitude tiers.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C6-09 | change3m vs spyChange3m | > 0% | +1 |
| C6-10 | change3m vs spyChange3m | > 5% | +1 |
| C6-11 | change3m vs spyChange3m | > 15% | +1 |

### 10D vs SPY Underperformance Guard
*Penalizes absence of point when stock drops sharply while SPY is rising — stock-specific weakness.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C6-12 | stockRS10d vs spyChange10d | NOT (stock < −5% AND SPY > 1%) | +1 |

### 52W vs QQQ Tracking Band
*Awards a point for stocks tracking closely to QQQ annual performance — neither diverging nor lagging badly.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C6-13 | change52w vs qqqChange52w | alpha between −1% and +1% | +1 |

---

## C7: Volume & Liquidity

### 20-Day Average Volume
*Rewards minimum liquidity thresholds so the stock is actively traded.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C7-01 | avgVolume20d | ≥ 200K | +1 |
| C7-02 | avgVolume20d | ≥ 500K | +1 |
| C7-03 | avgVolume20d | ≥ 1M | +1 |

### Daily Dollar Volume
*Rewards sufficient dollar liquidity so positions can be entered and exited without slippage.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C7-04 | avgDailyDollarVolume20d | > $5M | +1 |
| C7-05 | avgDailyDollarVolume20d | > $20M | +1 |
| C7-06 | avgDailyDollarVolume20d | > $100M | +1 |

### Volume Ratio (Today vs 20D Avg)
*Rewards elevated volume relative to the 20-day average as a signal of institutional interest.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C7-07 | volumeRatio | > 1.1x | +1 |
| C7-08 | volumeRatio | > 1.5x | +1 |

### Volume Surge
*Rewards high-volume up days (especially near 52W highs); penalizes high-volume selling pressure.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C7-09 | volume ≥ 2x AND price | UP | +1 |
| C7-10 | volume ≥ 2x AND price UP AND price | within 5% of 52W high | +1 |
| C7-11 | volume ≥ 2x AND price | DOWN | −1 |
| C7-12 | volume ≥ 2x AND price DOWN AND price | within 5% of 52W low | −1 |

### Float Turnover
*Awards a point when daily float turnover is ≥ 2%, indicating active institutional trading activity.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C7-13 | floatTurnover | ≥ 2% daily | +1 |

---

## C8: Volatility

### Volatility — ATR%
*Rewards low realized volatility — smoother stocks are more predictable for swing trading.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C8-01 | atr20DPercent | < 6% | +1 |
| C8-02 | atr20DPercent | < 4% | +1 |
| C8-03 | atr20DPercent | < 2.5% | +1 |

### Realized Volatility 20D
*Rewards lower realized volatility — calmer stocks are preferred for predictable swing setups.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C8-04 | realizedVol20D | < 0.60 | +1 |
| C8-05 | realizedVol20D | < 0.45 | +1 |
| C8-06 | realizedVol20D | < 0.30 | +1 |

---

## C9: Ownership & Coverage

### Institutional Ownership
*Rewards meaningful institutional presence as a signal of professional validation and stability.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C9-01 | institutionalOwnershipPct | > 0% | +1 |
| C9-02 | institutionalOwnershipPct | > 20% | +1 |

### Analyst Coverage
*Rewards stocks with active analyst coverage as a proxy for visibility and information quality.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C9-03 | analystCount | > 0 | +1 |
| C9-04 | analystCount | > 5 | +1 |

### Insider Activity
*Rewards net insider buying; penalizes net selling; also tracks institutional ownership changes.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C9-05 | netInsiderTransactions | buys > sells | +1 |
| C9-06 | netInsiderTransactions | sells > buys | −1 |
| C9-07 | instOwnershipChange QoQ | ≥ +1% | +1 |
| C9-08 | instOwnershipChange QoQ | ≤ −1% | −1 |

### Has Options
*Awards a point if the stock has listed options — signals sufficient size and trading interest.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C9-09 | hasOptions | = true | +1 |

---

## C10: Earnings & Events

### Earnings — EPS Beat / Miss
*Rewards stocks that beat earnings estimates; penalizes misses as a signal of execution risk.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C10-01 | actualEps vs estimatedEps | actual > estimated | +1 |
| C10-02 | actualEps vs estimatedEps | actual < estimated | −1 |

### Post-Earnings Gap
*Rewards positive post-earnings price reactions; penalizes severe post-earnings selloffs.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C10-03 | postEarningsGap | > 0% | +1 |
| C10-04 | postEarningsGap | ≥ 5% | +1 |
| C10-05 | postEarningsGap | ≤ −5% | −2 |

### Earnings Guidance
*Rewards positive or raised forward guidance as a signal of management confidence.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C10-06 | earningsGuidance | = positive or raised | +1 |
| C10-07 | earningsGuidance | = raised (specifically) | +1 |

### Major Catalyst
*Awards a point for confirmed positive catalysts such as product launches, contracts, or regulatory approvals.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C10-08 | majorCatalyst | positive catalyst present | +1 |

---

## C11: Risk & Penalty

### Country
*Awards a point for US-listed domestic companies as the lowest-risk regulatory environment.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C11-01 | country | = USA | +1 |

### Sector Preference
*Rewards preferred sectors; penalizes crypto-related stocks regardless of other signals; awards a clean bonus for non-crypto.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C11-02 | sector | in [Technology, Financial Services, Industrials, Communication Services, Healthcare, Consumer Defensive, Consumer Cyclical, Real Estate] AND NOT crypto | +1 |
| C11-03 | sector | in [Technology, Financial Services, Industrials, Communication Services] AND NOT crypto | +1 |
| C11-04 | symbol | NOT in [cryptoSymbols] | +1 |
| C11-05 | symbol | in [cryptoSymbols] | −4 |

### Biotech Spike Risk
*Penalizes biotech/pharma stocks with abnormally large short-term gains — likely binary event noise.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C11-06 | NOT (sector in [Healthcare, Biotechnology] AND change10d > 15%) | = true | +1 |

### Short Interest Risk
*Rewards low short interest; penalizes elevated and high short interest — a signal of bearish professional conviction.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C11-07 | shortPercentFloat | < 20% | +1 |
| C11-08 | shortPercentFloat | < 10% | +1 |
| C11-09 | shortPercentFloat | > 20% | −1 |
| C11-10 | shortPercentFloat | > 30% | −1 |

### Low Float Risk
*Rewards adequate float size; thin floats are prone to manipulation and erratic price swings.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C11-11 | floatShares | ≥ 20M | +1 |

### Mid-Cap Tech Penalty
*Penalizes absence of point for unprofitable mid-cap tech stocks — high risk with unproven business model.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C11-12 | midCapTech | NOT (tech AND $4B–$40B) OR profitable | +1 |

### SEC Investigation
*Awards a point when the company has no active SEC investigation, fraud case, or amended filings.*

| # | Field | Condition | Pts |
|---|---|---|---|
| C11-13 | secInvestigation | = false (clean) | +1 |

---

## CAA: AI Assessment
*AI-driven qualitative layer. Questions require judgment rather than raw data lookups.*

### Growth Sustainability
*Awards a point if at least one growth metric (annual or quarterly revenue) remains positive.*

| # | Field | Condition | Pts |
|---|---|---|---|
| CAA-01 | annualRevenueGrowth OR quarterlyRevenueGrowth | either > 0% | +1 |

### Earnings Guidance (CAA version)
*AI-assessed guidance tone — rewards positive language and raised guidance; penalizes caution or withdrawal.*

| # | Field | Condition | Pts |
|---|---|---|---|
| CAA-02 | earningsGuidanceAA | = positive language | +1 |
| CAA-03 | earningsGuidanceAA | = raised | +1 |
| CAA-04 | earningsGuidanceAA | = cautious | −1 |
| CAA-05 | earningsGuidanceAA | = lowered | −3 |
| CAA-06 | earningsGuidanceAA | = withdrawn | −4 |

### Major Catalyst (CAA version)
*AI-assessed catalyst presence — rewards confirmed positive events; penalizes confirmed negative ones.*

| # | Field | Condition | Pts |
|---|---|---|---|
| CAA-07 | majorCatalystAA | positive confirmed | +1 |
| CAA-08 | majorCatalystAA | negative confirmed | −3 |

### SEC / Fraud Risk (CAA version)
*AI-assessed clean record — no fraud, active investigation, or material restatements.*

| # | Field | Condition | Pts |
|---|---|---|---|
| CAA-09 | secFraudRisk | clean (no fraud/investigation/amended filing) | +1 |

---

## CF: Custom Fields
*Requires fields not in standard FMP data — implement after custom field infrastructure is confirmed.*

### Competitive Moat
*Rewards companies with gross margin or ROE above peer average; double reward if both are above.*

| # | Field | Condition | Pts |
|---|---|---|---|
| CF-01 | grossMarginPct vs peerAvgGrossMargin OR roe vs peerAvgROE | either above peer avg | +1 |
| CF-02 | grossMarginPct vs peerAvgGrossMargin AND roe vs peerAvgROE | both above peer avg | +1 |

### Revenue Segments
*Awards a point for companies with ≥ 3 revenue segments all showing growth — diversification bonus.*

| # | Field | Condition | Pts |
|---|---|---|---|
| CF-03 | revenueSegments AND both growth metrics | ≥ 3 segments AND annualRevGrowth > 0 AND quarterlyRevGrowth > 0 | +1 |

### Management Quality — Executive Turnover
*Rewards zero executive turnover in 12 months; penalizes high turnover or net insider selling.*

| # | Field | Condition | Pts |
|---|---|---|---|
| CF-04 | executiveTurnoverLast12m | = 0 | +1 |
| CF-05 | executiveTurnoverLast12m OR insider sells | ≥ 2 departures OR netInsiderSells > netInsiderBuys | −2 |

### Profitability Stability vs Prior Year
*Rewards sustained positive margins year-over-year; penalizes a flip from profitable to unprofitable.*

| # | Field | Condition | Pts |
|---|---|---|---|
| CF-06 | netProfitMargin + netProfitMarginPriorYear | both > 0 | +1 |
| CF-07 | netProfitMargin + netProfitMarginPriorYear | both > 0 AND drop < 5pp | +1 |
| CF-08 | netProfitMarginPriorYear > 0 AND netProfitMargin < 0 | positive → negative | −1 |

### Relative Valuation vs Sector
*Rewards trading at a discount to sector median PE; penalizes trading at a significant premium.*

| # | Field | Condition | Pts |
|---|---|---|---|
| CF-09 | peRatioTTM vs sectorMedianPE | ≤ 0.8× sector median | +1 |
| CF-10 | peRatioTTM vs sectorMedianPE | > 1.2× sector median | −1 |

---

## Post-Score (Pulse) Section
*Applied after SA Core score is computed. Requires SA Core ≥ 70 to qualify.*

### Pulse Questions
*Contextual market environment and score history checks applied on top of the SA Core.*

| # | Field | Condition | Pts |
|---|---|---|---|
| PQ-01 | saScoreHistory | SA ≥ 80 for 5+ consecutive days | +1 |
| PQ-02 | mcScore | MC between 30 and 80 | +1 |
| PQ-03 | qqqChange5d AND qqqChange1m | both > 0% | +1 |
| PQ-04 | cashFlowGrowthPts ≥ 4 AND spyAlpha1mPts ≥ 3 AND volumeSurgePts ≥ 4 | combo threshold met | +1 |
| PQ-05 | vixPrice | VIX between 25 and 29 | +1 |
| PQ-06 | vixPrice | VIX ≥ 30 | +1 |
| PQ-07 | mcScore | MC ≥ 20 | +1 |
| PQ-08 | mcScore | MC ≥ 30 | +1 |
| SA-195 # | Block | Reason |
| Q88–Q90 | 1-Day Change (>0%, >1%, >3%) | Too noisy for swing trading; 10-day window is sufficient |
| Q137–Q140 | Market Cap ($300M, $2B, $10B, $50B) | Covered indirectly by volume, dollar volume, and liquidity blocks |
| PQ-12 | Country — Developed market +1 | USA-only +1 retained; developed market tier removed as marginal signal |

---

## Intentionally Excluded from SA-195-Bi

The following SA-195-Bi questions were reviewed and excluded by design:

| SA-195 # | Block | Reason |
|---|---|---|
| Q88–Q90 | 1-Day Change (>0%, >1%, >3%) | Too noisy for swing trading; 10-day window is sufficient |
| Q137–Q140 | Market Cap ($300M, $2B, $10B, $50B) | Covered indirectly by volume, dollar volume, and liquidity blocks |
| Q169 | Country — Developed market +1 | USA-only +1 retained; developed market tier removed as marginal signal |
