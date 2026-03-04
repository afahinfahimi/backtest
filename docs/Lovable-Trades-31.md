SA Engine — V17 (31 Questions)
Normalization: -42 to 70
· Post-processing: Q16+Q17 max -4
Q1: Sales Growth
0 to 6 pts
Inputs: annualRevenueGrowth, quarterlyRevenueGrowth·Missing data: midpoint
Cap: isCyclicalNoBreakout → max 4
Conditions	Pts	Interpretation
annualRevenueGrowth >= 50 AND quarterlyRevenueGrowth > annualRevenueGrowth	+6	Accelerating Exceptional
annualRevenueGrowth >= 50 AND quarterlyRevenueGrowth > 0	+5	Steady Exceptional
annualRevenueGrowth >= 20 AND annualRevenueGrowth < 50 AND quarterlyRevenueGrowth > annualRevenueGrowth	+5	Accelerating Strong
annualRevenueGrowth >= 20 AND annualRevenueGrowth < 50 AND quarterlyRevenueGrowth > 0	+4	Steady Strong
annualRevenueGrowth >= 1 AND annualRevenueGrowth < 20 AND quarterlyRevenueGrowth > 0	+2	Growing
annualRevenueGrowth >= 0 AND quarterlyRevenueGrowth <= 0	+1	Stalling
annualRevenueGrowth < 0 AND quarterlyRevenueGrowth > 0	+1	Recovering
default	0	Declining
Q2: Operating Income Growth
0 to 6 pts
Inputs: annualOperatingIncomeGrowth, quarterlyOperatingIncomeGrowth·Missing data: midpoint
Cap: isCyclicalNoBreakout → max 4
Conditions	Pts	Interpretation
annualOperatingIncomeGrowth >= 50 AND quarterlyOperatingIncomeGrowth > annualOperatingIncomeGrowth	+6	Accelerating Exceptional
annualOperatingIncomeGrowth >= 50 AND quarterlyOperatingIncomeGrowth > 0	+5	Steady Exceptional
annualOperatingIncomeGrowth >= 20 AND annualOperatingIncomeGrowth < 50 AND quarterlyOperatingIncomeGrowth > annualOperatingIncomeGrowth	+5	Accelerating Strong
annualOperatingIncomeGrowth >= 20 AND annualOperatingIncomeGrowth < 50 AND quarterlyOperatingIncomeGrowth > 0	+4	Steady Strong
annualOperatingIncomeGrowth >= 1 AND annualOperatingIncomeGrowth < 20 AND quarterlyOperatingIncomeGrowth > 0	+2	Growing
annualOperatingIncomeGrowth >= 0 AND quarterlyOperatingIncomeGrowth <= 0	+1	Stalling
annualOperatingIncomeGrowth < 0 AND quarterlyOperatingIncomeGrowth > 0	+1	Recovering
default	0	Declining
Q3: Cash Flow Growth
0 to 6 pts
Inputs: annualCashFlowGrowth, quarterlyCashFlowGrowth·Missing data: midpoint
Cap: isCyclicalNoBreakout → max 4
Conditions	Pts	Interpretation
annualCashFlowGrowth >= 50 AND quarterlyCashFlowGrowth > annualCashFlowGrowth	+6	Accelerating Exceptional
annualCashFlowGrowth >= 50 AND quarterlyCashFlowGrowth > 0	+5	Steady Exceptional
annualCashFlowGrowth >= 20 AND annualCashFlowGrowth < 50 AND quarterlyCashFlowGrowth > annualCashFlowGrowth	+5	Accelerating Strong
annualCashFlowGrowth >= 20 AND annualCashFlowGrowth < 50 AND quarterlyCashFlowGrowth > 0	+4	Steady Strong
annualCashFlowGrowth >= 1 AND annualCashFlowGrowth < 20 AND quarterlyCashFlowGrowth > 0	+2	Growing
annualCashFlowGrowth >= 0 AND quarterlyCashFlowGrowth <= 0	+1	Stalling
annualCashFlowGrowth < 0 AND quarterlyCashFlowGrowth > 0	+1	Recovering
default	0	Declining
Q4: Net Profit Margin
0 to 5 pts
Inputs: netProfitMargin·Missing data: midpoint
Conditions	Pts	Interpretation
netProfitMargin >= 30	+5	Exceptional
netProfitMargin >= 20	+4	Strong
netProfitMargin >= 15	+3	Good
netProfitMargin >= 10	+2	Moderate
netProfitMargin >= 5	+1	Low
default	0	None
Q5: 1-Month Price Change
0 to 4 pts
Inputs: change1m·Missing data: midpoint
Conditions	Pts	Interpretation
change1m >= 20	+4	Strong momentum
change1m >= 10	+3	Good momentum
change1m >= 5	+2	Positive
change1m > 0	+1	Slight positive
default	0	Negative/Flat
Q6: 10-Day Price Change
0 to 3 pts
Inputs: change10d·Missing data: midpoint
Conditions	Pts	Interpretation
change10d >= 15	+3	Strong
change10d >= 10	+2	Good
change10d >= 5	+1	Positive
default	0	Weak
Q7: 20-Day Average Volume
0 to 3 pts
Inputs: avgVolume20d·Missing data: midpoint
Conditions	Pts	Interpretation
avgVolume20d >= 1000000	+3	High liquidity
avgVolume20d >= 500000	+2	Good liquidity
avgVolume20d >= 200000	+1	Moderate
default	0	Low liquidity
Q8: Ownership & Coverage
0 to 2 pts
additive
Inputs: institutionalOwnership, analystCount·Missing data: custom
Conditions	Pts	Interpretation
institutionalOwnership > 0	+1	Institutional ownership
analystCount > 0	+1	Analyst coverage
default	0	No coverage
Q9: Price vs Moving Averages
0 to 4 pts
Inputs: price, sma20, sma50·Missing data: midpoint
Conditions	Pts	Interpretation
price > sma20 AND price > sma50	+4	Above both 20D & 50D
price > sma50	+3	Above 50D only
price > sma20	+2	Above 20D only
default	0	Below both
Q10: Debt-to-Equity Ratio
-3 to 3 pts
Inputs: debtToEquity·Missing data: zero
Conditions	Pts	Interpretation
debtToEquity < 0	-3	Negative equity
debtToEquity < 0.5	+3	Excellent
debtToEquity < 1	+2	Good
debtToEquity < 2	+1	Moderate
default	0	High debt
Q11: Momentum Magnitude
0 to 3 pts
Inputs: change52w, change3m·Missing data: midpoint
Conditions	Pts	Interpretation
_momSum > 150	+3	Exceptional momentum
_momSum > 100	+2	Strong momentum
_momSum > 50	+1	Moderate momentum
default	0	Weak momentum
Q12: EPS Growth Prior Year
0 to 4 pts
Inputs: epsGrowthPriorYear·Missing data: midpoint
Conditions	Pts	Interpretation
epsGrowthPriorYear >= 100	+4	Exceptional
epsGrowthPriorYear >= 50	+3	Strong
epsGrowthPriorYear >= 25	+2	Good
epsGrowthPriorYear > 0	+1	Positive
default	0	Negative/Flat
Q13: Return on Equity
0 to 2 pts
Inputs: roe·Missing data: midpoint
Conditions	Pts	Interpretation
roe >= 20	+2	Excellent
roe >= 10	+1	Good
default	0	Low
Q14: Return on Assets
0 to 3 pts
Inputs: roa·Missing data: midpoint
Conditions	Pts	Interpretation
roa >= 15	+3	Excellent
roa >= 10	+2	Good
roa >= 5	+1	Moderate
default	0	Low
Q15: Country
-2 to 1 pts
Inputs: country·Missing data: zero
Conditions	Pts	Interpretation
country in [usCountries]	+1	USA
country in [developedCountries]	0	Developed
country in [chinaEmCountries]	-2	China/Emerging Market
default	0	Other
Q16: Cash Burn Risk
-3 to 0 pts
Inputs: netProfitMargin·Missing data: zero
Conditions	Pts	Interpretation
netProfitMargin >= 0	0	Profitable
operatingCashFlowQuarterly >= 0	0	Positive cash flow
marketCap >= 10000000000	0	Large cap buffer
default	-3	Cash burn risk
Q17: Deterioration Risk
-3 to 0 pts
Inputs: revenueQoQ, operatingIncomeQoQ, cashFlowQoQ·Missing data: zero
Conditions	Pts	Interpretation
revenueQoQ < 0 AND operatingIncomeQoQ < 0 AND cashFlowQoQ < 0	-3	All metrics declining QoQ
default	0	No deterioration
Q18: Financial Strength
0 to 3 pts
Inputs: netProfitMargin, roe, debtToEquity·Missing data: zero
Conditions	Pts	Interpretation
netProfitMargin >= 20 AND roe >= 20 AND debtToEquity < 0.5	+3	Excellent
netProfitMargin >= 10 AND roe >= 10 AND debtToEquity < 1.5	+2	Good
netProfitMargin >= 0 AND roe >= 5 AND debtToEquity < 3	+1	Moderate
default	0	Weak
Q19: Momentum Divergence Penalty
-3 to 0 pts
Inputs: change52w, change3m, change1m, change10d·Missing data: zero
Conditions	Pts	Interpretation
change52w > 0 AND change3m < 0 AND change1m < 0 AND change10d < 0	-3	Momentum divergence
default	0	No divergence
Q20: Sector Preference
-4 to 2 pts
Inputs: sector·Missing data: zero
Conditions	Pts	Interpretation
_symbol in [cryptoSymbols]	-4	Crypto-related
sector in [preferredSectors]	+2	Preferred sector
sector in [neutralSectors]	+1	Neutral sector
_symbol in [goldMiningSymbols]	0	Gold mining
default	0	Neutral
Q21: %B Position (Bollinger Bands)
0 to 4 pts
Inputs: bollingerPercentB·Missing data: midpoint
Conditions	Pts	Interpretation
bollingerPercentB > 100	+4	Breakout
bollingerPercentB > 95	+3	Near top
bollingerPercentB >= 80	+2	Upper zone
bollingerPercentB >= 20	+1	Mid-range
default	0	Buy zone
Q22: Momentum Quality
-1 to 2 pts
Inputs: change52w, change3m, change1m, change10d·Missing data: zero
Conditions	Pts	Interpretation
change10d > 20 AND change1m < 10	-1	Spike Risk
change52w > 0 AND change3m > 0 AND change1m > 0 AND change52w > change3m AND change3m > change1m AND change1m > change10d	+2	Smooth momentum
change3m > 0 AND _accelCheck > change52w	+1	Accelerating
default	0	Other
Q23: High P/E Momentum Trap
-4 to 0 pts
Inputs: peRatio, change10d·Missing data: zero
Conditions	Pts	Interpretation
peRatio > 50 AND change10d < -5	-4	High P/E momentum trap
default	0	No trap
Q24: Biotech Binary Event Burn
-3 to 0 pts
Inputs: sector, change10d·Missing data: zero
Conditions	Pts	Interpretation
sector in [biotechSectors] AND change10d > 15	-3	Biotech spike risk
default	0	N/A
Q25: Sustained Downtrend
-3 to 0 pts
Inputs: change1d, change5d, change1m·Missing data: zero
Conditions	Pts	Interpretation
change1d < 0 AND change5d < 0 AND change1m < 0	-3	Sustained downtrend
default	0	No downtrend
Q26: Sudden Drop / Slide
-6 to 0 pts
Inputs: dailyChanges·Missing data: zero
Conditions	Pts	Interpretation
_worstDrop3d <= -15	-6	Critical drop (15%+)
_worstDrop3d <= -10	-2	Severe drop (10%+)
_worstDrop3d <= -7	-1	Caution drop (7%+)
_cumulative5d <= -10	-1	Cumulative 5-day decline > 10%
default	0	No sudden drops
Q27: Short Interest Risk
-1 to 0 pts
Inputs: shortPercentFloat·Missing data: zero·No short data available
Conditions	Pts	Interpretation
shortPercentFloat > 20	-1	High short interest
default	0	Normal
Q28: Low Float Risk
-1 to 0 pts
Inputs: floatShares·Missing data: zero
Conditions	Pts	Interpretation
floatShares < 20000000	-1	Low float risk
default	0	Normal float
Q29: Sector Performance vs Peers
-1 to 1 pts
Inputs: change1m, spyChange1m·Missing data: zero
Conditions	Pts	Interpretation
_spyDiff1m > 10	+1	Outperforming SPY
_spyDiff1m < -10	-1	Underperforming SPY
default	0	In line with SPY
Q30: 5-Day Relative Strength
-3 to 3 pts
Inputs: change5d, qqqChange5d·Missing data: zero
Conditions	Pts	Interpretation
change5d > 0 AND qqqChange5d < 0	+3	Up while market down
_alpha5d >= 5	+2	Strong alpha
_alpha5d >= 0	+1	Slight alpha
_alpha5d >= -5	0	Slight underperformance
change5d < 0 AND qqqChange5d > 0	-3	Down while market up
default	-2	Significant underperformance
Q31: Trend Deterioration
-3 to 0 pts
Inputs: hasLowerHighsLowerLows·Missing data: zero
Conditions	Pts	Interpretation
hasLowerHighsLowerLows == true	-3	Lower highs AND lower lows
default	0	No structural downtrend
