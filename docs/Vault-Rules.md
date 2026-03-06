Read-only reference of all engine rules. Use rule IDs (e.g. "Q5", "R1", "M-V2", "NORM-SA", "CONST-CRYPTO") when requesting changes.

Download MD
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
_symbol in [metalsMiningSymbols]	0	Metals & Mining
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
MC Engine — V16 (17 Questions)
Normalization: -40 to 52
Q1: QQQ Price vs MAs
-5 to 5 pts
Inputs: qqqPrice, qqqSMA50, qqqSMA200·Missing data: zero
Conditions	Pts	Interpretation
qqqPrice <= qqqSMA50 AND qqqPrice <= qqqSMA200	+5	Below both MAs (Oversold - Buy Opportunity)
qqqPrice <= qqqSMA200 AND qqqPrice > qqqSMA50	+2	Below 200MA only
qqqPrice > qqqSMA200 AND qqqPrice <= qqqSMA50	-2	Above 200MA only
default	-5	Above both MAs (Extended - Caution)
Q2: Trend Confirmation
-3 to 5 pts
Inputs: qqqSMA50, qqqSMA200·Missing data: zero
Conditions	Pts	Interpretation
_maSpreadAbs <= 1	+5	MAs flat or converging (Inflection Point)
_maSpread < 0 AND _maSpreadAbs < 5	+3	50MA below 200MA, < 5% spread (Early Recovery)
_maSpread > 0 AND _maSpread < 5	+1	50MA above 200MA, < 5% spread (Mild Uptrend)
_maSpread >= 5	-3	50MA ≥ 5% above 200MA (Extended Uptrend)
default	-3	50MA ≥ 5% below 200MA (Deep Downtrend)
Q3: RSI Momentum
-3 to 5 pts
Inputs: qqqRSI·Missing data: custom
Conditions	Pts	Interpretation
qqqRSI < 30	+5	Oversold Opportunity
qqqRSI >= 30 AND qqqRSI < 40	+1	Low Momentum
qqqRSI >= 40 AND qqqRSI < 50	+2	Below Average
qqqRSI >= 50 AND qqqRSI < 60	+3	Healthy
qqqRSI >= 60 AND qqqRSI < 70	+1	Above Average
qqqRSI >= 70	-3	Overbought Risk
default	+1	Moderate zone
Q4: VIX vs 3-Month Avg
-5 to 5 pts
Inputs: vix3mChange·Missing data: zero
Conditions	Pts	Interpretation
vix3mChange > 20	+5	VIX spiking (Buy Opportunity)
vix3mChange >= 10	+3	VIX rising
vix3mChange >= -10	0	VIX near avg
vix3mChange >= -20	-3	VIX falling
default	-5	VIX well below avg (Complacency)
Q5: VIX Absolute Level
-3 to 5 pts
Inputs: vixPrice·Missing data: zero
Conditions	Pts	Interpretation
vixPrice > 22	+5	High Fear (Buy Opportunity)
vixPrice >= 14	0	Normal Range
default	-3	Complacency (Caution)
Q6: QQQ 52-Week Strength
-3 to 5 pts
Inputs: qqq52WChange·Missing data: zero
Conditions	Pts	Interpretation
qqq52WChange >= -10 AND qqq52WChange < 0	+5	Slight Loss (Best Buy Opportunity)
qqq52WChange >= 0 AND qqq52WChange < 10	+3	Slight Gain (Early Recovery)
qqq52WChange >= -20 AND qqq52WChange < -10	+1	Moderate Loss
qqq52WChange < -20	0	Severe Loss
qqq52WChange >= 10 AND qqq52WChange < 20	0	Good Yearly Gain
default	-3	Strong Yearly Gain (Extended)
Q7: MACD Score
-3 to 3 pts
Inputs: qqqMACDHistogram, qqqMACDHistogramPrev·Missing data: zero
Conditions	Pts	Interpretation
qqqMACDHistogram <= 0 AND _macdNearZero == true	0	Sell - Weakest (Near Zero)
qqqMACDHistogram <= 0	+3	Sell signal (contrarian buy)
qqqMACDHistogram > 0 AND _macdNearZero == true	0	Buy - Weakest (Near Zero)
qqqMACDHistogram > 0	-3	Buy signal (contrarian extended)
default	0	Neutral
Q8: QQQ Range Position
-2 to 3 pts
Inputs: qqqPrice, qqq52WHigh, qqq52WLow·Missing data: zero
Conditions	Pts	Interpretation
_rangePosition < 0.1	+3	Near support (bounce potential)
_rangePosition < 0.45	+1	Lower half
_rangePosition < 0.55	0	Near middle
_rangePosition < 0.9	+1	Upper half
default	-2	Near resistance (extended)
Q9: GDP Growth Proxy (SPY 3M)
-3 to 3 pts
Inputs: spy3mChange·Missing data: zero
Conditions	Pts	Interpretation
spy3mChange < 0	+3	Contraction (Buy Opportunity)
spy3mChange <= 6	0	Moderate/Stalling
default	-3	Strong Growth (Extended)
Q10: Unemployment Trend (XLI)
-1 to 2 pts
Inputs: xli1mChange·Missing data: zero
Conditions	Pts	Interpretation
xli1mChange < -2	+2	Industrial Weakness (Buy Opportunity)
xli1mChange <= 3	0	Stable
default	-1	Industrial Expansion (Extended)
Q11: International Markets (EFA vs SPY)
-2 to 2 pts
Inputs: efa1mChange, spy1mChange·Missing data: zero
Conditions	Pts	Interpretation
_efaDiff >= 1 AND _efaDiff <= 3	+2	Slight Outperformance
_efaDiff > 3	+1	Global Strength
_efaDiff >= -1	0	Neutral
_efaDiff >= -3	-1	EFA lags SPY
default	-2	US Isolation
Q12: Commodities (XLE + GLD)
-2 to 2 pts
Inputs: xle1mChange, gld1mChange·Missing data: zero
Conditions	Pts	Interpretation
xle1mChange < -3 AND gld1mChange > 3	+2	Risk-Off/Fear (Buy Opportunity)
xle1mChange < -3	+1	Mild Risk-Off
xle1mChange > 3 AND gld1mChange < -3	-2	Risk-On (Extended)
xle1mChange > 3	-1	Mild Risk-On
default	0	Mixed/Stable
Q13: Small-Cap Breadth (IWM vs QQQ)
-1 to 1 pts
Inputs: iwm1mChange, qqq1mChange·Missing data: zero
Conditions	Pts	Interpretation
_iwmDiff > 3	+1	High Risk Appetite
_iwmDiff < -3	-1	Flight to Safety
default	0	Neutral
Q14: Sector Rotation (XLY vs XLP)
-1 to 1 pts
Inputs: xly1mChange, xlp1mChange·Missing data: zero
Conditions	Pts	Interpretation
_xlyDiff < -3	+1	Defensive Rotation (Buy Opportunity)
_xlyDiff > 3	-1	Consumer Confidence (Extended)
default	0	Neutral
Q15: Equal-Weight Breadth (RSP vs SPY)
-1 to 1 pts
Inputs: rsp1mChange, spy1mChange·Missing data: zero
Conditions	Pts	Interpretation
_rspDiff < -0.5	+1	Narrow Rally (Reversal Risk)
_rspDiff > 2	-1	Broad Participation (Extended)
default	0	Neutral
Q16: Credit Spreads (HYG)
0 to 2 pts
Inputs: hyg1mChange·Missing data: zero
Conditions	Pts	Interpretation
hyg1mChange < -1	+2	Credit Stress (Buy Opportunity)
default	0	No Signal
Q17: Dollar Index (UUP)
-2 to 2 pts
Inputs: uup1mChange·Missing data: zero
Conditions	Pts	Interpretation
uup1mChange < -2	+2	Dollar Weakening (Bullish)
uup1mChange < 0	+1	Mild Weakening
uup1mChange <= 1	0	Neutral
uup1mChange <= 2	-1	Mild Strengthening
default	-2	Dollar Spiking (Headwind)
Action Signals — V18
Stock Rules
5
ID	Pri	Signal	Holding Signal	Conditions	Color
R1	30	Buy in Good Market	Hold and Add if Tier Allows	saScore >= 80	t-green
R2	31	Buy if Stable	Hold and Add if Tier Allows	saScore >= 75	t-teal
R3	32	Consider Buying	Consider Selling — Add 10% Trailing Stop Loss	saScore >= 70	t-blue
R4	33	Monitor	Sell Low Quality. Add tight Stops	saScore >= 60	t-yellow
FB	99	Watch	Hold	(always)	t-blue
Market Rules
8
ID	Pri	Signal	Holding Signal	Conditions	Color
M-V1	1	VIX ≥ 30 — Great Buying Opportunity	Hold and Add (SA ≥ 70 only)	vix >= 30	t-green
M-V2	2	VIX ≥ 25 — Buying Opportunity	Hold and Add (SA ≥ 70 only)	vix >= 25	t-teal
M-MC1	3	Very Weak Market — Sell All	Exit All Positions	mcScore < 20	t-red
M-MC2	4	Slow Market — Be Careful	Reduce Risk	mcScore >= 20 AND mcScore < 40	t-yellow
M-MC3	5	Over-Heated Market — Only Great Stocks	Exit Risky Positions	mcScore >= 81	t-blue
M-R1	6	Heated Market — Buy Carefully	Hold with Stops	mcScore > 60 AND mcScore <= 80	t-orange
M-R2	7	Normal Market — Buy Quality Stocks	Hold Quality Stocks	mcScore >= 40 AND mcScore <= 60	t-green
M-FB	99	Market — Unknown	Hold	(always)	t-gray
Tiers
Tier	SA	Condition	Max Position	Color
T1	≥ 65	Profitable + Market Cap > $50B	$100,000	t-green
T2	≥ 65	Profitable + Market Cap > $2B	$50,000	t-blue-2
T3	≥ 65	Market Cap > $100M + (Growth OR Small Profitable)	$20,000	t-yellow
SELL	N/A	Does not qualify	$0	t-red
Conviction Levels (V18)
Replaces Chart column. Column header: CON. The SA score bubble is the single color source — Signal text and CON box inherit the SA bubble color token. No independent color logic. Sort: Conviction level first (C1→C4), then SA score descending.

