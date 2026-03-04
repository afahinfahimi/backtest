# SA Master — Stock Analysis Scoring System
All questions Q1–Q81. V1 questions marked **(V1)**. Questions Q63+ are candidate additions from subsequent versions.

---

## Category 1: Growth

**Q1: Sales Growth (V1)**
0 to 6 pts | Inputs: annualRevenueGrowth, quarterlyRevenueGrowth | Missing: midpoint
Cap: isCyclicalNoBreakout → max 4
| Condition | Pts | Interpretation |
|---|---|---|
| annualRevenueGrowth >= 50 AND quarterlyRevenueGrowth > annualRevenueGrowth | +6 | Accelerating Exceptional |
| annualRevenueGrowth >= 50 AND quarterlyRevenueGrowth > 0 | +5 | Steady Exceptional |
| annualRevenueGrowth >= 20 AND < 50 AND quarterlyRevenueGrowth > annualRevenueGrowth | +5 | Accelerating Strong |
| annualRevenueGrowth >= 20 AND < 50 AND quarterlyRevenueGrowth > 0 | +4 | Steady Strong |
| annualRevenueGrowth >= 1 AND < 20 AND quarterlyRevenueGrowth > 0 | +2 | Growing |
| annualRevenueGrowth >= 0 AND quarterlyRevenueGrowth <= 0 | +1 | Stalling |
| annualRevenueGrowth < 0 AND quarterlyRevenueGrowth > 0 | +1 | Recovering |
| default | 0 | Declining |

---

**Q2: Operating Income Growth (V1)**
0 to 6 pts | Inputs: annualOperatingIncomeGrowth, quarterlyOperatingIncomeGrowth | Missing: midpoint
Cap: isCyclicalNoBreakout → max 4
| Condition | Pts | Interpretation |
|---|---|---|
| annualOperatingIncomeGrowth >= 50 AND quarterlyOperatingIncomeGrowth > annualOperatingIncomeGrowth | +6 | Accelerating Exceptional |
| annualOperatingIncomeGrowth >= 50 AND quarterlyOperatingIncomeGrowth > 0 | +5 | Steady Exceptional |
| annualOperatingIncomeGrowth >= 20 AND < 50 AND quarterlyOperatingIncomeGrowth > annualOperatingIncomeGrowth | +5 | Accelerating Strong |
| annualOperatingIncomeGrowth >= 20 AND < 50 AND quarterlyOperatingIncomeGrowth > 0 | +4 | Steady Strong |
| annualOperatingIncomeGrowth >= 1 AND < 20 AND quarterlyOperatingIncomeGrowth > 0 | +2 | Growing |
| annualOperatingIncomeGrowth >= 0 AND quarterlyOperatingIncomeGrowth <= 0 | +1 | Stalling |
| annualOperatingIncomeGrowth < 0 AND quarterlyOperatingIncomeGrowth > 0 | +1 | Recovering |
| default | 0 | Declining |

---

**Q3: Cash Flow Growth (V1)**
0 to 6 pts | Inputs: annualCashFlowGrowth, quarterlyCashFlowGrowth | Missing: midpoint
Cap: isCyclicalNoBreakout → max 4
| Condition | Pts | Interpretation |
|---|---|---|
| annualCashFlowGrowth >= 50 AND quarterlyCashFlowGrowth > annualCashFlowGrowth | +6 | Accelerating Exceptional |
| annualCashFlowGrowth >= 50 AND quarterlyCashFlowGrowth > 0 | +5 | Steady Exceptional |
| annualCashFlowGrowth >= 20 AND < 50 AND quarterlyCashFlowGrowth > annualCashFlowGrowth | +5 | Accelerating Strong |
| annualCashFlowGrowth >= 20 AND < 50 AND quarterlyCashFlowGrowth > 0 | +4 | Steady Strong |
| annualCashFlowGrowth >= 1 AND < 20 AND quarterlyCashFlowGrowth > 0 | +2 | Growing |
| annualCashFlowGrowth >= 0 AND quarterlyCashFlowGrowth <= 0 | +1 | Stalling |
| annualCashFlowGrowth < 0 AND quarterlyCashFlowGrowth > 0 | +1 | Recovering |
| default | 0 | Declining |

---

**Q12: EPS Growth Prior Year (V1)**
0 to 4 pts | Inputs: epsGrowthPriorYear | Missing: midpoint
| Condition | Pts | Interpretation |
|---|---|---|
| epsGrowthPriorYear >= 100 | +4 | Exceptional |
| epsGrowthPriorYear >= 50 | +3 | Strong |
| epsGrowthPriorYear >= 25 | +2 | Good |
| epsGrowthPriorYear > 0 | +1 | Positive |
| default | 0 | Negative/Flat |

---

