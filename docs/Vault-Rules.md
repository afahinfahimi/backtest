# Engine Rules Reference
*Exported: 2026-03-09*

Use rule IDs (e.g. "Q5", "R1", "M-V2", "NORM-SA", "CONST-CRYPTO", "CE-80") when requesting changes.

---

## SA Engine — V17 (32 Questions)

**Normalization:** min -43, max 70
**Post-processing:** Q16+Q17 max -4

### Q1: Sales Growth

- **Points range:** 0 to 6
- **Inputs:** annualRevenueGrowth, quarterlyRevenueGrowth
- **Missing data:** midpoint
- **Context caps:** isCyclicalNoBreakout → max 4

| Conditions | Pts | Interpretation |
|---|---|---|
| annualRevenueGrowth >= 50 AND quarterlyRevenueGrowth > annualRevenueGrowth | +6 | Accelerating Exceptional |
| annualRevenueGrowth >= 50 AND quarterlyRevenueGrowth > 0 | +5 | Steady Exceptional |
| annualRevenueGrowth >= 20 AND annualRevenueGrowth < 50 AND quarterlyRevenueGrowth > annualRevenueGrowth | +5 | Accelerating Strong |
| annualRevenueGrowth >= 20 AND annualRevenueGrowth < 50 AND quarterlyRevenueGrowth > 0 | +4 | Steady Strong |
| annualRevenueGrowth >= 1 AND annualRevenueGrowth < 20 AND quarterlyRevenueGrowth > 0 | +2 | Growing |
| annualRevenueGrowth >= 0 AND quarterlyRevenueGrowth <= 0 | +1 | Stalling |
| annualRevenueGrowth < 0 AND quarterlyRevenueGrowth > 0 | +1 | Recovering |
| *(default)* | 0 | Declining |

### Q2: Operating Income Growth

- **Points range:** 0 to 6
- **Inputs:** annualOperatingIncomeGrowth, quarterlyOperatingIncomeGrowth
- **Missing data:** midpoint
- **Context caps:** isCyclicalNoBreakout → max 4

| Conditions | Pts | Interpretation |
|---|---|---|
| annualOperatingIncomeGrowth >= 50 AND quarterlyOperatingIncomeGrowth > annualOperatingIncomeGrowth | +6 | Accelerating Exceptional |
| annualOperatingIncomeGrowth >= 50 AND quarterlyOperatingIncomeGrowth > 0 | +5 | Steady Exceptional |
| annualOperatingIncomeGrowth >= 20 AND annualOperatingIncomeGrowth < 50 AND quarterlyOperatingIncomeGrowth > annualOperatingIncomeGrowth | +5 | Accelerating Strong |
| annualOperatingIncomeGrowth >= 20 AND annualOperatingIncomeGrowth < 50 AND quarterlyOperatingIncomeGrowth > 0 | +4 | Steady Strong |
| annualOperatingIncomeGrowth >= 1 AND annualOperatingIncomeGrowth < 20 AND quarterlyOperatingIncomeGrowth > 0 | +2 | Growing |
| annualOperatingIncomeGrowth >= 0 AND quarterlyOperatingIncomeGrowth <= 0 | +1 | Stalling |
| annualOperatingIncomeGrowth < 0 AND quarterlyOperatingIncomeGrowth > 0 | +1 | Recovering |
| *(default)* | 0 | Declining |

### Q3: Cash Flow Growth

- **Points range:** 0 to 6
- **Inputs:** annualCashFlowGrowth, quarterlyCashFlowGrowth
- **Missing data:** midpoint
- **Context caps:** isCyclicalNoBreakout → max 4

| Conditions | Pts | Interpretation |
|---|---|---|
| annualCashFlowGrowth >= 50 AND quarterlyCashFlowGrowth > annualCashFlowGrowth | +6 | Accelerating Exceptional |
| annualCashFlowGrowth >= 50 AND quarterlyCashFlowGrowth > 0 | +5 | Steady Exceptional |
| annualCashFlowGrowth >= 20 AND annualCashFlowGrowth < 50 AND quarterlyCashFlowGrowth > annualCashFlowGrowth | +5 | Accelerating Strong |
| annualCashFlowGrowth >= 20 AND annualCashFlowGrowth < 50 AND quarterlyCashFlowGrowth > 0 | +4 | Steady Strong |
| annualCashFlowGrowth >= 1 AND annualCashFlowGrowth < 20 AND quarterlyCashFlowGrowth > 0 | +2 | Growing |
| annualCashFlowGrowth >= 0 AND quarterlyCashFlowGrowth <= 0 | +1 | Stalling |
| annualCashFlowGrowth < 0 AND quarterlyCashFlowGrowth > 0 | +1 | Recovering |
| *(default)* | 0 | Declining |

