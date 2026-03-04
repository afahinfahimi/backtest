# Stock Scoring Configuration
Version: 13 (V13 - 31 Questions)
Last Updated: 02/04/2026

Max Raw Score: 71
Normalize By: 112
Formula: ROUND(((Raw Score + 41) / 112) × 100)

---

## Questions

### Q1: Sales Growth
- ID: 1
- Category: Growth Metrics
- Max Points: 6
- Min Points: 0
- Fields: annualRevenueGrowth, quarterlyRevenueYoY
- Scoring:
  - Annual ≥50% AND Quarterly > Annual: 6 pts (Accelerating Exceptional)
  - Annual ≥50% AND Quarterly > 0 but ≤ Annual: 5 pts (Steady Exceptional)
  - Annual 20-49% AND Quarterly > Annual: 5 pts (Accelerating Strong)
  - Annual 20-49% AND Quarterly > 0 but ≤ Annual: 4 pts (Steady Strong)
  - Annual 1-19% AND Quarterly > 0: 2 pts (Growing)
  - Annual ≥ 0 AND Quarterly ≤ 0: 1 pts (Stalling)
  - Annual < 0 AND Quarterly > 0: 1 pts (Recovering)
  - Annual < 0 AND Quarterly ≤ 0: 0 pts (Declining)

### Q2: Operating Income Growth
- ID: 2
- Category: Growth Metrics
- Max Points: 6
- Min Points: 0
- Fields: annualOperatingIncomeGrowth, quarterlyOperatingIncomeYoY
- Scoring:
  - Annual ≥50% AND Quarterly > Annual: 6 pts (Accelerating Exceptional)
  - Annual ≥50% AND Quarterly > 0 but ≤ Annual: 5 pts (Steady Exceptional)
  - Annual 20-49% AND Quarterly > Annual: 5 pts (Accelerating Strong)
  - Annual 20-49% AND Quarterly > 0 but ≤ Annual: 4 pts (Steady Strong)
  - Annual 1-19% AND Quarterly > 0: 2 pts (Growing)
  - Annual ≥ 0 AND Quarterly ≤ 0: 1 pts (Stalling)
  - Annual < 0 AND Quarterly > 0: 1 pts (Recovering)
  - Annual < 0 AND Quarterly ≤ 0: 0 pts (Declining)

### Q3: Cash Flow Growth
- ID: 3
- Category: Growth Metrics
- Max Points: 6
- Min Points: 0
- Fields: annualCashFlowGrowth, quarterlyCashFlowYoY
- Scoring:
  - Annual ≥50% AND Quarterly > Annual: 6 pts (Accelerating Exceptional)
  - Annual ≥50% AND Quarterly > 0 but ≤ Annual: 5 pts (Steady Exceptional)
  - Annual 20-49% AND Quarterly > Annual: 5 pts (Accelerating Strong)
  - Annual 20-49% AND Quarterly > 0 but ≤ Annual: 4 pts (Steady Strong)
  - Annual 1-19% AND Quarterly > 0: 2 pts (Growing)
  - Annual ≥ 0 AND Quarterly ≤ 0: 1 pts (Stalling)
  - Annual < 0 AND Quarterly > 0: 1 pts (Recovering)
  - Annual < 0 AND Quarterly ≤ 0: 0 pts (Declining)

### Q4: Net Profit Margin
- ID: 4
- Category: Profitability
- Max Points: 5
- Min Points: 0
- Fields: netProfitMargin
- Scoring:
  - ≥ 30%: 5 pts (Exceptional)
  - > 20%: 4 pts (Strong)
  - > 15%: 3 pts (Good)
  - > 10%: 2 pts (Moderate)
  - > 5%: 1 pts (Low)
  - ≤ 5%: 0 pts

### Q5: 1-Month Price Change
- ID: 5
- Category: Momentum
- Max Points: 4
- Min Points: 0
- Fields: priceChange1Month
- Scoring:
  - ≥ 20%: 4 pts
  - > 10%: 3 pts
  - > 5%: 2 pts
  - > 0%: 1 pts
  - ≤ 0%: 0 pts

### Q6: 10-Day Price Change
- ID: 6
- Category: Momentum
- Max Points: 3
- Min Points: 0
- Fields: priceChange10Day
- Scoring:
  - ≥ 15%: 3 pts
  - > 10%: 2 pts
  - > 5%: 1 pts
  - ≤ 5%: 0 pts

### Q7: Volume Liquidity
- ID: 7
- Category: Liquidity
- Max Points: 3
- Min Points: 0
- Fields: avgVolume20Day
- Scoring:
  - > 1M: 3 pts
  - > 500K: 2 pts
  - > 200K: 1 pts
  - ≤ 200K: 0 pts

