# SA Engine — V17 (31 Questions)

## Core Metrics:
* Normalization: -42 to 70
* Post-processing: Q16 + Q17 max -4

## Growth & Profitability (Q1 - Q4)

| ID | Metric | Inputs | Caps / Notes |
|----|--------|--------|--------------|
| Q1 | Sales Growth | `annualRevenueGrowth`, `quarterlyRevenueGrowth` | `isCyclical` `NoBreakout` → max 4 |
| Q2 | Operating Income Growth | `annualOperatingIncomeGrowth`, `quarterlyOperatingIncomeGrowth` | `isCyclical` `NoBreakout` → max 4 |
| Q3 | Cash Flow Growth | `annualCashFlowGrowth`, `quarterlyCashFlowGrowth` | `isCyclical` `NoBreakout` → max 4 |

### Scoring Table for Q1, Q2, and Q3:

| Conditions | Pts | Interpretation |
|------------|-----|----------------|
| annualGrowth >= 50 AND quarterlyGrowth > annualGrowth | +6 | Accelerating Exceptional |
| annualGrowth >= 50 AND quarterlyGrowth > 0 | +5 | Steady Exceptional |
| annualGrowth >= 20 AND < 50 AND quarterlyGrowth > annualGrowth | +5 | Accelerating Strong |
| annualGrowth >= 20 AND < 50 AND quarterlyGrowth > 0 | +4 | Steady Strong |
| annualGrowth >= 1 AND < 20 AND quarterlyGrowth > 0 | +2 | Growing |
| annualGrowth >= 0 AND quarterlyGrowth <= 0 | +1 | Stalling |
| annualGrowth < 0 AND quarterlyGrowth > 0 | +1 | Recovering |
| default | 0 | Declining |

### Q4: Net Profit Margin
* Inputs: `netProfitMargin`

| Conditions | Pts | Interpretation |
|------------|-----|----------------|
| netProfitMargin >= 30 | +5 | Exceptional |
| netProfitMargin >= 20 | +4 | Strong |
| netProfitMargin >= 15 | +3 | Good |
| netProfitMargin >= 10 | +2 | Moderate |
| netProfitMargin >= 5 | +1 | Low |
| default | 0 | None |

## Momentum & Liquidity (Q5 - Q9)

| ID | Metric | Conditions | Pts | Interpretation |
|----|--------|------------|-----|----------------|
| Q5 | 1-Month Price Change | change1m >= 20 / 10 / 5 / >0 | +4 / +3 / +2 / +1 | Momentum tiers |
| Q6 | 10-Day Price Change | change10d >= 15 / 10 / 5 | +3 / +2 / +1 | Short-term strength |
| Q7 | 20-Day Avg Volume | avgVolume20d >= 1M / 500k / 200k | +3 / +2 / +1 | Liquidity tiers |
| Q8 | Ownership & Coverage | institutionalOwnership > 0 / analystCount > 0 | +1 / +1 | Additive coverage |
| Q9 | Price vs Moving Avg | price > sma20 AND sma50 | +4 | Above both 20D & 50D |
|    |                     | price > sma50 / price > sma20 | +3 / +2 | Above one MA |

## Financial Health & Returns (Q10 - Q15)

| ID | Metric | Conditions | Pts | Interpretation |
|----|--------|------------|-----|----------------|
| Q10 | Debt-to-Equity | < 0 / < 0.5 / < 1 / < 2 | -3 / +3 / +2 / +1 | Capital structure |
| Q11 | Momentum Mag. | _momSum > 150 / 100 / 50 | +3 / +2 / +1 | Aggregate momentum |
| Q12 | EPS Growth (PY) | >= 100 / 50 / 25 / >0 | +4 / +3 / +2 / +1 | Historical growth |
| Q13 | Return on Equity | roe >= 20 / 10 | +2 / +1 | Efficiency |
| Q14 | Return on Assets | roa >= 15 / 10 / 5 | +3 / +2 / +1 | Efficiency |
| Q15 | Country | US / Developed / China-EM | +1 / 0 / -2 | Geopolitical risk |

## Risk Assessment (Q16 - Q20)

| ID | Metric | Conditions | Pts | Interpretation |
|----|--------|------------|-----|----------------|
| Q16 | Cash Burn Risk | If not profitable/CF positive/Large Cap | -3 | Financial instability |
| Q17 | Deterioration Risk | Rev, OpInc, & CF all < 0 QoQ | -3 | Broad fundamental decline |
| Q18 | Financial Strength | High margins, ROE, and low debt | +1 to +3 | Combined quality score |
| Q19 | Mom. Divergence | 52w high but short-term falling | -3 | Bull trap / Reversal |
| Q20 | Sector Preference | Preferred / Neutral / Crypto | +2 / +1 / -4 | Industry outlook |

## Technicals & Advanced Risk (Q21 - Q31)

| ID | Metric | Conditions | Pts | Interpretation |
|----|--------|------------|-----|----------------|
| Q21 | %B (Bollinger) | > 100 / > 95 / >= 80 / >= 20 | +4 / +3 / +2 / +1 | Price channel position |
| Q22 | Mom. Quality | Smooth / Accelerating / Spike Risk | +2 / +1 / -1 | Trend sustainability |
| Q23 | High P/E Trap | peRatio > 50 AND change10d < -5 | -4 | Valuation cliff |
| Q24 | Biotech Spike | biotechSector AND change10d > 15 | -3 | Binary event risk |
| Q25 | Sustained Down | 1d, 5d, and 1m all negative | -3 | Structural decline |
| Q26 | Sudden Drop | 3d drop >= 15% / 10% / 7% | -6 / -2 / -1 | Crash protection |
| Q27 | Short Interest | shortPercentFloat > 20 | -1 | High short risk |
| Q28 | Low Float | floatShares < 20,000,000 | -1 | Volatility risk |
| Q29 | Relative vs SPY | _spyDiff1m > 10 / < -10 | +1 / -1 | Market outperformance |
| Q30 | Relative vs QQQ | Up while mkt down / Alpha 5d | +3 / +2 | Relative strength |
| Q31 | Trend Deterioration | Lower Highs + Lower Lows | -3 | Structural downtrend |