**Q32: Net Income Growth** *(similar to Q1–Q3)*
0 to 6 pts | Inputs: annualNetIncomeGrowth, quarterlyNetIncomeGrowth | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| annualNetIncomeGrowth >= 50 AND quarterlyNetIncomeGrowth > annualNetIncomeGrowth | +6 | Accelerating Exceptional |
| annualNetIncomeGrowth >= 50 AND quarterlyNetIncomeGrowth > 0 | +5 | Steady Exceptional |
| annualNetIncomeGrowth >= 20 AND quarterlyNetIncomeGrowth > annualNetIncomeGrowth | +5 | Accelerating Strong |
| annualNetIncomeGrowth >= 20 AND quarterlyNetIncomeGrowth > 0 | +4 | Steady Strong |
| annualNetIncomeGrowth >= 1 AND quarterlyNetIncomeGrowth > 0 | +2 | Growing |
| default | 0 | Flat/Declining |

---

**Q33: Revenue Acceleration** *(similar to Q1 — trend direction only)*
-2 to 2 pts | Inputs: quarterlyRevenues | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| _revenueAccel > 0 | +2 | Accelerating |
| _revenueAccel < 0 | -2 | Decelerating |
| default | 0 | Flat / Insufficient Data |

---

**Q34: Gross Margin Trend** *(direction of gross margin change)*
0 to 2 pts | Inputs: currentGrossMargin, priorGrossMargin | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| currentGrossMargin > priorGrossMargin | +2 | Improving |
| default | 0 | No Change |

---

**Q55: Net Income Growth** *(full tiered version — similar to Q32)*
0 to 6 pts | Inputs: annualNetIncomeGrowth, quarterlyNetIncomeGrowth | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| annualNetIncomeGrowth >= 50 AND quarterlyNetIncomeGrowth > annualNetIncomeGrowth | +6 | Accelerating Exceptional |
| annualNetIncomeGrowth >= 50 AND quarterlyNetIncomeGrowth > 0 | +5 | Steady Exceptional |
| annualNetIncomeGrowth >= 20 AND quarterlyNetIncomeGrowth > annualNetIncomeGrowth | +5 | Accelerating Strong |
| annualNetIncomeGrowth >= 20 AND quarterlyNetIncomeGrowth > 0 | +4 | Steady Strong |
| annualNetIncomeGrowth >= 1 AND quarterlyNetIncomeGrowth > 0 | +2 | Growing |
| default | 0 | Flat/Declining |

---

**Q64: Weighted Momentum** *(similar to Q11 — weighted formula)*
0 to 3 pts | Inputs: change52w, change3m | Missing: zero
_weightedMom = (0.7 × change52w) + (0.3 × change3m)
| Condition | Pts | Interpretation |
|---|---|---|
| _weightedMom > 80 | +3 | Exceptional |
| _weightedMom >= 40 | +2 | Strong |
| _weightedMom >= 0 | +1 | Moderate |
| default | 0 | Weak/Negative |

---

## Category 2: Profitability

**Q4: Net Profit Margin (V1)**
0 to 5 pts | Inputs: netProfitMargin | Missing: midpoint
| Condition | Pts | Interpretation |
|---|---|---|
| netProfitMargin >= 30 | +5 | Exceptional |
| netProfitMargin >= 20 | +4 | Strong |
| netProfitMargin >= 15 | +3 | Good |
| netProfitMargin >= 10 | +2 | Moderate |
| netProfitMargin >= 5 | +1 | Low |
| default | 0 | None |

---

**Q13: Return on Equity (V1)**
0 to 2 pts | Inputs: roe | Missing: midpoint
| Condition | Pts | Interpretation |
|---|---|---|
| roe >= 20 | +2 | Excellent |
| roe >= 10 | +1 | Good |
| default | 0 | Low |

---

**Q14: Return on Assets (V1)**
0 to 3 pts | Inputs: roa | Missing: midpoint
| Condition | Pts | Interpretation |
|---|---|---|
| roa >= 15 | +3 | Excellent |
| roa >= 10 | +2 | Good |
| roa >= 5 | +1 | Moderate |
| default | 0 | Low |

---

**Q18: Financial Strength (V1)** *(composite)*
0 to 3 pts | Inputs: netProfitMargin, roe, debtToEquity | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| netProfitMargin >= 20 AND roe >= 20 AND debtToEquity < 0.5 | +3 | Excellent |
| netProfitMargin >= 10 AND roe >= 10 AND debtToEquity < 1.5 | +2 | Good |
| netProfitMargin >= 0 AND roe >= 5 AND debtToEquity < 3 | +1 | Moderate |
| default | 0 | Weak |

---

**Q35: Gross Margin %** *(similar to Q4)*
0 to 5 pts | Inputs: grossMarginPct | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| grossMarginPct >= 60 | +5 | Exceptional |
| grossMarginPct >= 40 | +3 | Good |
| default | 0 | Low |

---

