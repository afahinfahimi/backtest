# SA Merged — Stock Analysis Scoring System
All questions from V1 (original 31) plus candidate additions. V1 questions marked **(V1)**. Point ranges preserved exactly. Similarity tags added where applicable. Use this document to evaluate and select best questions per category.

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

**Q32: Net Income Growth** *(similar to Q1, Q2, Q3 — different metric)*
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

**Q33: Revenue Acceleration** *(similar to Q1 — focuses on trend direction only)*
-2 to 2 pts | Inputs: quarterlyRevenues | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| _revenueAccel > 0 | +2 | Accelerating |
| _revenueAccel < 0 | -2 | Decelerating |
| default | 0 | Flat / Insufficient Data |

---

**Q34: Gross Margin Trend** *(unique — direction of gross margin change)*
0 to 2 pts | Inputs: currentGrossMargin, priorGrossMargin | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| currentGrossMargin > priorGrossMargin | +2 | Improving |
| default | 0 | No Change |

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

**Q18: Financial Strength (V1)** *(composite — similar to Q4, Q13, Q10 combined)*
0 to 3 pts | Inputs: netProfitMargin, roe, debtToEquity | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| netProfitMargin >= 20 AND roe >= 20 AND debtToEquity < 0.5 | +3 | Excellent |
| netProfitMargin >= 10 AND roe >= 10 AND debtToEquity < 1.5 | +2 | Good |
| netProfitMargin >= 0 AND roe >= 5 AND debtToEquity < 3 | +1 | Moderate |
| default | 0 | Weak |

---

**Q35: Gross Margin %** *(similar to Q4 — different margin level)*
0 to 5 pts | Inputs: grossMarginPct | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| grossMarginPct >= 60 | +5 | Exceptional |
| grossMarginPct >= 40 | +3 | Good |
| default | 0 | Low |

---

**Q36: Operating Margin %** *(similar to Q4 — different margin level)*
0 to 5 pts | Inputs: operatingMarginPct | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| operatingMarginPct >= 25 | +5 | Exceptional |
| operatingMarginPct >= 15 | +3 | Good |
| default | 0 | Low |

---

**Q37: Return on Invested Capital (ROIC)** *(similar to Q13, Q14 — different metric)*
0 to 5 pts | Inputs: roicTTM | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| roicTTM >= 0.20 | +5 | Exceptional |
| roicTTM >= 0.14 | +4 | Strong |
| roicTTM >= 0.08 | +3 | Good |
| roicTTM >= 0.04 | +2 | Moderate |
| default | 0 | Low |

---

**Q38: Free Cash Flow Yield** *(similar to Q3 — different angle: yield vs growth)*
-4 to 4 pts | Inputs: freeCashFlowYield | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| freeCashFlowYield >= 8 | +4 | Strong |
| freeCashFlowYield >= 4 | +2 | Good |
| freeCashFlowYield >= 0 | 0 | Neutral |
| freeCashFlowYield >= -5 | -2 | Weak |
| default | -4 | Burning Cash |

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

**Q39: Interest Coverage Ratio** *(unique — not in V1)*
0 to 5 pts | Inputs: interestCoverageTTM | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| interestCoverageTTM >= 10 | +5 | Excellent |
| interestCoverageTTM >= 5 | +4 | Strong |
| interestCoverageTTM >= 3 | +3 | Good |
| interestCoverageTTM >= 1.5 | +1 | Adequate |
| default | 0 | At Risk |

---

**Q40: Current Ratio** *(unique — not in V1)*
0 to 5 pts | Inputs: currentRatioTTM | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| currentRatioTTM >= 2 | +5 | Excellent |
| currentRatioTTM >= 1.5 | +4 | Strong |
| currentRatioTTM >= 1 | +3 | Adequate |
| currentRatioTTM >= 0.7 | +1 | Weak |
| default | 0 | At Risk |

---

## Category 4: Valuation

