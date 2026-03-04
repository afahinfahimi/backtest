# Market Conditions Configuration
Version: 13.0.0
Last Updated: 2026-02-01

Max Score: undefined
Min Score: undefined
Normalize By: undefined

---

## Questions

### Q1: QQQ Price vs Moving Averages
- ID: 1
- Category: Technical Indicators
- Max Points: 5
- Min Points: -5
- Fields: price, sma50, sma200
- Scoring:
  - QQQ above both 50MA and 200MA: 5 pts
  - QQQ above 200MA only (below 50MA): 2 pts
  - QQQ at/near both MAs (± 1%): 0 pts
  - QQQ below 200MA only (above 50MA): -2 pts
  - QQQ below both 50MA and 200MA: -5 pts

### Q2: Trend Confirmation (50MA-200MA Spread)
- ID: 2
- Category: Technical Indicators
- Max Points: 5
- Min Points: -5
- Formula: 50MA-200MA Spread %
- Fields: sma50, sma200
- Scoring:
  - 50MA ≥ 5% above 200MA: 5 pts
  - 50MA above 200MA, < 5% spread: 3 pts
  - MAs flat or converging (± 1%): 0 pts
  - 50MA below 200MA, < 5% spread: -3 pts
  - 50MA ≥ 5% below 200MA: -5 pts

### Q3: RSI Momentum
- ID: 3
- Category: Technical Indicators
- Max Points: 5
- Min Points: -3
- Fields: rsi
- Scoring:
  - RSI < 30 (oversold opportunity): 5 pts
  - RSI 50-60: 3 pts
  - RSI 40-50: 2 pts
  - RSI 60-70 OR RSI 30-40: 1 pts
  - RSI > 70 (overbought risk): -3 pts

### Q4: VIX vs 3-Month Average
- ID: 4
- Category: Technical Indicators
- Max Points: 5
- Min Points: -5
- Fields: vix3MonthChange
- Scoring:
  - VIX 3M %Chg < -20% (well below avg): 5 pts
  - VIX 3M %Chg -20% to -10%: 3 pts
  - VIX 3M %Chg -10% to +10% (near avg): 0 pts
  - VIX 3M %Chg +10% to +20%: -3 pts
  - VIX 3M %Chg > +20% (well above avg): -5 pts

### Q5: VIX Absolute Level
- ID: 5
- Category: Technical Indicators
- Max Points: 3
- Min Points: -5
- Fields: vix
- Scoring:
  - VIX 14-18: 3 pts
  - VIX < 14: 2 pts
  - VIX 18-22: 1 pts
  - VIX 22-25: -1 pts
  - VIX 25-30: -3 pts
  - VIX > 30: -5 pts

### Q6: Intermarket Correlation
- ID: 6
- Category: Technical Indicators
- Max Points: 0
- Min Points: 0
- Fields: N/A
- Scoring:
  - SKIPPED - No reliable API data: 0 pts

### Q7: QQQ 52-Week Strength
- ID: 7
- Category: Technical Indicators
- Max Points: 5
- Min Points: -5
- Fields: qqq52WeekChange
- Scoring:
  - 52W Change ≥ 20%: 5 pts
  - 52W Change 10-20%: 3 pts
  - 52W Change 0-10%: 1 pts
  - 52W Change -10% to 0%: -1 pts
  - 52W Change -20% to -10%: -3 pts
  - 52W Change < -20%: -5 pts

### Q8: MACD Score
- ID: 8
- Category: Technical Indicators
- Max Points: 4
- Min Points: -4
- Fields: macdHistogram, prevMacdHistogram
- Scoring:
  - Buy Signal + Strengthening: 4 pts
  - Buy Signal + Weakening: 2 pts
  - Buy Signal + Near Zero: 1 pts
  - Sell Signal + Near Zero: -1 pts
  - Sell Signal + Weakening: -2 pts
  - Sell Signal + Strengthening: -4 pts