**Q36: Operating Margin %** *(similar to Q4)*
0 to 5 pts | Inputs: operatingMarginPct | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| operatingMarginPct >= 25 | +5 | Exceptional |
| operatingMarginPct >= 15 | +3 | Good |
| default | 0 | Low |

---

**Q37: Return on Invested Capital (ROIC)**
0 to 5 pts | Inputs: roicTTM | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| roicTTM >= 0.20 | +5 | Exceptional |
| roicTTM >= 0.14 | +4 | Strong |
| roicTTM >= 0.08 | +3 | Good |
| roicTTM >= 0.04 | +2 | Moderate |
| default | 0 | Low |

---

**Q38: Free Cash Flow Yield**
-4 to 4 pts | Inputs: freeCashFlowYield | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| freeCashFlowYield >= 8 | +4 | Strong |
| freeCashFlowYield >= 4 | +2 | Good |
| freeCashFlowYield >= 0 | 0 | Neutral |
| freeCashFlowYield >= -5 | -2 | Weak |
| default | -4 | Burning Cash |

---

**Q43: Gross Margin %** *(simplified version — similar to Q35)*
0 to 5 pts | Inputs: grossMarginPct | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| grossMarginPct >= 60 | +5 | Exceptional |
| grossMarginPct >= 40 | +3 | Good |
| default | 0 | Low |

---

**Q44: Operating Margin %** *(simplified version — similar to Q36)*
0 to 5 pts | Inputs: operatingMarginPct | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| operatingMarginPct >= 25 | +5 | Exceptional |
| operatingMarginPct >= 15 | +3 | Good |
| default | 0 | Low |

---

**Q73: Profitability & Growth Check** *(unprofitable gets pass if growing fast)*
-5 to 0 pts | Inputs: netProfitMargin, annualRevenueGrowth | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| netProfitMargin >= 0 | 0 | Profitable |
| netProfitMargin < 0 AND annualRevenueGrowth >= 25 | 0 | Fast growth offsets loss |
| default | -5 | Unprofitable and slow growth |

---

**Q74: Operational Efficiency (Revenue per Employee)**
0 to 2 pts | Inputs: quarterlyRevenue, employeeCount | Missing: zero
_revPerEmployee = (quarterlyRevenue × 4) / employeeCount
| Condition | Pts | Interpretation |
|---|---|---|
| _revPerEmployee > 1000000 | +2 | Highly efficient |
| _revPerEmployee >= 500000 | +1 | Efficient |
| default | 0 | Labor intensive |

---

## Category 3: Balance Sheet & Financial Health

**Q10: Debt-to-Equity Ratio (V1)**
-3 to 3 pts | Inputs: debtToEquity | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| debtToEquity < 0 | -3 | Negative equity |
| debtToEquity < 0.5 | +3 | Excellent |
| debtToEquity < 1 | +2 | Good |
| debtToEquity < 2 | +1 | Moderate |
| default | 0 | High debt |

---

**Q16: Cash Burn Risk (V1)**
-3 to 0 pts | Inputs: netProfitMargin, operatingCashFlowQuarterly, marketCap | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| netProfitMargin >= 0 | 0 | Profitable |
| operatingCashFlowQuarterly >= 0 | 0 | Positive cash flow |
| marketCap >= 10000000000 | 0 | Large cap buffer |
| default | -3 | Cash burn risk |
Post-processing: Q16+Q17 max -4

---

**Q17: Deterioration Risk (V1)**
-3 to 0 pts | Inputs: revenueQoQ, operatingIncomeQoQ, cashFlowQoQ | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| revenueQoQ < 0 AND operatingIncomeQoQ < 0 AND cashFlowQoQ < 0 | -3 | All metrics declining QoQ |
| default | 0 | No deterioration |
Post-processing: Q16+Q17 max -4

---

**Q39: Interest Coverage Ratio**
0 to 5 pts | Inputs: interestCoverageTTM | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| interestCoverageTTM >= 10 | +5 | Excellent |
| interestCoverageTTM >= 5 | +4 | Strong |
| interestCoverageTTM >= 3 | +3 | Good |
| interestCoverageTTM >= 1.5 | +1 | Adequate |
| default | 0 | At Risk |

---

**Q40: Current Ratio**
0 to 5 pts | Inputs: currentRatioTTM | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| currentRatioTTM >= 2 | +5 | Excellent |
| currentRatioTTM >= 1.5 | +4 | Strong |
| currentRatioTTM >= 1 | +3 | Adequate |
| currentRatioTTM >= 0.7 | +1 | Weak |
| default | 0 | At Risk |

---

**Q45: Return on Invested Capital (ROIC)** *(same as Q37 — duplicate)*
0 to 5 pts | Inputs: roicTTM | Missing: zero
See Q37.

---