### Q4: Net Profit Margin

- **Points range:** -2 to 3
- **Inputs:** netProfitMargin
- **Missing data:** midpoint

| Conditions | Pts | Interpretation |
|---|---|---|
| netProfitMargin > 10 | +3 | Strong |
| netProfitMargin > 0 | +1 | Positive |
| netProfitMargin == 0 | 0 | Breakeven |
| *(default)* | -2 | Unprofitable |

### Q5: 1-Month Price Change

- **Points range:** 0 to 4
- **Inputs:** change1m
- **Missing data:** midpoint

| Conditions | Pts | Interpretation |
|---|---|---|
| change1m >= 20 | +4 | Strong momentum |
| change1m >= 10 | +3 | Good momentum |
| change1m >= 5 | +2 | Positive |
| change1m > 0 | +1 | Slight positive |
| *(default)* | 0 | Negative/Flat |

### Q6: 10-Day Price Change

- **Points range:** 0 to 3
- **Inputs:** change10d
- **Missing data:** midpoint

| Conditions | Pts | Interpretation |
|---|---|---|
| change10d >= 15 | +3 | Strong |
| change10d >= 10 | +2 | Good |
| change10d >= 5 | +1 | Positive |
| *(default)* | 0 | Weak |

### Q7: 20-Day Average Volume

- **Points range:** 0 to 3
- **Inputs:** avgVolume20d
- **Missing data:** midpoint

| Conditions | Pts | Interpretation |
|---|---|---|
| avgVolume20d >= 1000000 | +3 | High liquidity |
| avgVolume20d >= 500000 | +2 | Good liquidity |
| avgVolume20d >= 200000 | +1 | Moderate |
| *(default)* | 0 | Low liquidity |

### Q8: Market Cap

- **Points range:** 0 to 2
- **Inputs:** marketCap
- **Missing data:** midpoint

| Conditions | Pts | Interpretation |
|---|---|---|
| marketCap > 40000000000 | +2 | Large cap (>40B) |
| marketCap >= 4000000000 | +1 | Mid cap (4-40B) |
| *(default)* | 0 | Small cap (<4B) |

### Q9: Price vs Moving Averages

- **Points range:** 0 to 4
- **Inputs:** price, sma20, sma50
- **Missing data:** midpoint

| Conditions | Pts | Interpretation |
|---|---|---|
| price > sma20 AND price > sma50 | +4 | Above both 20D & 50D |
| price > sma50 | +3 | Above 50D only |
| price > sma20 | +2 | Above 20D only |
| *(default)* | 0 | Below both |

### Q10: Debt-to-Equity Ratio

- **Points range:** -3 to 3
- **Inputs:** debtToEquity
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| debtToEquity < 0 | -3 | Negative equity |
| debtToEquity < 0.5 | +3 | Excellent |
| debtToEquity < 1 | +2 | Good |
| debtToEquity < 2 | +1 | Moderate |
| *(default)* | 0 | High debt |

### Q11: Momentum Magnitude

- **Points range:** 0 to 3
- **Inputs:** change52w, change3m
- **Missing data:** midpoint

| Conditions | Pts | Interpretation |
|---|---|---|
| _momSum > 150 | +3 | Exceptional momentum |
| _momSum > 100 | +2 | Strong momentum |
| _momSum > 50 | +1 | Moderate momentum |
| *(default)* | 0 | Weak momentum |

### Q12: EPS Growth Prior Year

- **Points range:** 0 to 3
- **Inputs:** epsGrowthPriorYear
- **Missing data:** midpoint

| Conditions | Pts | Interpretation |
|---|---|---|
| epsGrowthPriorYear >= 100 | +2 | Exceptional |
| epsGrowthPriorYear >= 50 | +3 | Strong |
| epsGrowthPriorYear >= 25 | +2 | Good |
| epsGrowthPriorYear > 0 | +1 | Positive |
| *(default)* | 0 | Negative/Flat |

### Q13: Return on Equity

- **Points range:** 0 to 2
- **Inputs:** roe
- **Missing data:** midpoint