### Q8: Ownership & Coverage
- ID: 8
- Category: Analyst & Institutions
- Max Points: 2
- Min Points: 0
- Fields: institutionalOwnership, hasAnalystCoverage
- Scoring:
  - Institutional ownership > 0%: 1 pts
  - Number of Analysts ≥ 1: 1 pts

### Q9: Price vs Moving Averages
- ID: 9
- Category: Technical
- Max Points: 4
- Min Points: 0
- Fields: price, sma50, sma200
- Scoring:
  - Above both 50D & 200D: 4 pts
  - Above 50D only: 3 pts
  - Above 200D only: 2 pts
  - Below both: 0 pts

### Q10: Debt-to-Equity
- ID: 10
- Category: Financial Health
- Max Points: 3
- Min Points: -3
- Fields: debtToEquity
- Scoring:
  - Negative (negative equity): -3 pts
  - < 0.5: 3 pts
  - < 1.0: 2 pts
  - < 2.0: 1 pts
  - ≥ 2.0: 0 pts

### Q11: Momentum Magnitude
- ID: 11
- Category: Weighted Momentum
- Max Points: 3
- Min Points: 0
- Formula: 52W %Chg + 3M %Chg
- Fields: priceChange52Week, priceChange3Month
- Scoring:
  - > 150%: 3 pts
  - > 100%: 2 pts
  - > 50%: 1 pts
  - ≤ 50%: 0 pts

### Q12: EPS Growth Prior Year
- ID: 12
- Category: EPS Growth
- Max Points: 4
- Min Points: 0
- Fields: epsGrowth
- Scoring:
  - ≥ 100%: 4 pts
  - > 50%: 3 pts
  - > 25%: 2 pts
  - > 0%: 1 pts
  - ≤ 0%: 0 pts

### Q13: Return on Equity
- ID: 13
- Category: Returns
- Max Points: 2
- Min Points: 0
- Fields: roe
- Scoring:
  - > 20%: 2 pts
  - > 10%: 1 pts
  - ≤ 10%: 0 pts

### Q14: Return on Assets
- ID: 14
- Category: Returns
- Max Points: 3
- Min Points: 0
- Fields: roa
- Scoring:
  - ≥ 15%: 3 pts
  - > 10%: 2 pts
  - > 5%: 1 pts
  - ≤ 5%: 0 pts

### Q15: Options Available
- ID: 15
- Category: Options & Country
- Max Points: 1
- Min Points: 0
- Fields: hasOptions
- Scoring:
  - Yes: 1 pts
  - No: 0 pts

### Q16: Country
- ID: 16
- Category: Options & Country
- Max Points: 1
- Min Points: 0
- Fields: country
- Scoring:
  - USA: 1 pts
  - Other: 0 pts

### Q17: Cash Burn Risk
- ID: 17
- Category: Risk Penalties
- Max Points: 0
- Min Points: -3
- Type: penalty
- Fields: netProfitMargin, quarterlyCashFlow, marketCap
- Scoring:
  - Profitable (Profit% ≥ 0%): 0 pts
  - Unprofitable BUT Quarterly Cash Flow ≥ 0: 0 pts
  - Unprofitable + Negative CF BUT Market Cap ≥ $10B: 0 pts
  - Profit% < 0% AND Quarterly CF < 0 AND Market Cap < $10B: -3 pts

### Q18: Deterioration Risk
- ID: 18
- Category: Risk Penalties
- Max Points: 0
- Min Points: -3
- Type: penalty
- Fields: quarterlySales, quarterlySalesQ4, quarterlyOpIncome, quarterlyOpIncomeQ4, quarterlyCashFlow, quarterlyCashFlowQ4
- Scoring:
  - Quarterly Sales < Sales(q-4) AND Quarterly OpIncome < OpIncome(q-4) AND Quarterly CashFlow < CashFlow(q-4): -3 pts
  - Otherwise: 0 pts

### Q19: Trend Consistency
- ID: 19
- Category: Trend & Strength
- Max Points: 3
- Min Points: 0
- Fields: priceChange3Month, priceChange52Week
- Scoring:
  - Both 3M AND 52W positive: 3 pts
  - One positive, one negative/zero: 1 pts
  - Both negative or zero: 0 pts

### Q20: Financial Strength
- ID: 20
- Category: Trend & Strength
- Max Points: 3
- Min Points: 0
- Fields: netProfitMargin, roe, debtToEquity
- Scoring:
  - Margin ≥20% AND ROE ≥20% AND D/E <0.5: 3 pts
  - Margin ≥10% AND ROE ≥10% AND D/E <1.5: 2 pts
  - Margin ≥0% AND ROE ≥5% AND D/E <3.0: 1 pts
  - Fails thresholds or missing data: 0 pts