**Q46: Interest Coverage Ratio** *(same as Q39 — duplicate)*
0 to 5 pts | Inputs: interestCoverageTTM | Missing: zero
See Q39.

---

**Q47: Current Ratio** *(same as Q40 — duplicate)*
0 to 5 pts | Inputs: currentRatioTTM | Missing: zero
See Q40.

---

**Q68: Balance Sheet Quality** *(AI/qualitative)*
-1 to 1 pts | Inputs: qualitative assessment | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| Net cash, no debt concerns | +1 | Fortress balance sheet |
| Neutral | 0 | No signal |
| Hidden leverage, off-balance-sheet risk, covenant concerns | -1 | Hidden risk |

---

## Category 4: Valuation

**Q23: High P/E Momentum Trap (V1)**
-4 to 0 pts | Inputs: peRatio, change10d | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| peRatio > 50 AND change10d < -5 | -4 | High P/E momentum trap |
| default | 0 | No trap |

---

**Q41: P/E TTM Full Range** *(broader scoring — rewards low P/E too)*
-5 to 2 pts | Inputs: peRatio | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| peRatio > 0 AND peRatio <= 50 | +2 | Attractive |
| peRatio > 50 AND peRatio <= 100 | +1 | Elevated |
| peRatio > 100 AND peRatio <= 200 | 0 | High |
| peRatio > 200 AND peRatio <= 300 | -1 | Very High |
| peRatio > 300 AND peRatio <= 500 | -3 | Extreme |
| peRatio > 500 | -5 | Absurd |
| peRatio <= 0 | -1 | Unprofitable |

---

**Q42: Valuation Sanity (P/E < 30)** *(rewards low P/E only)*
0 to 3 pts | Inputs: peTTM | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| peTTM < 30 | +3 | Reasonable Valuation |
| default | 0 | Stretched |

---

**Q43: Price-to-Sales Ratio** *(penalty only for extreme P/S)*
-1 to 0 pts | Inputs: priceToSales | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| priceToSales > 50 | -1 | Extreme P/S |
| default | 0 | Normal |

---

**Q44: EV/EBITDA**
0 to 5 pts | Inputs: evToEbitdaTTM | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| evToEbitdaTTM < 8 | +5 | Exceptional Value |
| evToEbitdaTTM < 12 | +4 | Good Value |
| evToEbitdaTTM < 18 | +3 | Fair |
| evToEbitdaTTM < 30 | +1 | Stretched |
| default | 0 | Expensive |

---

**Q48: EV/EBITDA** *(same as Q44 — duplicate)*
See Q44.

---

**Q54: Valuation Sanity (P/E < 30)** *(same as Q42 — duplicate)*
See Q42.

---

**Q56: P/E TTM Full Range** *(same as Q41 — duplicate)*
See Q41.

---

**Q69: Valuation vs Peers** *(AI/qualitative)*
-1 to 1 pts | Inputs: qualitative assessment | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| Trading at discount to comparable peers | +1 | Undervalued vs peers |
| Neutral | 0 | In line |
| Extreme premium without justification | -1 | Overvalued vs peers |

---

## Category 5: Technical / Price Momentum

**Q5: 1-Month Price Change (V1)**
0 to 4 pts | Inputs: change1m | Missing: midpoint
| Condition | Pts | Interpretation |
|---|---|---|
| change1m >= 20 | +4 | Strong momentum |
| change1m >= 10 | +3 | Good momentum |
| change1m >= 5 | +2 | Positive |
| change1m > 0 | +1 | Slight positive |
| default | 0 | Negative/Flat |

---

**Q6: 10-Day Price Change (V1)**
0 to 3 pts | Inputs: change10d | Missing: midpoint
| Condition | Pts | Interpretation |
|---|---|---|
| change10d >= 15 | +3 | Strong |
| change10d >= 10 | +2 | Good |
| change10d >= 5 | +1 | Positive |
| default | 0 | Weak |

---

**Q9: Price vs Moving Averages (V1)**
0 to 4 pts | Inputs: price, sma20, sma50 | Missing: midpoint
| Condition | Pts | Interpretation |
|---|---|---|
| price > sma20 AND price > sma50 | +4 | Above both 20D & 50D |
| price > sma50 | +3 | Above 50D only |
| price > sma20 | +2 | Above 20D only |
| default | 0 | Below both |

---

**Q11: Momentum Magnitude (V1)** ⭐ BEST PREDICTOR
0 to 3 pts | Inputs: change52w, change3m | Missing: midpoint
_momSum = change52w + change3m
| Condition | Pts | Backtest Win Rate |
|---|---|---|
| _momSum > 150 | +3 | 73% |
| _momSum > 100 | +2 | 63% |
| _momSum > 50 | +1 | 55% |
| default | 0 | 47% |

---