**Q23: High P/E Momentum Trap (V1)**
-4 to 0 pts | Inputs: peRatio, change10d | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| peRatio > 50 AND change10d < -5 | -4 | High P/E momentum trap |
| default | 0 | No trap |

---

**Q41: P/E TTM Full Range** *(similar to Q23 — broader scoring, rewards low P/E too)* ⚠️ range -5 to +2
-5 to 2 pts | Inputs: peRatio | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| peRatio > 0 AND peRatio <= 50 | +2 | Attractive |
| peRatio > 50 AND peRatio <= 100 | +1 | Elevated |
| peRatio > 100 AND peRatio <= 200 | 0 | High |
| peRatio > 200 AND peRatio <= 300 | -1 | Very High |
| peRatio > 300 AND peRatio <= 500 | -3 | Extreme |
| peRatio > 500 | -5 | Absurd |
| peRatio <= 0 (unprofitable) | -1 | Unprofitable |

---

**Q42: Valuation Sanity (P/E < 30)** *(similar to Q23 — rewards low P/E only, no penalty)*
0 to 3 pts | Inputs: peTTM | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| peTTM < 30 | +3 | Reasonable Valuation |
| default | 0 | Stretched |

---

**Q43: Price-to-Sales Ratio** *(similar to Q23 — penalty only for extreme P/S)*
-1 to 0 pts | Inputs: priceToSales | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| priceToSales > 50 | -1 | Extreme P/S |
| default | 0 | Normal |

---

**Q44: EV/EBITDA** *(unique — not in V1)*
0 to 5 pts | Inputs: evToEbitdaTTM | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| evToEbitdaTTM < 8 | +5 | Exceptional Value |
| evToEbitdaTTM < 12 | +4 | Good Value |
| evToEbitdaTTM < 18 | +3 | Fair |
| evToEbitdaTTM < 30 | +1 | Stretched |
| default | 0 | Expensive |

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

**Q11: Momentum Magnitude (V1)**
0 to 3 pts | Inputs: change52w, change3m | Missing: midpoint
| Condition | Pts | Interpretation |
|---|---|---|
| _momSum > 150 | +3 | Exceptional momentum |
| _momSum > 100 | +2 | Strong momentum |
| _momSum > 50 | +1 | Moderate momentum |
| default | 0 | Weak momentum |

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
| Condition | Pts | Interpretation |
|---|---|---|
| change10d > 20 AND change1m < 10 | -1 | Spike Risk |
| change52w > 0 AND change3m > 0 AND change1m > 0 AND change52w > change3m AND change3m > change1m AND change1m > change10d | +2 | Smooth momentum |
| change3m > 0 AND _accelCheck > change52w | +1 | Accelerating |
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
-6 to 0 pts | Inputs: dailyChanges | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| _worstDrop3d <= -15 | -6 | Critical drop (15%+) |
| _worstDrop3d <= -10 | -2 | Severe drop (10%+) |
| _worstDrop3d <= -7 | -1 | Caution drop (7%+) |
| _cumulative5d <= -10 | -1 | Cumulative 5-day decline > 10% |
| default | 0 | No sudden drops |

---

**Q31: Trend Deterioration (V1)**
-3 to 0 pts | Inputs: hasLowerHighsLowerLows | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| hasLowerHighsLowerLows == true | -3 | Lower highs AND lower lows |
| default | 0 | No structural downtrend |

---

**Q45: Price Change 1D** *(similar to Q5, Q6 — shorter timeframe)*
0 to 5 pts | Inputs: priceChange1D | Missing: zero ⚠️ max +5 vs V1 scale
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

**Q47: 52-Week Proximity** *(unique — proximity to 52W high/low)*
-2 to 2 pts | Inputs: price, yearHigh, yearLow | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| _pctFromHigh <= 5 | +2 | Near 52W High |
| _pctFromLow <= 5 | -2 | Near 52W Low |
| default | 0 | Mid Range |

---