### Q9: QQQ Range Position
- ID: 9
- Category: Technical Indicators
- Max Points: 3
- Min Points: -2
- Formula: (Price - 52W Low) / (52W High - 52W Low)
- Fields: price, 52WeekHigh, 52WeekLow
- Scoring:
  - Range < 0.10 (Bottom 10% - bounce potential): 3 pts
  - Range 0.10-0.45 (Lower half): 1 pts
  - Range 0.45-0.55 (Near middle): 0 pts
  - Range 0.55-0.90 (Upper half): 1 pts
  - Range > 0.90 (Top 10% - extended): -2 pts

### Q10: GDP Growth Proxy (SPY 3M)
- ID: 10
- Category: Macro Indicators
- Max Points: 3
- Min Points: -3
- Fields: spy3MonthChange
- Scoring:
  - SPY 3M > 10% (Strong Growth): 3 pts
  - SPY 3M 6-10%: 2 pts
  - SPY 3M 3-6%: 0 pts
  - SPY 3M 0-3% (Stalling): -2 pts
  - SPY 3M negative (Contraction risk): -3 pts

### Q11: Federal Reserve Policy (TLT-IEF Spread)
- ID: 11
- Category: Macro Indicators
- Max Points: 3
- Min Points: -3
- Formula: TLT 1M %Chg - IEF 1M %Chg
- Fields: tlt1MonthChange, ief1MonthChange
- Scoring:
  - Spread > 2% (Dovish / Rates Falling): 3 pts
  - Spread 0% to 2%: 2 pts
  - Spread -1% to 0% (Stable): 0 pts
  - Spread -2% to -1% (Hawkish lean): -1 pts
  - Spread < -2% (Hawkish / Rates Rising): -3 pts

### Q12: Unemployment Trend (XLI Momentum)
- ID: 12
- Category: Macro Indicators
- Max Points: 2
- Min Points: -2
- Formula: XLI 1M %Chg
- Fields: xli1MonthChange
- Scoring:
  - Change > 3% (Industrial Expansion): 2 pts
  - Change 0-3%: 1 pts
  - Change -2% to 0%: 0 pts
  - Change -5% to -2%: -1 pts
  - Change < -5% (Industrial Contraction): -2 pts

### Q13: Treasury Yield Curve
- ID: 13
- Category: Macro Indicators
- Max Points: 3
- Min Points: -3
- Formula: 10Y Rate - 2Y Rate
- Fields: 10YRate, 2YRate
- Scoring:
  - Spread > 1% (Healthy): 3 pts
  - Spread 0-1%: 1 pts
  - Spread -0.5% to 0% (Flat): 0 pts
  - Spread -1% to -0.5% (Inverted): -2 pts
  - Spread < -1% (Deeply Inverted): -3 pts

### Q14: International Markets (EFA vs SPY)
- ID: 14
- Category: Breadth & Intermarket
- Max Points: 2
- Min Points: -2
- Formula: EFA 1M %Chg - SPY 1M %Chg
- Fields: efa1MonthChange, spy1MonthChange
- Scoring:
  - EFA beats SPY by > 3% (Global Strength): 2 pts
  - EFA beats SPY by 1-3%: 1 pts
  - Within ± 1%: 0 pts
  - EFA lags SPY by 1-3%: -1 pts
  - EFA lags SPY by > 3% (US Isolation): -2 pts

### Q15: Commodities Trend (XLE + GLD)
- ID: 15
- Category: Breadth & Intermarket
- Max Points: 2
- Min Points: -2
- Fields: xle1MonthChange, gld1MonthChange
- Scoring:
  - XLE Up AND GLD Down (Risk-On): 2 pts
  - XLE Up AND GLD Stable: 1 pts
  - Mixed / Both Stable: 0 pts
  - XLE Down AND GLD Stable: -1 pts
  - XLE Down AND GLD Up (Risk-Off): -2 pts