| Conditions | Pts | Interpretation |
|---|---|---|
| roe >= 20 | +2 | Excellent |
| *(default)* | 0 | Below threshold |

### Q14: Return on Assets

- **Points range:** 0 to 3
- **Inputs:** roa
- **Missing data:** midpoint

| Conditions | Pts | Interpretation |
|---|---|---|
| roa >= 15 | +3 | Excellent |
| roa >= 10 | +2 | Good |
| roa >= 5 | +1 | Moderate |
| *(default)* | 0 | Low |

### Q15: Country

- **Points range:** 0 to 0
- **Inputs:** country
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| country in [usCountries] | 0 | USA |
| country in [developedCountries] | 0 | Developed |
| country in [chinaEmCountries] | 0 | China/Emerging Market |
| *(default)* | 0 | Other |

### Q16: Cash Burn Risk

- **Points range:** -3 to 0
- **Inputs:** netProfitMargin
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| netProfitMargin >= 0 | 0 | Profitable |
| operatingCashFlowQuarterly >= 0 | 0 | Positive cash flow |
| marketCap >= 10000000000 | 0 | Large cap buffer |
| *(default)* | -3 | Cash burn risk |

### Q17: Deterioration Risk

- **Points range:** -3 to 0
- **Inputs:** revenueQoQ, operatingIncomeQoQ, cashFlowQoQ
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| revenueQoQ < 0 AND operatingIncomeQoQ < 0 AND cashFlowQoQ < 0 | -3 | All metrics declining QoQ |
| *(default)* | 0 | No deterioration |

### Q18: Financial Strength

- **Points range:** 0 to 3
- **Inputs:** netProfitMargin, roe, debtToEquity
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| netProfitMargin >= 20 AND roe >= 20 AND debtToEquity < 0.5 | +3 | Excellent |
| netProfitMargin >= 10 AND roe >= 10 AND debtToEquity < 1.5 | +2 | Good |
| netProfitMargin >= 0 AND roe >= 5 AND debtToEquity < 3 | +1 | Moderate |
| *(default)* | 0 | Weak |

### Q19: Momentum Divergence Penalty

- **Points range:** -3 to 0
- **Inputs:** change52w, change3m, change1m, change10d
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| change52w > 0 AND change3m < 0 AND change1m < 0 AND change10d < 0 | -3 | Momentum divergence |
| *(default)* | 0 | No divergence |

### Q20: Sector Preference

- **Points range:** -10 to 2
- **Inputs:** sector
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| _symbol in [cryptoSymbols] | -4 | Crypto-related |
| _symbol in [metalsMiningSymbols] | 0 | Metals & Mining (override) |
| _symbol in [cleanEnergySymbols] | +2 | Clean Energy (override) |
| _symbol in [oilGasSymbols] | -2 | Oil & Gas |
| sector in [preferredSectors] | +2 | Preferred sector |
| sector in [neutralSectors] | +1 | Neutral sector |
| sector in [weakSectors] | -10 | Weak sector |
| *(default)* | 0 | Default |

### Q21: %B Position (Bollinger Bands)

- **Points range:** 0 to 4
- **Inputs:** bollingerPercentB
- **Missing data:** midpoint

| Conditions | Pts | Interpretation |
|---|---|---|
| bollingerPercentB > 100 | +4 | Breakout |
| bollingerPercentB > 95 | +3 | Near top |
| bollingerPercentB >= 80 | +2 | Upper zone |
| bollingerPercentB >= 20 | +1 | Mid-range |
| *(default)* | 0 | Buy zone |

### Q22: Momentum Quality

- **Points range:** -1 to 2
- **Inputs:** change52w, change3m, change1m, change10d
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| change10d > 20 AND change1m < 10 | -1 | Spike Risk |
| change52w > 0 AND change3m > 0 AND change1m > 0 AND change52w > change3m AND change3m > change1m AND change1m > change10d | +2 | Smooth momentum |
| change3m > 0 AND _accelCheck > change52w | +1 | Accelerating |
| *(default)* | 0 | Other |

### Q23: High P/E Momentum Trap

- **Points range:** -4 to 0
- **Inputs:** peRatio, change10d
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| peRatio > 50 AND change10d < -5 | -4 | High P/E momentum trap |
| *(default)* | 0 | No trap |

### Q24: Biotech Binary Event Burn