**Q19: Momentum Divergence Penalty (V1)**
-3 to 0 pts | Inputs: change52w, change3m, change1m, change10d | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| change52w > 0 AND change3m < 0 AND change1m < 0 AND change10d < 0 | -3 | Momentum divergence |
| default | 0 | No divergence |

---

**Q21: %B Position / Bollinger Bands (V1)**
0 to 4 pts | Inputs: bollingerPercentB | Missing: midpoint
| Condition | Pts | Interpretation |
|---|---|---|
| bollingerPercentB > 100 | +4 | Breakout |
| bollingerPercentB > 95 | +3 | Near top |
| bollingerPercentB >= 80 | +2 | Upper zone |
| bollingerPercentB >= 20 | +1 | Mid-range |
| default | 0 | Buy zone |

---

**Q22: Momentum Quality (V1)**
-1 to 2 pts | Inputs: change52w, change3m, change1m, change10d | Missing: zero
*(Evaluate in order — stop at first match)*
| Condition | Pts | Interpretation |
|---|---|---|
| change10d > 20 AND change1m < 10 | -1 | Spike Risk |
| change52w > 0 AND change3m > 0 AND change1m > 0 AND change52w > change3m AND change3m > change1m AND change1m > change10d | +2 | Smooth momentum |
| change3m > 0 AND (change3m × 4) > change52w | +1 | Accelerating |
| default | 0 | Other |

---

**Q25: Sustained Downtrend (V1)**
-3 to 0 pts | Inputs: change1d, change5d, change1m | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| change1d < 0 AND change5d < 0 AND change1m < 0 | -3 | Sustained downtrend |
| default | 0 | No downtrend |

---

**Q26: Sudden Drop / Slide (V1)**
-6 to 0 pts | Inputs: dailyChanges last 5 days | Missing: zero
*(Highest tier only — no stacking)*
| Condition | Pts | Interpretation |
|---|---|---|
| _worstDrop3d <= -15 | -6 | Critical (15%+) |
| _worstDrop3d <= -10 | -2 | Severe (10%+) |
| _worstDrop3d <= -7 OR _cumulative5d <= -10 | -1 | Caution (7%+ or -10% cumulative) |
| default | 0 | Normal |

---

**Q31: Trend Deterioration / Lower Lows & Lower Highs (V1)**
-3 to 0 pts | Inputs: dailyOHLC last 30 days | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| hasLowerHighsLowerLows == true | -3 | Structural downtrend |
| default | 0 | No structural downtrend |

---

**Q45: Price Change 1D** *(similar to Q5/Q6 — 1-day timeframe)*
0 to 5 pts | Inputs: priceChange1D | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| priceChange1D >= 3% | +5 | Strong Up |
| priceChange1D >= 1% | +3 | Positive |
| priceChange1D >= -1% | +2 | Flat |
| priceChange1D >= -3% | +1 | Slight Down |
| default | 0 | Down |

---

**Q46: MA Stack Alignment (Price > 20MA > 50MA)** *(similar to Q9 — adds MA ordering)*
0 to 4 pts | Inputs: price, sma20, sma50 | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| price > sma20 AND sma20 > sma50 | +4 | Full Stack Aligned |
| price > sma20 AND sma20 <= sma50 | +2 | Price above 20 only |
| price <= sma20 AND price > sma50 | +1 | Price above 50 only |
| default | 0 | No alignment |

---

**Q47: 52-Week Proximity**
-2 to 2 pts | Inputs: price, yearHigh, yearLow | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| _pctFromHigh <= 5 | +2 | Near 52W High |
| _pctFromLow <= 5 | -2 | Near 52W Low |
| default | 0 | Mid Range |

---

**Q48: Volume Surge** *(contextual — direction + proximity to high/low)*
-4 to 4 pts | Inputs: volume, avgVolume20d, change1d, price, yearHigh, yearLow | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| _volumeRatio >= 2 AND change1d > 0 AND _pctFromHigh <= 5 | +4 | Volume Surge Near 52W High |
| _volumeRatio >= 2 AND change1d > 0 | +2 | Volume Surge Up |
| _volumeRatio >= 2 AND change1d < 0 AND _pctFromLow <= 5 | -4 | Volume Surge Near 52W Low |
| _volumeRatio >= 2 AND change1d < 0 | -2 | Volume Surge Down |
| default | 0 | Normal Volume |

---

**Q53: Price Change 1D** *(same as Q45 — duplicate)*
See Q45.

---

**Q59: MA Stack Alignment** *(same as Q46 — duplicate)*
See Q46.

---

**Q65: Overextension & Trend Breakdown**
-6 to 0 pts | Inputs: change52w, peRatio, netProfitMargin, price, sma50, currentScore | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| change52w > 100 AND (peRatio > 50 OR netProfitMargin < 10) | -4 | Extended run with weak fundamentals |
| price < sma50 AND currentScore >= 60 | -2 | High score but below 50MA — trap risk |
| default | 0 | No overextension |