### Q21: Momentum Divergence Penalty
- ID: 21
- Category: Risk Detection
- Max Points: 0
- Min Points: -10
- Type: penalty
- Fields: priceChange52Week, priceChange3Month
- Scoring:
  - 52W > 40% AND 3M < -5%: -10 pts
  - Otherwise: 0 pts

### Q22: Sector Preference
- ID: 22
- Category: Risk Detection
- Max Points: 2
- Min Points: -4
- Fields: sector, industry
- Scoring:
  - Computers and Technology, Finance, Business Services, Aerospace, Defence: 2 pts
  - Consumer Staples, Consumer Discretionary, Auto-Tires-Trucks, Retail-Wholesale, Medical, Industrial Products, Transportation, Utilities, Construction: 1 pts
  - Oils-Energy, Basic Materials, Gold/Mining, Pharma: 0 pts
  - Crypto-related (Bitcoin miners, crypto exchanges, blockchain companies): -4 pts

### Q23: Range Position (%B Bollinger)
- ID: 23
- Category: Range Position
- Max Points: 4
- Min Points: 0
- Formula: %B = (Price − Lower Band) ÷ (Upper Band − Lower Band)
- Fields: price, bollingerUpper, bollingerLower
- Scoring:
  - Breakout (> 100%): 4 pts
  - Buy zone (≤ 20%): 3 pts
  - Mid-range (20-80%): 2 pts
  - Upper zone (80-95%): 1 pts
  - Near top (> 95%): 0 pts

### Q24: Momentum Quality
- ID: 24
- Category: Momentum Quality
- Max Points: 2
- Min Points: -1
- Fields: priceChange52Week, priceChange3Month, priceChange1Month, priceChange10Day
- Scoring:
  - Spike Risk: 10D > 20% AND 1M < 10%: -1 pts
  - Smooth: 52W > 0 AND 3M > 0 AND 1M > 0 AND 52W > 3M > 1M > 10D: 2 pts
  - Accelerating: 3M > 0 AND (3M × 4) > 52W: 1 pts
  - Other / Default: 0 pts

### Q25: High P/E Momentum Trap
- ID: 25
- Category: Risk Detection
- Max Points: 0
- Min Points: -4
- Type: penalty
- Fields: peRatio, priceChange10Day
- Scoring:
  - P/E > 50 AND 10D < -5%: -4 pts
  - Otherwise: 0 pts

### Q26: Biotech Binary Event Burn
- ID: 26
- Category: Risk Detection
- Max Points: 0
- Min Points: -3
- Type: penalty
- Fields: sector, priceChange10Day
- Scoring:
  - 10D > 15%: -3 pts
  - Otherwise: 0 pts

### Q27: Sustained Downtrend
- ID: 27
- Category: Risk Penalty
- Max Points: 0
- Min Points: -3
- Type: penalty
- Fields: priceChangePercent, priceChange5Day, priceChange1Month
- Scoring:
  - 1D < 0% AND 5D < 0% AND 1M < 0%: -3 pts
  - Otherwise: 0 pts

### Q28: Sudden Drop / Slide
- ID: 28
- Category: Risk Penalty
- Max Points: 0
- Min Points: -6
- Type: penalty
- Fields: sessionChange0, sessionChange1, sessionChange2, priceChange5Day
- Scoring:
  - Critical: Any single day ≥ 15% drop within last 3 days: -6 pts
  - Severe: Any single day ≥ 10% drop within last 3 days: -2 pts
  - Caution: Any single day ≥ 7% drop within last 3 days, OR cumulative 5-day return ≤ -10%: -1 pts
  - None: No conditions met: 0 pts

### Q29: Short Interest Risk
- ID: 29
- Category: Risk Penalty
- Max Points: 0
- Min Points: -1
- Type: penalty
- Fields: shortPercentFloat
- Scoring:
  - Short % Float > 20%: -1 pts
  - Short % Float ≤ 20%: 0 pts

### Q30: Low Float Risk
- ID: 30
- Category: Risk Penalty
- Max Points: 0
- Min Points: -1
- Type: penalty
- Fields: floatShares
- Scoring:
  - Float < 20M shares: -1 pts
  - Float ≥ 20M shares: 0 pts

### Q31: Sector Performance vs Peers
- ID: 31
- Category: Momentum
- Max Points: 1
- Min Points: -1
- Fields: priceChange1Month, sectorPerformance1M
- Scoring:
  - Outperforms sector by > 10%: 1 pts
  - Within ±10% of sector: 0 pts
  - Underperforms sector by > 10%: -1 pts