Level	Label	Conditions Met	Sort Priority
C1	Prime	All 3 (A + B + C)	1st
C2	Strong	Any 2 of 3	2nd
C3	Valid	Any 1 of 3	3rd
C4	Weak	None	4th
Conviction Conditions

ID	Condition	Requirement
A	SA Hold	SA ≥ 80 held for 10+ consecutive days
B	MC Zone	MC between 50 and 80
C	QQQ Trend	QQQ positive on 1D, 5D, and 1M price change
Conviction % — SA 80+

Conditions Met	MC 50–80	MC 40–49	MC 30–39	MC 20–29
3 (C1)	90%	85%	80%	75%
2 (C2)	80%	75%	70%	65%
1 (C3)	75%	70%	65%	60%
0 (C4)	70%	65%	60%	55%
Conviction % — SA 75–79

Conditions Met	MC 50–80	MC 40–49	MC 30–39	MC 20–29
3 (C1)	75%	70%	65%	60%
2 (C2)	70%	65%	60%	55%
1 (C3)	68%	63%	58%	53%
0 (C4)	65%	60%	55%	50%
Conviction % — SA 65–74 (Informational Only)

Grayed out. No buy signal. No condition bonuses — MC band drives % only. VIX adjustment does NOT apply. No C1–C4 labels.