- **Points range:** -3 to 0
- **Inputs:** sector, change10d
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| sector in [biotechSectors] AND change10d > 15 | -3 | Biotech spike risk |
| *(default)* | 0 | N/A |

### Q25: Sustained Downtrend

- **Points range:** -3 to 0
- **Inputs:** change1d, change5d, change1m
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| change1d < 0 AND change5d < 0 AND change1m < 0 | -3 | Sustained downtrend |
| *(default)* | 0 | No downtrend |

### Q26: Sudden Drop / Slide

- **Points range:** -6 to 0
- **Inputs:** dailyChanges
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| _worstDrop3d <= -15 | -6 | Critical drop (15%+) |
| _worstDrop3d <= -10 | -2 | Severe drop (10%+) |
| _worstDrop3d <= -7 | -1 | Caution drop (7%+) |
| _cumulative5d <= -10 | -1 | Cumulative 5-day decline > 10% |
| *(default)* | 0 | No sudden drops |

### Q27: Short Interest Risk

- **Points range:** -1 to 0
- **Inputs:** shortPercentFloat
- **Missing data:** zero — No short data available

| Conditions | Pts | Interpretation |
|---|---|---|
| shortPercentFloat > 20 | -1 | High short interest |
| *(default)* | 0 | Normal |

### Q28: Low Float Risk

- **Points range:** -1 to 0
- **Inputs:** floatShares
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| floatShares < 20000000 | -1 | Low float risk |
| *(default)* | 0 | Normal float |

### Q29: Sector Performance vs Peers

- **Points range:** -1 to 1
- **Inputs:** change1m, spyChange1m
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| _spyDiff1m > 10 | +1 | Outperforming SPY |
| _spyDiff1m < -10 | -1 | Underperforming SPY |
| *(default)* | 0 | In line with SPY |

### Q30: 5-Day Relative Strength

- **Points range:** -3 to 3
- **Inputs:** change5d, qqqChange5d
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| change5d > 0 AND qqqChange5d < 0 | +3 | Up while market down |
| _alpha5d >= 5 | +2 | Strong alpha |
| _alpha5d >= 0 | +1 | Slight alpha |
| _alpha5d >= -5 | 0 | Slight underperformance |
| change5d < 0 AND qqqChange5d > 0 | -3 | Down while market up |
| *(default)* | -2 | Significant underperformance |

### Q31: Trend Deterioration

- **Points range:** -3 to 0
- **Inputs:** hasLowerHighsLowerLows
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| hasLowerHighsLowerLows == true | -3 | Lower highs AND lower lows |
| *(default)* | 0 | No structural downtrend |

### Q32: Mid-Cap Tech Penalty

- **Points range:** -3 to 0
- **Inputs:** sector, marketCap
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| sector == Technology AND marketCap >= 4000000000 AND marketCap < 40000000000 | -3 | Mid-cap Tech penalty |
| *(default)* | 0 | N/A |

---

## MC Engine — V16 (17 Questions)

**Normalization:** min -40, max 52

### Q1: QQQ Price vs MAs

- **Points range:** -5 to 5
- **Inputs:** qqqPrice, qqqSMA50, qqqSMA200
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| qqqPrice <= qqqSMA50 AND qqqPrice <= qqqSMA200 | +5 | Below both MAs (Oversold - Buy Opportunity) |
| qqqPrice <= qqqSMA200 AND qqqPrice > qqqSMA50 | +2 | Below 200MA only |
| qqqPrice > qqqSMA200 AND qqqPrice <= qqqSMA50 | -2 | Above 200MA only |
| *(default)* | -5 | Above both MAs (Extended - Caution) |

### Q2: Trend Confirmation

- **Points range:** -3 to 5
- **Inputs:** qqqSMA50, qqqSMA200
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| _maSpreadAbs <= 1 | +5 | MAs flat or converging (Inflection Point) |
| _maSpread < 0 AND _maSpreadAbs < 5 | +3 | 50MA below 200MA, < 5% spread (Early Recovery) |
| _maSpread > 0 AND _maSpread < 5 | +1 | 50MA above 200MA, < 5% spread (Mild Uptrend) |
| _maSpread >= 5 | -3 | 50MA ≥ 5% above 200MA (Extended Uptrend) |
| *(default)* | -3 | 50MA ≥ 5% below 200MA (Deep Downtrend) |

### Q3: RSI Momentum

- **Points range:** -3 to 5
- **Inputs:** qqqRSI
- **Missing data:** custom