### Q16: Small-Cap Breadth (IWM vs QQQ)
- ID: 16
- Category: Breadth & Intermarket
- Max Points: 3
- Min Points: -3
- Formula: IWM 1M %Chg - QQQ 1M %Chg
- Fields: iwm1MonthChange, qqq1MonthChange
- Scoring:
  - IWM beats QQQ by > 3% (High Risk Appetite): 3 pts
  - IWM beats QQQ by 1-3%: 1 pts
  - Within ± 1%: 0 pts
  - IWM lags QQQ by 1-3%: -1 pts
  - IWM lags QQQ by > 3% (Flight to Safety): -3 pts

### Q17: Sector Rotation (XLY vs XLP)
- ID: 17
- Category: Breadth & Intermarket
- Max Points: 2
- Min Points: -2
- Formula: XLY 1M %Chg - XLP 1M %Chg
- Fields: xly1MonthChange, xlp1MonthChange
- Scoring:
  - XLY beats XLP by > 3% (Consumer Confidence): 2 pts
  - XLY beats XLP by 1-3%: 1 pts
  - Within ± 1%: 0 pts
  - XLY lags XLP by 1-3%: -1 pts
  - XLY lags XLP by > 3% (Defensive Rotation): -2 pts

### Q18: Equal-Weight Breadth (RSP vs SPY)
- ID: 18
- Category: Breadth & Intermarket
- Max Points: 2
- Min Points: -2
- Formula: RSP 1M %Chg - SPY 1M %Chg
- Fields: rsp1MonthChange, spy1MonthChange
- Scoring:
  - RSP beats SPY by > 2% (Broad Participation): 2 pts
  - RSP beats SPY by 0.5-2%: 1 pts
  - Within ± 0.5%: 0 pts
  - RSP lags SPY by 0.5-2%: -1 pts
  - RSP lags SPY by > 2% (Narrow Rally): -2 pts

### Q19: Transportation (IYT vs SPY)
- ID: 19
- Category: Breadth & Intermarket
- Max Points: 2
- Min Points: -2
- Formula: IYT 1M %Chg - SPY 1M %Chg
- Fields: iyt1MonthChange, spy1MonthChange
- Scoring:
  - IYT beats SPY by > 2% (Economic Activity High): 2 pts
  - IYT beats SPY by 0.5-2%: 1 pts
  - Within ± 0.5%: 0 pts
  - IYT lags SPY by 0.5-2%: -1 pts
  - IYT lags SPY by > 2% (Demand Issues): -2 pts

### Q20: Credit Spreads (HYG Performance)
- ID: 20
- Category: Credit & Sentiment
- Max Points: 2
- Min Points: -2
- Fields: hyg1MonthChange
- Scoring:
  - HYG > 1% (Risk Appetite High): 2 pts
  - HYG 0% to 1%: 1 pts
  - HYG -0.5% to 0%: 0 pts
  - HYG -1% to -0.5%: -1 pts
  - HYG < -1% (Credit Stress): -2 pts

### Q21: Dollar Index (UUP Trend)
- ID: 21
- Category: Credit & Sentiment
- Max Points: 2
- Min Points: -2
- Fields: uup1MonthChange
- Scoring:
  - UUP < -2% (Dollar Weakening - Bullish): 2 pts
  - UUP -2% to 0%: 1 pts
  - UUP 0% to +1%: 0 pts
  - UUP +1% to +2%: -1 pts
  - UUP > +2% (Dollar Spiking - Headwind): -2 pts

### Q22: Volatility Trend (VIX 1M Check)
- ID: 22
- Category: Credit & Sentiment
- Max Points: 2
- Min Points: -2
- Fields: vix1MonthChange
- Scoring:
  - VIX 1M %Chg < -10% (Calm): 2 pts
  - VIX 1M %Chg -5% to -10%: 1 pts
  - VIX 1M %Chg ± 5%: 0 pts
  - VIX 1M %Chg +5% to +10%: -1 pts
  - VIX 1M %Chg > +10% (Rising Fear): -2 pts

---

## Modifiers

### Euphoria Penalty
- ID: M1

### Breadth Divergence
- ID: M2

### VIX Divergence
- ID: M3

### Yield Curve Risk
- ID: M4

### Momentum Fatigue
- ID: M5