---

**Q76: Sustained Downtrend** *(same logic as Q25 — from later version)*
-3 to 0 pts | Inputs: change1d, change5d, change1m | Missing: zero
See Q25.

---

**Q77: Sudden Drop / Slide** *(same logic as Q26 — from later version; penalty scale differs)*
-10 to 0 pts | Inputs: last 5 daily close prices | Missing: zero
*(Highest tier only — no stacking)*
| Condition | Pts | Interpretation |
|---|---|---|
| Any single day drop >= 15% within last 3 days | -10 | Catastrophic |
| Any single day drop >= 10% within last 3 days | -5 | Severe |
| Any single day drop >= 7% OR cumulative 5D <= -10% | -3 | Caution |
| default | 0 | Normal |

---

**Q80: 5-Day Relative Strength (Alpha)**
-3 to 3 pts | Inputs: change5d, qqq5dChange | Missing: zero
_alpha = change5d - qqq5dChange
*(Evaluate in order — stop at first match)*
| Condition | Pts | Interpretation |
|---|---|---|
| change5d > 0 AND qqq5dChange < 0 | +3 | True alpha — stock up, market down |
| _alpha >= 5 | +2 | Beating market by 5%+ |
| _alpha >= 0 | +1 | Beating market |
| _alpha >= -5 | 0 | Slightly lagging |
| change5d < 0 AND qqq5dChange > 0 | -3 | Stock down while market up |
| default | -2 | Badly lagging market |

*Backtested: Up/Market Down = 82.1% win rate. Down/Market Up = 47.8% win rate.*

---

**Q81: Trend Deterioration (Lower Lows & Lower Highs)** ⚠️ INCOMPLETE
0 to -3 pts | Inputs: Daily OHLC last 30 trading days | Missing: zero
*(Scoring logic not yet defined — needs full specification)*

---

## Category 6: Relative Strength

**Q29: Sector Performance vs Peers (V1)**
-1 to 1 pts | Inputs: change1m, sectorAvgChange1m | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| change1m > sectorAvgChange1m + 10 | +1 | Outperforming sector |
| change1m < sectorAvgChange1m - 10 | -1 | Underperforming sector |
| default | 0 | In line |

---

**Q30: 5-Day Relative Strength (V1)**
-3 to 3 pts | Inputs: change5d, qqqChange5d | Missing: zero
*(Same as Q80 — V1 version)*
See Q80.

---

**Q49: 3-Month Relative Strength vs S&P 500** *(longer window)*
0 to 7 pts | Inputs: change3m, spyChange3m | Missing: zero
_rs3m = change3m - spyChange3m
| Condition | Pts | Interpretation |
|---|---|---|
| _rs3m >= 15 | +7 | Exceptional Alpha |
| _rs3m >= 5 | +4 | Strong Alpha |
| _rs3m >= 0 | +2 | Slight Alpha |
| default | 0 | Underperforming |

---

**Q50: Relative Strength Divergence (10-Day)**
-5 to 0 pts | Inputs: change10d, spyChange10d | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| _stockRS10d < -5 AND spyChange10d > 1 | -5 | Diverging badly vs rising market |
| default | 0 | No divergence |

---

**Q57: 3-Month Relative Strength vs S&P 500** *(same as Q49 — duplicate)*
See Q49.

---

**Q58: Relative Strength Divergence (10-Day)** *(same as Q50 — duplicate)*
See Q50.

---

**Q79: Sector Performance vs Peers** *(same as Q29 — from later version)*
See Q29.

---

## Category 7: Volume & Liquidity

**Q7: 20-Day Average Volume (V1)**
0 to 3 pts | Inputs: avgVolume20d | Missing: midpoint
| Condition | Pts | Interpretation |
|---|---|---|
| avgVolume20d >= 1000000 | +3 | High liquidity |
| avgVolume20d >= 500000 | +2 | Good liquidity |
| avgVolume20d >= 200000 | +1 | Moderate |
| default | 0 | Low liquidity |

---

**Q36: Volume Surge** *(same as Q48 — duplicate)*
See Q48.

---

**Q41: Float Turnover**
0 to 2 pts | Inputs: floatShares, avgVolume20d | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| _floatTurnover >= 2 | +2 | High Turnover |
| default | 0 | Low Turnover |

---

**Q50: Avg Daily Dollar Volume (20D)**
0 to 5 pts | Inputs: avgDailyDollarVolume20D | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| avgDailyDollarVolume20D >= 100M | +5 | Very High |
| avgDailyDollarVolume20D >= 20M | +4 | High |
| avgDailyDollarVolume20D >= 5M | +3 | Moderate |
| avgDailyDollarVolume20D >= 1M | +1 | Low |
| default | 0 | Illiquid |

---

**Q52: Float Turnover** *(same as Q41 — duplicate)*
See Q41.

---