MC Band	SA 70–74	SA 65–69
50–80	50%	50%
40–49	55%	50%
30–39	50%	50%
20–29	45%	45%
< 20	Hard block	Hard block
VIX Adjustment (applied after base % — SA 75+ only)

Condition	Adjustment	Cap
VIX 25–29	+3%	95%
VIX ≥ 30	+5%	95%
SA < 65: CON column empty, no % shown. Detail panel still opens.
SA 65–74: CON box renders in gray — informational only, never actionable buy signals.

CON Box Color Thresholds

Conviction %	Color Token	Display
> 74%	t-green	Green — strong conviction
65–74%	t-teal	Teal — moderate conviction
55–64%	t-blue	Blue — low conviction
< 55%	t-yellow	Yellow — weak conviction
SA 65–74	muted	Gray — informational only
Hard Blocks

ID	Target	Effect
CRYPTO-BLOCK	CONST-CRYPTO symbols	🚫 No buy signal regardless of SA score. Conviction % shown with 🚫 badge
HEALTH-BLOCK	CONST-BIOTECH sectors (SA ≥ 75)	🚫 No buy signal in 80+ and 75-79 zones. Conviction % shown with 🚫 badge
BM-ALERT	Basic Materials 3rd+ stock	⚠️ Sector Concentration badge (alert only, not blocked)
Entry Confirmation Signals (3-Day Rule)
Day 0 = trigger, Day 1 = hold, Day 2 = act. Signals require SA score to cross and hold at a threshold for 3 consecutive days.

Entry Signals

ID	Label	Holding Label	Threshold	Color
CE-80	3D of 80+	Continue Holding	SA crosses above 80, held 3 days	t-green
CE-75	3D of 75+	Continue Holding	SA crosses above 75, held 3 days	t-teal
CE-70	3D of 70+	Consider Selling	SA crosses above 70, held 3 days	t-blue
Exit Signals

ID	Label	Holding Label	Threshold	Color
CX-65	Do Not Buy	Under 65 Exit	SA crosses below 65, held 3 days	t-red
CX-70	Wait and Monitor	Under 70 Exit	SA crosses below 70, held 3 days	t-orange
CX-75	Reduce Position	—	SA crosses below 75, held 3 days	t-orange
CX-80	Move Under 80. Monitor	Watch Carefully	SA crosses below 80, held 3 days	t-yellow
Recovery Signals (Dip-and-Recover)