| Conditions | Pts | Interpretation |
|---|---|---|
| qqqRSI < 30 | +5 | Oversold Opportunity |
| qqqRSI >= 30 AND qqqRSI < 40 | +1 | Low Momentum |
| qqqRSI >= 40 AND qqqRSI < 50 | +2 | Below Average |
| qqqRSI >= 50 AND qqqRSI < 60 | +3 | Healthy |
| qqqRSI >= 60 AND qqqRSI < 70 | +1 | Above Average |
| qqqRSI >= 70 | -3 | Overbought Risk |
| *(default)* | +1 | Moderate zone |

### Q4: VIX vs 3-Month Avg

- **Points range:** -5 to 5
- **Inputs:** vix3mChange
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| vix3mChange > 20 | +5 | VIX spiking (Buy Opportunity) |
| vix3mChange >= 10 | +3 | VIX rising |
| vix3mChange >= -10 | 0 | VIX near avg |
| vix3mChange >= -20 | -3 | VIX falling |
| *(default)* | -5 | VIX well below avg (Complacency) |

### Q5: VIX Absolute Level

- **Points range:** -3 to 5
- **Inputs:** vixPrice
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| vixPrice > 22 | +5 | High Fear (Buy Opportunity) |
| vixPrice >= 14 | 0 | Normal Range |
| *(default)* | -3 | Complacency (Caution) |

### Q6: QQQ 52-Week Strength

- **Points range:** -3 to 5
- **Inputs:** qqq52WChange
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| qqq52WChange >= -10 AND qqq52WChange < 0 | +5 | Slight Loss (Best Buy Opportunity) |
| qqq52WChange >= 0 AND qqq52WChange < 10 | +3 | Slight Gain (Early Recovery) |
| qqq52WChange >= -20 AND qqq52WChange < -10 | +1 | Moderate Loss |
| qqq52WChange < -20 | 0 | Severe Loss |
| qqq52WChange >= 10 AND qqq52WChange < 20 | 0 | Good Yearly Gain |
| *(default)* | -3 | Strong Yearly Gain (Extended) |

### Q7: MACD Score

- **Points range:** -3 to 3
- **Inputs:** qqqMACDHistogram, qqqMACDHistogramPrev
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| qqqMACDHistogram <= 0 AND _macdNearZero == true | 0 | Sell - Weakest (Near Zero) |
| qqqMACDHistogram <= 0 | +3 | Sell signal (contrarian buy) |
| qqqMACDHistogram > 0 AND _macdNearZero == true | 0 | Buy - Weakest (Near Zero) |
| qqqMACDHistogram > 0 | -3 | Buy signal (contrarian extended) |
| *(default)* | 0 | Neutral |

### Q8: QQQ Range Position

- **Points range:** -2 to 3
- **Inputs:** qqqPrice, qqq52WHigh, qqq52WLow
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| _rangePosition < 0.1 | +3 | Near support (bounce potential) |
| _rangePosition < 0.45 | +1 | Lower half |
| _rangePosition < 0.55 | 0 | Near middle |
| _rangePosition < 0.9 | +1 | Upper half |
| *(default)* | -2 | Near resistance (extended) |

### Q9: GDP Growth Proxy (SPY 3M)

- **Points range:** -3 to 3
- **Inputs:** spy3mChange
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| spy3mChange < 0 | +3 | Contraction (Buy Opportunity) |
| spy3mChange <= 6 | 0 | Moderate/Stalling |
| *(default)* | -3 | Strong Growth (Extended) |

### Q10: Unemployment Trend (XLI)

- **Points range:** -1 to 2
- **Inputs:** xli1mChange
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| xli1mChange < -2 | +2 | Industrial Weakness (Buy Opportunity) |
| xli1mChange <= 3 | 0 | Stable |
| *(default)* | -1 | Industrial Expansion (Extended) |

### Q11: International Markets (EFA vs SPY)

- **Points range:** -2 to 2
- **Inputs:** efa1mChange, spy1mChange
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| _efaDiff >= 1 AND _efaDiff <= 3 | +2 | Slight Outperformance |
| _efaDiff > 3 | +1 | Global Strength |
| _efaDiff >= -1 | 0 | Neutral |
| _efaDiff >= -3 | -1 | EFA lags SPY |
| *(default)* | -2 | US Isolation |

### Q12: Commodities (XLE + GLD)