**Q48: Volume Surge** *(similar to Q7 — directional, near 52W high/low context)*
-4 to 4 pts | Inputs: volume, avgVolume20d, change1d, price, yearHigh, yearLow | Missing: zero ⚠️ wider range
| Condition | Pts | Interpretation |
|---|---|---|
| _volumeRatio >= 2 AND change1d > 0 AND _pctFromHigh <= 5 | +4 | Volume Surge Near 52W High |
| _volumeRatio >= 2 AND change1d > 0 | +2 | Volume Surge Up |
| _volumeRatio >= 2 AND change1d < 0 AND _pctFromLow <= 5 | -4 | Volume Surge Near 52W Low |
| _volumeRatio >= 2 AND change1d < 0 | -2 | Volume Surge Down |
| default | 0 | Normal Volume |

---

## Category 6: Relative Strength

**Q29: Sector Performance vs Peers (V1)**
-1 to 1 pts | Inputs: change1m, spyChange1m | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| _spyDiff1m > 10 | +1 | Outperforming SPY |
| _spyDiff1m < -10 | -1 | Underperforming SPY |
| default | 0 | In line with SPY |

---

**Q30: 5-Day Relative Strength (V1)**
-3 to 3 pts | Inputs: change5d, qqqChange5d | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| change5d > 0 AND qqqChange5d < 0 | +3 | Up while market down |
| _alpha5d >= 5 | +2 | Strong alpha |
| _alpha5d >= 0 | +1 | Slight alpha |
| _alpha5d >= -5 | 0 | Slight underperformance |
| change5d < 0 AND qqqChange5d > 0 | -3 | Down while market up |
| default | -2 | Significant underperformance |

---

**Q49: 3-Month Relative Strength vs S&P 500** *(similar to Q29, Q30 — longer window)* ⚠️ max +7
0 to 7 pts | Inputs: change3m, spyChange3m | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| _rs3m >= 15 | +7 | Exceptional Alpha |
| _rs3m >= 5 | +4 | Strong Alpha |
| _rs3m >= 0 | +2 | Slight Alpha |
| default | 0 | Underperforming |

---

**Q50: Relative Strength Divergence (10-Day)** *(similar to Q19 — market-relative version)*
-5 to 0 pts | Inputs: change10d, spyChange10d | Missing: zero ⚠️ max penalty -5
| Condition | Pts | Interpretation |
|---|---|---|
| _stockRS10d < -5 AND spyChange10d > 1 | -5 | Diverging badly vs rising market |
| default | 0 | No divergence |

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

**Q51: Avg Daily Dollar Volume (20D)** *(similar to Q7 — dollar-based, more granular)* ⚠️ max +5
0 to 5 pts | Inputs: avgDailyDollarVolume20D | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| avgDailyDollarVolume20D >= 100M | +5 | Very High |
| avgDailyDollarVolume20D >= 20M | +4 | High |
| avgDailyDollarVolume20D >= 5M | +3 | Moderate |
| avgDailyDollarVolume20D >= 1M | +1 | Low |
| default | 0 | Illiquid |

---

**Q52: Float Turnover** *(similar to Q7 — float relative to volume)*
0 to 2 pts | Inputs: floatShares, avgVolume20d | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| _floatTurnover >= 2 | +2 | High Turnover |
| default | 0 | Low Turnover |

---

**Q53: Market Cap Score** *(unique — V1 only uses marketCap as a buffer in Q16)*
0 to 5 pts | Inputs: marketCap | Missing: zero ⚠️ max +5
| Condition | Pts | Interpretation |
|---|---|---|
| marketCap >= 50B | +5 | Mega Cap |
| marketCap >= 10B | +4 | Large Cap |
| marketCap >= 2B | +3 | Mid Cap |
| marketCap >= 300M | +2 | Small Cap |
| default | 0 | Micro Cap |

---

## Category 8: Volatility