ID	Label	Holding Label	Trigger	Color
CR-80	Good Buy Time	Drop 80 Recovery Hold	Was ≥80, dipped below, recovered within 3 days	t-green
CR-75	OK to Buy	Drop 75 Recovery	Was ≥75, dipped below, recovered next day	t-teal
CR-70	Ready to Buy	Drop 70 Recovery	Was ≥70, dipped below, recovered next day	t-yellow
Gradual Decline Signals

ID	Label	Holding Label	Trigger	Color
CD-DROP	6+ Drop	Consider Selling	SA drops 5+ pts over 2 days, sustained for 2 days (SA ≥ 65)	t-yellow
CD-REC	6+ Drop Recovery	Watch Carefully	SA drops 5+ pts but recovers next day (SA ≥ 65)	t-yellow
Suppression Rules

ID	Rule	Effect
CS-1	SA rises 5+ pts in 1 day	Signal suppressed — no predictive value
CS-2	SA drops 5–10 pts but stays above 75	Signal suppressed — buy the dip
CS-3	MC < 30 AND SA ≥ 80 AND 3+ days above 80	Exit signals suppressed — strong stock in oversold market
Formulas, Constants & Reference
Formulas & Caps
ID	Name	Formula / Value	Source
NORM-SA	SA Normalization	((raw + 42) / 112) × 100 — min: -42, max: 70	sa-config
NORM-MC	MC Normalization	((raw + 40) / 92) × 100 — min: -40, max: 52	mc-config
PP-1	Combined Penalty Cap	Q16 + Q17 combined max -4	sa-config postProcessing
CAP-CYCLICAL	Cyclical Sector Cap	Q1–Q3 capped at 4 pts for Basic Materials/Energy/Mining unless Q21 breakout (>100%)	sa-config contextFlags
BM-ALERT	Basic Materials Concentration	3rd+ Basic Materials stock shows ⚠️ "Sector Concentration" badge (alert only, no signal block)	action-signal-engine
Forward Performance Periods
ID	Period	Applies To	Description
FWD-STOCK-1	5D	Stock Matrix	5 trading days forward return
FWD-STOCK-2	10D	Stock Matrix	10 trading days forward return
FWD-STOCK-3	1M	Stock Matrix	~21 trading days forward return
FWD-STOCK-4	2M	Stock Matrix	~42 trading days forward return
FWD-STOCK-5	3M	Stock Matrix	~63 trading days forward return
FWD-MC-1	5D	MC Matrix	5 trading days forward return
FWD-MC-2	10D	MC Matrix	10 trading days forward return
FWD-MC-3	1M	MC Matrix	~21 trading days forward return
FWD-MC-4	2M	MC Matrix	~42 trading days forward return
FWD-MC-5	3M	MC Matrix	~63 trading days forward return
Constants & Lists
ID	Name	Count	Values
CONST-CRYPTO	Crypto Symbols	21	IREN, MARA, CLSK, RIOT, BITF, WULF, HUT, CIFR, COIN, MSTR, CORZ, BTBT, HIVE, BTDR, GRDI, MIGI, BTCS, ARBK, DGHI, MGTI, SOS
CONST-METALS	Metals & Mining Symbols	25	NEM, GFI, KGC, AU, HMY, CDE, HL, NGD, CGAU, AEM, GOLD, AG, WPM, FNV, RGLD, OR, PAAS, EXK, FSM, MAG, SVM, FCX, TECK, HBM, SBSW
CONST-PREFERRED	Preferred Sectors	11	Technology, Computers and Technology, Finance, Financial Services, Business Services, Aerospace, Defence, Industrials, Industrial Products, Construction, Transportation
CONST-NEUTRAL	Neutral Sectors	5	Consumer Staples, Consumer Discretionary, Auto-Tires-Trucks, Retail-Wholesale, Utilities
CONST-BIOTECH	Biotech Sectors	6	Healthcare, Biotechnology, Medical Devices, Drug Manufacturers, Medical, Pharma
CONST-US	US Countries	3	USA, US, UNITED STATES
CONST-DEVELOPED	Developed Countries	28	Canada, UK, United Kingdom, Netherlands, Germany, France, Japan, Australia, Taiwan, South Korea, Switzerland, Ireland, Israel, Sweden, Norway, Denmark, Finland, Spain, Italy, Singapore, New Zealand, Hong Kong, Belgium, Austria, UAE, United Arab Emirates, Saudi Arabia, Qatar
CONST-EM	China/EM Countries	20	China, Brazil, South Africa, India, Mexico, Indonesia, Turkey, Thailand, Philippines, Vietnam, Colombia, Chile, Peru, Egypt, Nigeria, Pakistan, Bangladesh, Malaysia, Argentina, Russia