**Q53: Market Cap Score**
0 to 5 pts | Inputs: marketCap | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| marketCap >= 50B | +5 | Mega Cap |
| marketCap >= 10B | +4 | Large Cap |
| marketCap >= 2B | +3 | Mid Cap |
| marketCap >= 300M | +2 | Small Cap |
| default | 0 | Micro Cap |

---

**Q71: Relative Volume** *(ratio-based version of Q7)*
0 to 3 pts | Inputs: volume, avgVolume20d | Missing: zero
_volumeRatio = volume / avgVolume20d
| Condition | Pts | Interpretation |
|---|---|---|
| _volumeRatio > 1.5 | +3 | High relative volume |
| _volumeRatio >= 1.1 | +2 | Above average |
| _volumeRatio >= 0.8 | +1 | Normal |
| default | 0 | Low volume |

---

## Category 8: Volatility

**Q51: ATR 20D % of Price**
0 to 5 pts | Inputs: atr20DPercent | Missing: zero
*(Lower ATR = higher score)*
| Condition | Pts | Interpretation |
|---|---|---|
| atr20DPercent < 1.5% | +5 | Very Low Volatility |
| atr20DPercent < 2.5% | +4 | Low |
| atr20DPercent < 4% | +3 | Moderate |
| atr20DPercent < 6% | +1 | High |
| default | 0 | Very High |

---

**Q52: Realized Volatility 20D (Annualized)**
0 to 5 pts | Inputs: realizedVol20D | Missing: zero
*(Lower vol = higher score)*
| Condition | Pts | Interpretation |
|---|---|---|
| realizedVol20D < 0.20 | +5 | Very Low |
| realizedVol20D < 0.30 | +4 | Low |
| realizedVol20D < 0.45 | +3 | Moderate |
| realizedVol20D < 0.60 | +1 | High |
| default | 0 | Very High |

---

## Category 9: Ownership & Coverage

**Q8: Ownership & Coverage (V1)**
0 to 2 pts | Inputs: institutionalOwnership, analystCount | Missing: custom | additive
| Condition | Pts | Interpretation |
|---|---|---|
| institutionalOwnership > 0 | +1 | Institutional ownership |
| analystCount > 0 | +1 | Analyst coverage |

---

**Q35: Insider Buying**
-2 to 2 pts | Inputs: netInsiderBuying | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| netInsiderBuying > 0 | +2 | Net Buying |
| netInsiderBuying < 0 | -2 | Net Selling |
| default | 0 | Neutral / No Data |

---

**Q39: Institutional Accumulation** *(tracks change, not just presence)*
-2 to 2 pts | Inputs: currentInstOwnership, priorInstOwnership | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| _instOwnershipChange >= 1 | +2 | Accumulating |
| _instOwnershipChange <= -1 | -2 | Distribution |
| default | 0 | Stable / No Data |

---

**Q56: Insider Buying** *(same as Q35 — duplicate)*
See Q35.

---

**Q57: Institutional Accumulation** *(same as Q39 — duplicate)*
See Q39.

---

**Q63: Has Options**
0 to 1 pts | Inputs: hasOptions | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| hasOptions == true | +1 | Options available |
| default | 0 | No options |

---

**Q72: Insider Ownership Point** *(additive to Q8)*
0 to 1 pts | Inputs: insiderOwnership | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| insiderOwnership > 0 | +1 | Has insider ownership |
| default | 0 | No insider ownership |

---

## Category 10: Earnings & Events

**Q33: Earnings Surprise**
-2 to 2 pts | Inputs: actualEps, estimatedEps | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| actualEps > estimatedEps | +2 | Beat |
| actualEps < estimatedEps | -2 | Miss |
| default | 0 | In Line / No Data |

---

**Q42: Post-Earnings Reaction**
-4 to 4 pts | Inputs: lastEarningsDate, historicalPrices | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| _postEarningsGap >= 5 | +4 | Strong Gap Up |
| _postEarningsGap > 0 | +2 | Slight Gap Up |
| _postEarningsGap >= -5 | 0 | Slight Down |
| default | -4 | Gap Down |

---

**Q58: Earnings Surprise** *(same as Q33 — duplicate)*
See Q33.

---

**Q59: Post-Earnings Reaction** *(same as Q42 — duplicate)*
See Q42.

---

**Q60: Earnings Guidance Performance**
-3 to 2 pts | Inputs: earningsGuidance | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| earningsGuidance == "raised" | +2 | Raised guidance |
| earningsGuidance == "positive" | +1 | Positive language |
| earningsGuidance == "maintained" | 0 | Maintained |
| earningsGuidance == "cautious" | -1 | Cautious tone |
| earningsGuidance == "lowered" | -2 | Lowered guidance |
| earningsGuidance == "withdrawn" | -3 | Withdrawn guidance |

---