- **Points range:** -2 to 2
- **Inputs:** xle1mChange, gld1mChange
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| xle1mChange < -3 AND gld1mChange > 3 | +2 | Risk-Off/Fear (Buy Opportunity) |
| xle1mChange < -3 | +1 | Mild Risk-Off |
| xle1mChange > 3 AND gld1mChange < -3 | -2 | Risk-On (Extended) |
| xle1mChange > 3 | -1 | Mild Risk-On |
| *(default)* | 0 | Mixed/Stable |

### Q13: Small-Cap Breadth (IWM vs QQQ)

- **Points range:** -1 to 1
- **Inputs:** iwm1mChange, qqq1mChange
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| _iwmDiff > 3 | +1 | High Risk Appetite |
| _iwmDiff < -3 | -1 | Flight to Safety |
| *(default)* | 0 | Neutral |

### Q14: Sector Rotation (XLY vs XLP)

- **Points range:** -1 to 1
- **Inputs:** xly1mChange, xlp1mChange
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| _xlyDiff < -3 | +1 | Defensive Rotation (Buy Opportunity) |
| _xlyDiff > 3 | -1 | Consumer Confidence (Extended) |
| *(default)* | 0 | Neutral |

### Q15: Equal-Weight Breadth (RSP vs SPY)

- **Points range:** -1 to 1
- **Inputs:** rsp1mChange, spy1mChange
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| _rspDiff < -0.5 | +1 | Narrow Rally (Reversal Risk) |
| _rspDiff > 2 | -1 | Broad Participation (Extended) |
| *(default)* | 0 | Neutral |

### Q16: Credit Spreads (HYG)

- **Points range:** 0 to 2
- **Inputs:** hyg1mChange
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| hyg1mChange < -1 | +2 | Credit Stress (Buy Opportunity) |
| *(default)* | 0 | No Signal |

### Q17: Dollar Index (UUP)

- **Points range:** -2 to 2
- **Inputs:** uup1mChange
- **Missing data:** zero

| Conditions | Pts | Interpretation |
|---|---|---|
| uup1mChange < -2 | +2 | Dollar Weakening (Bullish) |
| uup1mChange < 0 | +1 | Mild Weakening |
| uup1mChange <= 1 | 0 | Neutral |
| uup1mChange <= 2 | -1 | Mild Strengthening |
| *(default)* | -2 | Dollar Spiking (Headwind) |

---

## Action Signals — V18

### Stock Rules

| ID | Pri | Signal | Holding Signal | Conditions | Color |
|---|---|---|---|---|---|
| R1 | 30 | Buy in Good Market | Hold and Add if Tier Allows | saScore >= 80 | t-green |
| R2 | 31 | Buy if Stable | Hold and Add if Tier Allows | saScore >= 75 | t-teal |
| R3 | 32 | Consider Buying | Monitor | saScore >= 70 | t-blue |
| R4 | 33 | Monitor | Sell Low Quality. Add tight Stops | saScore >= 60 | t-yellow |
| FB | 99 | Watch | Sell All | (always) | t-blue |

### Market Rules

| ID | Pri | Signal | Holding Signal | Conditions | Color |
|---|---|---|---|---|---|
| M-V1 | 1 | VIX ≥ 30 — Great Buying Opportunity | Hold and Add (SA ≥ 70 only) | vix >= 30 | t-green |
| M-V2 | 2 | VIX ≥ 25 — Buying Opportunity | Hold and Add (SA ≥ 70 only) | vix >= 25 | t-teal |
| M-MC1 | 3 | Very Weak Market — Sell All | Exit All Positions | mcScore < 20 | t-red |
| M-MC2 | 4 | Slow Market — Be Careful | Reduce Risk | mcScore >= 20 AND mcScore < 40 | t-yellow |
| M-MC3 | 5 | Over-Heated Market — Only Great Stocks | Exit Risky Positions | mcScore >= 81 | t-blue |
| M-R1 | 6 | Heated Market — Buy Carefully | Hold with Stops | mcScore > 60 AND mcScore <= 80 | t-orange |
| M-R2 | 7 | Normal Market — Buy Quality Stocks | Hold Quality Stocks | mcScore >= 40 AND mcScore <= 60 | t-green |
| M-FB | 99 | Market — Unknown | Hold | (always) | t-gray |

### Tiers & Position Sizing