**Q54: ATR 20D % of Price** *(unique — not in V1)*
0 to 5 pts | Inputs: atr20DPercent | Missing: zero ⚠️ max +5
*(Lower ATR = higher score — rewards low volatility)*
| Condition | Pts | Interpretation |
|---|---|---|
| atr20DPercent < 1.5% | +5 | Very Low Volatility |
| atr20DPercent < 2.5% | +4 | Low |
| atr20DPercent < 4% | +3 | Moderate |
| atr20DPercent < 6% | +1 | High |
| default | 0 | Very High |

---

**Q55: Realized Volatility 20D (Annualized)** *(unique — not in V1)*
0 to 5 pts | Inputs: realizedVol20D | Missing: zero ⚠️ max +5
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
| default | 0 | No coverage |

---

**Q56: Insider Buying** *(unique — not in V1)*
-2 to 2 pts | Inputs: netInsiderBuying | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| netInsiderBuying > 0 | +2 | Net Buying |
| netInsiderBuying < 0 | -2 | Net Selling |
| default | 0 | Neutral / No Data |

---

**Q57: Institutional Accumulation** *(similar to Q8 — tracks change, not just presence)*
-2 to 2 pts | Inputs: currentInstOwnership, priorInstOwnership | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| _instOwnershipChange >= 1 | +2 | Accumulating |
| _instOwnershipChange <= -1 | -2 | Distribution |
| default | 0 | Stable / No Data |

---

## Category 10: Earnings & Events

**Q58: Earnings Surprise** *(unique — not in V1)*
-2 to 2 pts | Inputs: actualEps, estimatedEps | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| actualEps > estimatedEps | +2 | Beat |
| actualEps < estimatedEps | -2 | Miss |
| default | 0 | In Line / No Data |

---

**Q59: Post-Earnings Reaction** *(similar to Earnings Surprise — price reaction vs estimate beat)*
-4 to 4 pts | Inputs: lastEarningsDate, historicalPrices | Missing: zero ⚠️ wider range
| Condition | Pts | Interpretation |
|---|---|---|
| _postEarningsGap >= 5 | +4 | Strong Gap Up |
| _postEarningsGap > 0 | +2 | Slight Gap Up |
| _postEarningsGap >= -5 | 0 | Slight Down |
| default | -4 | Gap Down |

---

**Q60: Earnings Guidance Performance** *(unique — not in V1)*
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

**Q61: Major Catalyst Bonus** *(unique — not in V1)*
0 to 3 pts | Inputs: majorCatalyst | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| majorCatalyst == true | +3 | Large contract, M&A, FDA approval, or index inclusion |
| default | 0 | No catalyst |

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
| _symbol in [cryptoSymbols] | -4 | Crypto-related |
| sector in [preferredSectors] | +2 | Preferred sector |
| sector in [neutralSectors] | +1 | Neutral sector |
| _symbol in [goldMiningSymbols] | 0 | Gold mining |
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

**Q62: SEC / Fraud Investigation Penalty** *(unique — not in V1)*
-5 to 0 pts | Inputs: secInvestigation | Missing: zero ⚠️ max penalty -5
| Condition | Pts | Interpretation |
|---|---|---|
| secInvestigation == true | -5 | Active SEC investigation, fraud, or restatement |
| default | 0 | Clean |

---

## Summary

| Category | V1 Questions | Added Questions | Total |
|---|---|---|---|
| Growth | 4 | 3 | 7 |
| Profitability | 4 | 4 | 8 |
| Balance Sheet | 3 | 2 | 5 |
| Valuation | 1 | 4 | 5 |
| Technical/Momentum | 9 | 5 | 14 |
| Relative Strength | 2 | 2 | 4 |
| Volume & Liquidity | 1 | 3 | 4 |
| Volatility | 0 | 2 | 2 |
| Ownership & Coverage | 1 | 2 | 3 |
| Earnings & Events | 0 | 4 | 4 |
| Risk & Penalty | 5 | 1 | 6 |
| **Total** | **31** | **32** | **63** |

⚠️ = Point range differs from typical V1 scale (max 6). Review before normalizing.