**Q61: Major Catalyst Bonus**
0 to 3 pts | Inputs: majorCatalyst | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| majorCatalyst == true | +3 | Large contract, M&A, FDA approval, or index inclusion |
| default | 0 | No catalyst |

---

**Q75: Event-Driven Adjustment** *(AI/research required)*
-2 to 2 pts | Inputs: recent news | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| Major catalyst (earnings beat, FDA, acquisition, product launch) | +1 to +2 | Positive catalyst |
| After-hours/pre-market positive move | +1 | Near-term momentum |
| Turnaround inflection point | +1 | Recovery signal |
| Restructuring/layoffs (efficiency-driven) | +1 | Positive efficiency |
| Restructuring/layoffs (distress-driven) | -1 | Negative signal |
| Imminent negative event (lockup expiry, debt maturity) | -1 to -2 | Near-term risk |
| default | 0 | No notable events |

---

## Category 11: Risk & Penalty

**Q15: Country (V1)**
-2 to 1 pts | Inputs: country | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| country in [usCountries] | +1 | USA |
| country in [developedCountries] | 0 | Developed |
| country in [chinaEmCountries] | -2 | China/Emerging Market |
| default | 0 | Other |

---

**Q20: Sector Preference (V1)**
-4 to 2 pts | Inputs: sector | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| symbol in [cryptoSymbols] | -4 | Crypto-related |
| sector in [preferredSectors] | +2 | Preferred (Tech, Finance, Aerospace, Business Services) |
| sector in [neutralSectors] | +1 | Neutral (Consumer, Medical, Industrial, etc.) |
| symbol in [goldMiningSymbols] | 0 | Gold mining |
| default | 0 | Neutral |

---

**Q24: Biotech Binary Event Burn (V1)**
-3 to 0 pts | Inputs: sector, change10d | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| sector in [biotechSectors] AND change10d > 15 | -3 | Biotech spike risk |
| default | 0 | N/A |

---

**Q27: Short Interest Risk (V1)**
-1 to 0 pts | Inputs: shortPercentFloat | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| shortPercentFloat > 20 | -1 | High short interest |
| default | 0 | Normal |

---

**Q28: Low Float Risk (V1)**
-1 to 0 pts | Inputs: floatShares | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| floatShares < 20000000 | -1 | Low float risk |
| default | 0 | Normal float |

---

**Q62: SEC / Fraud Investigation Penalty**
-5 to 0 pts | Inputs: secInvestigation | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| secInvestigation == true | -5 | Active SEC investigation, fraud, or restatement |
| default | 0 | Clean |

---

**Q78: Short Interest Risk** *(tiered version of Q27)*
-2 to 0 pts | Inputs: shortPercentFloat | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| shortPercentFloat > 30 | -2 | High short interest |
| shortPercentFloat > 20 | -1 | Elevated short interest |
| default | 0 | Normal |

---

## Category 12: AI / Qualitative

**Q66: Competitive Moat** *(AI/qualitative — requires research)*
-1 to 1 pts | Inputs: qualitative assessment | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| Dominant market position, pricing power, high switching costs | +1 | Strong moat |
| Neutral | 0 | No clear moat signal |
| No moat, commoditized, or facing disruption | -1 | Moat risk |

---

**Q67: Growth Sustainability** *(AI/qualitative — requires research)*
-1 to 1 pts | Inputs: qualitative assessment | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| Recurring revenue, secular trend, expanding TAM | +1 | Durable growth |
| Neutral | 0 | Unclear |
| One-time boost, hype-driven, or decelerating without catalyst | -1 | Unsustainable |

---

**Q70: Execution & Management** *(AI/qualitative — requires research)*
-1 to 1 pts | Inputs: qualitative assessment | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| Proven track record, aligned incentives, strong insider buying | +1 | Strong management |
| Neutral | 0 | No signal |
| SEC issues, high turnover, controversy, meme/squeeze target | -1 | Management risk |

---

## Summary

| Category | V1 Qs | Added Qs | Total |
|---|---|---|---|
| Growth | 4 | 5 | 9 |
| Profitability | 4 | 6 | 10 |
| Balance Sheet | 3 | 5 | 8 |
| Valuation | 1 | 5 | 6 |
| Technical/Momentum | 9 | 10 | 19 |
| Relative Strength | 2 | 3 | 5 |
| Volume & Liquidity | 1 | 4 | 5 |
| Volatility | 0 | 2 | 2 |
| Ownership & Coverage | 1 | 4 | 5 |
| Earnings & Events | 0 | 5 | 5 |
| Risk & Penalty | 5 | 2 | 7 |
| AI/Qualitative | 0 | 3 | 3 |
| **Total** | **31** | **50** | **81** |

⚠️ Q81 is incomplete — scoring logic not yet defined.
Note: Some questions are duplicates across versions (same logic, different numbering). Duplicates are noted with "See QXX."