| Tier | SA | Condition | Max Position | Size Label | Color |
|---|---|---|---|---|---|
| T1 | ≥ 65 | Profitable + Market Cap > $50B | $100,000 | Large | t-green |
| T2 | ≥ 65 | Profitable + Market Cap > $2B | $50,000 | Medium | t-blue-2 |
| T3 | ≥ 65 | Market Cap > $100M + (Growth OR Small Profitable) | $20,000 | Small | t-yellow |
| SELL | N/A | Does not qualify | $0 | — | t-red |

### Entry Confirmation Signals (3-Day Rule)

Day 0 = trigger, Day 1 = hold, Day 2 = act.

| ID | Label | Holding Label | Threshold | Color |
|---|---|---|---|---|
| CE-80 | 3D of 80+ | Continue Holding | SA crosses above 80, held 3 days | t-green |
| CE-75 | 3D of 75+ | Continue Holding | SA crosses above 75, held 3 days | t-teal |
| CE-70 | 3D of 70+ | Monitor | SA crosses above 70, held 3 days | t-blue |

### Conviction Levels (V19 — 4 Conditions)

Levels based on any combination of all 4 conditions (A, B, C, D).

| Level | Label | Conditions Met | Badge | Sort Priority |
|---|---|---|---|---|
| C1 | Prime | All 4 (A + B + C + D) | 🔥 | 1st |
| C2 | Strong | Any 3 of 4 | ⭐ | 2nd |
| C3 | Valid | Any 2 of 4 | ✅ | 3rd |
| Others | Weak/Monitor | Any 1 or none | ⚠️ | 4th |

#### Conviction Conditions

| Icon | ID | Condition | Requirement |
|---|---|---|---|
| 🔒 | A | SA Hold | SA ≥ 80 held for 5+ consecutive days |
| 📊 | B | MC Zone | MC between 30 and 80 |
| 📈 | C | QQQ Trend | QQQ positive on 5D and 1M price change |
| 🎯 | D | Combo Signal | Q3 ≥ 4pts AND Q11 ≥ 3pts AND Q12 ≥ 4pts |

#### Conviction % — SA 80+

| Level | MC 50+ | MC 40–49 | MC <40 |
|---|---|---|---|
| C1 | 90% | 80% | 70% |
| C2 | 90% | 75% | 65% |
| C3 | 75% | 70% | 65% |
| Others | 70% | 70% | 60% |

#### Conviction % — SA 75–79

Flat 60% assigned regardless of MC group or conviction level.

#### VIX Adjustment (applied after base %)

| Condition | Adjustment | Cap |
|---|---|---|
| VIX 25–29 | +3% | 95% |
| VIX ≥ 30 | +5% | 95% |

SA < 75: No conviction % shown.

#### MC Gate

| MC Range | Effect |
|---|---|
| < 20 | Hard override — no buy signals, show "Sell All" |
| 20–49 | Conviction capped at C3 (Valid) |
| 50–80 | Normal signal flow |
| ≥ 81 | Alert badge 🔴 "Overheated Market — Only Great Stocks" |

#### Hard Blocks

| ID | Target | Effect |
|---|---|---|
| CRYPTO-BLOCK | CONST-CRYPTO symbols | 🚫 No buy signal regardless of SA score |
| HEALTH-BLOCK | CONST-BIOTECH sectors (SA ≥ 75) | 🚫 No buy signal in 80+ and 75-79 zones |
| BM-ALERT | Basic Materials 3rd+ stock | ⚠️ Sector Concentration badge (alert only) |

### Q20 — Sector Preference (-5 to +2 pts)

Priority: 1) Crypto → -4, 2) Metals → 0, 3) Clean Energy → +2, 4) Oil & Gas → -2, 5) Sector rules.

| Points | Group | Sectors / Symbols |
|---|---|---|
| +2 | Preferred | Technology, Financial Services, Industrials, Communication Services, Consumer Cyclical |
| +2 | Clean Energy override | ENPH, FSLR, NEXT |
| +1 | Neutral | Consumer Staples, Consumer Discretionary, Utilities, Transportation, Construction |
| 0 | Default | All others |
| 0 | Metals override | CONST-METALS symbols |
| -2 | Oil & Gas | See symbols list |
| -4 | Crypto-related | CONST-CRYPTO symbols |
| -5 | Weak | Healthcare (non-biotech), Basic Materials (non-metals) |

---

## Formulas, Constants & Reference

### Formulas & Caps

| ID | Name | Formula / Value | Source |
|---|---|---|---|
| NORM-SA | SA Normalization | ((raw + 43) / 113) × 100 — min: -43, max: 70 | sa-config |
| NORM-MC | MC Normalization | ((raw + 40) / 92) × 100 — min: -40, max: 52 | mc-config |
| PP-1 | Combined Penalty Cap | Q16 + Q17 combined max -4 | sa-config postProcessing |
| CAP-CYCLICAL | Cyclical Sector Cap | Q1–Q3 capped at 4 pts for Basic Materials/Energy/Mining unless Q21 breakout (>100%) | sa-config contextFlags |
| BM-ALERT | Basic Materials Concentration | 3rd+ Basic Materials stock shows ⚠️ "Sector Concentration" badge (alert only) | action-signal-engine |

### Forward Performance Periods

| ID | Period | Applies To | Description |
|---|---|---|---|
| FWD-STOCK-1 | 5D | Stock Matrix | 5 trading days forward return |
| FWD-STOCK-2 | 10D | Stock Matrix | 10 trading days forward return |
| FWD-STOCK-3 | 1M | Stock Matrix | ~21 trading days forward return |
| FWD-STOCK-4 | 2M | Stock Matrix | ~42 trading days forward return |
| FWD-STOCK-5 | 3M | Stock Matrix | ~63 trading days forward return |
| FWD-MC-1 | 5D | MC Matrix | 5 trading days forward return |
| FWD-MC-2 | 10D | MC Matrix | 10 trading days forward return |
| FWD-MC-3 | 1M | MC Matrix | ~21 trading days forward return |
| FWD-MC-4 | 2M | MC Matrix | ~42 trading days forward return |
| FWD-MC-5 | 3M | MC Matrix | ~63 trading days forward return |

### Constants & Lists

| ID | Name | Count | Values |
|---|---|---|---|
| CONST-CRYPTO | Crypto Symbols | 21 | IREN, MARA, CLSK, RIOT, BITF, WULF, HUT, CIFR, COIN, MSTR, CORZ, BTBT, HIVE, BTDR, GRDI, MIGI, BTCS, ARBK, DGHI, MGTI, SOS |
| CONST-METALS | Metals & Mining Symbols | 25 | NEM, GFI, KGC, AU, HMY, CDE, HL, NGD, CGAU, AEM, GOLD, AG, WPM, FNV, RGLD, OR, PAAS, EXK, FSM, MAG, SVM, FCX, TECK, HBM, SBSW |
| CONST-PREFERRED | Preferred Sectors | 4 | Technology, Financial Services, Industrials, Communication Services |
| CONST-NEUTRAL | Neutral Sectors | 5 | Consumer Staples, Consumer Discretionary, Utilities, Transportation, Construction |
| CONST-BIOTECH | Biotech Sectors | 6 | Healthcare, Biotechnology, Medical Devices, Drug Manufacturers, Medical, Pharma |
| CONST-US | US Countries | 3 | USA, US, UNITED STATES |
| CONST-DEVELOPED | Developed Countries | 28 | Canada, UK, United Kingdom, Netherlands, Germany, France, Japan, Australia, Taiwan, South Korea, Switzerland, Ireland, Israel, Sweden, Norway, Denmark, Finland, Spain, Italy, Singapore, New Zealand, Hong Kong, Belgium, Austria, UAE, United Arab Emirates, Saudi Arabia, Qatar |
| CONST-EM | China/EM Countries | 20 | China, Brazil, South Africa, India, Mexico, Indonesia, Turkey, Thailand, Philippines, Vietnam, Colombia, Chile, Peru, Egypt, Nigeria, Pakistan, Bangladesh, Malaysia, Argentina, Russia |
| CONST-CLEAN-ENERGY | Clean Energy Symbols | 3 | ENPH, FSLR, NEXT |
| CONST-OIL-GAS | Oil & Gas Symbols | 48 | XOM, CVX, COP, EOG, FANG, APA, MUR, CRC, CRGY, VET, KOS, MGY, NOG, CHRD, AR, CNX, BKV, HPK, WTI, TALO, GFR, BATL, VLO, MPC, DK, CVI, KMI, WMB, ET, EPD, TRGP, WES, CQP, LNG, FLNG, GLNG, DLNG, GEL, BKR, AROC, TPL, NFG, EQNR, E, WDS, BTE, VIST, VG |
| CONST-WEAK | Weak Sectors | 2 | Healthcare, Basic Materials |
