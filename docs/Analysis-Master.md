# Stock Analysis Test (SAT)

**Lovable Trade V18 - Updated 2/24/2026**

## SAT Score Overview

- Score each stock provided by the user (via CSV or direct entry).
- Answer each question below and find the points that apply.
- Add all points to calculate the Raw Score and normalize it using the formula at the end of this document.
- Pull the data from connected FMP API. 

**Missing Data Handling:** If data unavailable for any question, do not estimate, follow the rules to assign points:
- For questions with positive-only answers (e.g., 0 to 6): assign middle value (e.g., 3)
- For questions with negative-only answer range: assign 0
- For questions with both positive and negative answer range (e.g., -5 to +5): assign 0
- For penalty questions (max 0): assign 0 (no penalty)

---

## SAT Questions 

### Growth Metrics 

**Q1: Sales Growth**
- Fields: Annual Revenue Growth %, Quarterly Revenue Growth % (YoY)
- Max Points: 6
- Min Points: 0

| Points | Condition | Interpretation |
|--------|-----------|----------------|
| 6 | Annual ≥50% AND Quarterly > Annual | Accelerating Exceptional |
| 5 | Annual ≥50% AND Quarterly > 0 but ≤ Annual | Steady Exceptional |
| 5 | Annual 20-49% AND Quarterly > Annual | Accelerating Strong |
| 4 | Annual 20-49% AND Quarterly > 0 but ≤ Annual | Steady Strong |
| 2 | Annual 1-19% AND Quarterly > 0 | Growing |
| 1 | Annual ≥0 AND Quarterly ≤ 0 | Stalling |
| 1 | Annual <0 AND Quarterly > 0 | Recovering |
| 0 | Annual <0 AND Quarterly ≤ 0 | Declining |

**Q2: Operating Income Growth**
- Fields: Annual Operating Income Growth %, Quarterly Operating Income Growth % (YoY)
- Max Points: 6
- Min Points: 0

| Points | Condition | Interpretation |
|--------|-----------|----------------|
| 6 | Annual ≥50% AND Quarterly > Annual | Accelerating Exceptional |
| 5 | Annual ≥50% AND Quarterly > 0 but ≤ Annual | Steady Exceptional |
| 5 | Annual 20-49% AND Quarterly > Annual | Accelerating Strong |
| 4 | Annual 20-49% AND Quarterly > 0 but ≤ Annual | Steady Strong |
| 2 | Annual 1-19% AND Quarterly > 0 | Growing |
| 1 | Annual ≥0 AND Quarterly ≤ 0 | Stalling |
| 1 | Annual <0 AND Quarterly > 0 | Recovering |
| 0 | Annual <0 AND Quarterly ≤ 0 | Declining |

**Q3: Cash Flow Growth**
- Fields: Annual Operating Cash Flow Growth %, Quarterly Operating Cash Flow Growth % (YoY)
- Max Points: 6
- Min Points: 0

| Points | Condition | Interpretation |
|--------|-----------|----------------|
| 6 | Annual ≥50% AND Quarterly > Annual | Accelerating Exceptional |
| 5 | Annual ≥50% AND Quarterly > 0 but ≤ Annual | Steady Exceptional |
| 5 | Annual 20-49% AND Quarterly > Annual | Accelerating Strong |
| 4 | Annual 20-49% AND Quarterly > 0 but ≤ Annual | Steady Strong |
| 2 | Annual 1-19% AND Quarterly > 0 | Growing |
| 1 | Annual ≥0 AND Quarterly ≤ 0 | Stalling |
| 1 | Annual <0 AND Quarterly > 0 | Recovering |
| 0 | Annual <0 AND Quarterly ≤ 0 | Declining |

### Cyclical Sector Cap
**Applies to Sectors:** Basic Materials, Energy, Mining
**Rule:** For stocks in these sectors, the maximum score for **Q1, Q2, and Q3** is capped at **4 points** each (instead of 6).

**Exception (Breakout Rule):**
If **Q21 (Range Position)** equals **"Breakout"** (Score 4), the cap is lifted, and the stock may earn the full 6 points for growth.

### EPS Growth

**Q12: EPS Growth Prior Year**
- Field: EPS Growth % (Prior Fiscal Year)
- Max Points: 4
- Min Points: 0

| Growth | Points |
|--------|--------|
| ≥100% | 4 |
| ≥50% | 3 |
| ≥25% | 2 |
| >0% | 1 |
| ≤0% | 0 |


---

### Profitability

**Q4: Net Profit Margin**
- Field: Net Profit Margin
- Formula: `Net Profit Margin` = Net Income ÷ Revenue (TTM).
- Max Points: 5
- Min Points: 0

| Condition | Points | Interpretation |
|-----------|--------|----------------|
| ≥30% | 5 | Exceptional |
| ≥20% | 4 | Strong |
| ≥15% | 3 | Good |
| ≥10% | 2 | Moderate |
| ≥5% | 1 | Low |
| <5% | 0 | None |

---

### Momentum 

**Q5: 1-Month Price Change**
- Field: 1-Month Price Change %
- Max Points: 4
- Min Points: 0

| Change | Points |
|--------|--------|
| ≥20% | 4 |
| ≥10% | 3 |
| ≥5% | 2 |
| >0% | 1 |
| ≤0% | 0 |

**Q6: 10-Day Price Change**
- Field: 10-Day Price Change %
- Max Points: 3
- Min Points: 0

| Change | Points |
|--------|--------|
| ≥15% | 3 |
| ≥10% | 2 |
| ≥5% | 1 |
| <5% | 0 |

---

### Weighted Momentum

**Q11: Momentum Magnitude**
- Field: 52-Week Price Change %, 3-Month Price Change %
- Formula: 52W %Chg + 3M %Chg
- Max Points: 3
- Min Points: 0

| Sum | Points | Backtest Win Rate |
|-----|--------|-------------------|
| >150% | 3 | 73% |
| >100% | 2 | 63% |
| >50% | 1 | 55% |
| ≤50% | 0 | 47% |

### Momentum Quality 

**Q22: Momentum Quality**
- Fields: 52-Week %Chg, 3-Month %Chg, 1-Month %Chg, 10-Day %Chg
- Max Points: 2
- Min Points: -1
- **Evaluate in order listed (stop at first match):**

| Pattern | Condition | Points |
|---------|-----------|--------|
| Spike Risk | 10-Day %Chg >20% AND 1-Month %Chg <10% | -1 |
| Smooth | 52-Week %Chg >0 AND 3-Month %Chg >0 AND 1-Month %Chg >0 AND 52-Week %Chg > 3-Month %Chg > 1-Month %Chg > 10-Day %Chg | +2 |
| Accelerating | 3-Month %Chg >0 AND (3-Month %Chg × 4) > 52-Week %Chg | +1 |
| Other | Default | 0 |


---

### Liquidity 

**Q7: 20-Day Average Volume**
- Field: 20-Day Average Volume
- Max Points: 3
- Min Points: 0

| Volume | Points |
|--------|--------|
| ≥1M | 3 |
| ≥500K | 2 |
| ≥200K | 1 |
| <200K | 0 |

---

### Analyst & Institutions

**Q8: Ownership & Coverage**
- Field: Number of Analyst Ratings, Institutional Ownership %
- Conditional Points
- Max Points: 2
- Min Points: 0

| Condition | Points |
|-----------|--------|
| Institutional Ownership % > 0% | +1 |
| Number of Analyst Ratings > 0 | +1 |

---

### Technical 

**Q9: Price vs Moving Averages**
- Field: Current Price, 20-Day SMA, 50-Day SMA
- Max Points: 4
- Min Points: 0

| Position | Points |
|----------|--------|
| Above both 20D & 50D | 4 |
| Above 50D only | 3 |
| Above 20D only | 2 |
| Below both | 0 |


### Range Position

**Q21: %B Position (Bollinger Bands — Momentum)**
- Field: Bollinger Bands %B (Period 20, StdDev 2)
- Max Points: 4
- Min Points: 0

| Position | Points |
|----------|--------|
| Breakout (>100%) | 4 |
| Near top (>95%) | 3 |
| Upper zone (80-95%) | 2 |
| Mid-range (20-80%) | 1 |
| Buy zone (≤20%) | 0 |


---

### Financial Health 

**Q10: Debt-to-Equity Ratio**
- Field: Total Debt / Total Equity (Most Recent Quarter)
- Max Points: 3
- Min Points: -3
- **Evaluate in order listed (stop at first match):**

| D/E Ratio | Points |
|-----------|--------|
| Negative (negative equity) | -3 |
| <0.5 | 3 |
| <1.0 | 2 |
| <2.0 | 1 |
| ≥2.0 | 0 |

---

### Returns 

**Q13: Return on Equity (ROE)**
- Field: Return on Equity (TTM)
- Max Points: 2
- Min Points: 0

| ROE | Points |
|-----|--------|
| ≥20% | 2 |
| ≥10% | 1 |
| <10% | 0 |

**Q14: Return on Assets (ROA)**
- Field: Return on Assets (TTM)
- Max Points: 3
- Min Points: 0

| ROA | Points |
|-----|--------|
| ≥15% | 3 |
| ≥10% | 2 |
| ≥5% | 1 |
| <5% | 0 |

### Trend & Strength 

**Q18: Financial Strength**
- Fields: Net Profit Margin, Return on Equity, Debt/Equity Ratio
- Max Points: 3
- Min Points: 0

| Condition | Points |
|-----------|--------|
| Net Profit Margin ≥20% AND Return on Equity ≥20% AND Debt/Equity Ratio <0.5 | 3 |
| Net Profit Margin ≥10% AND Return on Equity ≥10% AND Debt/Equity Ratio <1.5 | 2 |
| Net Profit Margin ≥0% AND Return on Equity ≥5% AND Debt/Equity Ratio <3.0 | 1 |
| Fails thresholds or missing data | 0 |

---

### Country 

**Q15: Country** 
- Field: Country (from FMP `/api/v3/profile/{symbol}`)
- Max Points: 1
- Min Points: -2

| Tier | Countries | Points |
|------|-----------|--------|
| USA | US-listed domestic companies | +1 |
| Developed | Canada, UK, Netherlands, Germany, France, Japan, Australia, Taiwan, South Korea, Switzerland, Ireland, Israel | 0 |
| China / Emerging Markets | China, Brazil, South Africa, and other EM countries | -2 |

---

### Risk Penalties

**Q16: Cash Burn Risk**
- Fields: Net Profit Margin, Operating Cash Flow (Quarterly), Market Cap
- Max Points: 0
- Min Points: -3

| Condition | Points |
|-----------|--------|
| Profitable (Net Profit Margin ≥ 0%) | 0 |
| Unprofitable BUT Operating Cash Flow (Quarterly) ≥ 0 | 0 |
| Unprofitable + Negative CF BUT Market Cap ≥ $10B | 0 |
| Profit% < 0% AND Operating Cash Flow (Quarterly) < 0 AND Market Cap < $10B | -3 |

**Note:** FMP API provides the full raw number (e.g., 10,000,000,000 for $10B). *Note: Do not treat as thousands.*


**Q17: Deterioration Risk**
- Fields: Quarterly Revenue, Quarterly Operating Income, Quarterly Operating Cash Flow (vs Same Qtr Year Ago)
- Max Points: 0
- Min Points: -3

| Condition | Points |
|-----------|--------|
| Quarterly Revenue < Sales(q-4) AND Quarterly Operating Income < OpIncome(q-4) AND Quarterly Operating Cash Flow < CashFlow(q-4) | -3 |
| Otherwise | 0 |

**Combined Penalty Cap:** If both Q16 and Q17 trigger, apply -4 total (not cumulative)

### Risk Detection

**Q19: Momentum Divergence Penalty**
- Fields: 52-Week Price Change %, 3-Month Price Change %, 1-Month Price Change %, 10-Day Price Change %
- Max Points: 0
- Min Points: -3

| Condition | Points |
|-----------|--------|
| 52-Week Price Change % > 0% AND 3-Month Price Change % < 0% AND 1-Month Price Change % < 0% AND 10-Day Price Change % < 0% | -3 |
| Otherwise | 0 |

---

### Risk Detection - Part 2 

**Q23: High P/E Momentum Trap**
- Fields: P/E Ratio (TTM), 10-Day Price Change %
- Max Points: 0
- Min Points: -4

| Condition | Points |
|-----------|--------|
| P/E Ratio (TTM) > 50 AND 10-Day Price Change < -5% | -4 |
| P/E > 100 (positive only) | -4 |

 Do not Stack Points

**First Match**

**Q27: Short Interest Risk**
- Fields: Short % of Float
- Category: Risk Penalty
- Max Points: 0 
- Min Points: -1
- Logic: High short interest amplifies volatility in both directions.

| Short % Float | Penalty |
|---------------|---------|
| > 20% | -1 |
| ≤ 20% | 0 |

- Data Source: FMP institutional/short interest endpoint
- Rationale: Heavily shorted stocks have unpredictable, amplified moves. For 1-month swing trades, this adds risk regardless of direction.

---

**Q20: Sector Preference**
- Field: Sector (GICS)
- Max Points: 2
- Min Points: -4

| Sector | Points |
|--------|--------|
| Computers and Technology, Finance, Business Services, Aerospace, Defence | +2 |
| Consumer Staples, Consumer Discretionary, Auto-Tires-Trucks, Retail-Wholesale, Medical, Industrial Products, Transportation, Utilities, Construction | +1 |
| Energy, Basic Materials, Mining, Pharma | 0 |
| Crypto-related (Bitcoin miners, crypto exchanges, blockchain companies) | -4 |

**Sector Classification Notes:**
- **Gold/Mining includes:** NEM, GFI, KGC, AU, HMY, CDE, HL, NGD, CGAU, AEM, GOLD, AG
- **Crypto includes:** IREN, MARA, CLSK, RIOT, BITF, WULF, HUT, CIFR, COIN, MSTR, CORZ, BTBT, HIVE, BTDR


---


---



---

**Q24: Biotech Binary Event Burn** 
- Max Points: 0 
- Min Points: -3
- Fields: Sector, 10-Day Price Change %
- Applies to: Medical, Pharma 

| Condition | Points |
|-----------|--------|
| Sector is Medical or Pharma AND 10-Day Price Change % > 15% | -3 |
| Otherwise | 0 |

---

**Q25: Sustained Downtrend**
- Fields: 1-Day Price Change %, 5-Day Price Change %, 1-Month Price Change %
- Max Points: 0 
- Min Points: -3

| Condition | Points |
|-----------|--------|
| 1D < 0% AND 5D < 0% AND 1M < 0% | -3 |
| Otherwise | 0 |

---

**Q26: Sudden Drop / Slide**
- Fields: Historical Daily Close Prices (last 5 trading days)
- **Category:** Risk Penalty
- Max Points: 0 
- Min Points: -6
- **Logic:** Check for abnormal price drops. Evaluate each of the last 3 trading days individually (close-to-close). Also check cumulative 5-day return. Triggered by the HIGHEST matching tier only (no stacking):

| Tier | Condition | Penalty |
|------|-----------|---------|
| Critical | Any single day ≥ 15% drop within last 3 days | -6 |
| Severe | Any single day ≥ 10% drop within last 3 days | -2 |
| Caution | Any single day ≥ 7% drop within last 3 days, OR cumulative 5-day return ≤ -10% | -1 |
| None | No conditions met | 0 |

- **Data Source:** Historical daily prices (last 5 trading days, close prices)
- **Self-Healing:** Clears once the drop day falls outside the 3-day window. If decline continues, the 5-day cumulative condition sustains the Caution tier.
- **Rationale:** Tiered response to abnormal drops. 7%+ warrants caution. 10%+ signals something significant. 15%+ is catastrophic — effectively makes the stock untradeable by score alone.

---



---

**Q28: Sector Performance vs SPY**
- Fields: 1-Month Price Change %, SPY 1-Month Return % (spyChange1m)
- Category: Momentum
- Max Points: +1 
- Min Points: -1
- Logic: Compare stock's 1M return vs its sector average 1M return.

| Condition | Points |
|-----------|--------|
| Outperforms SPY 1-Month Return % by > 10% | +1 |
| Within ±10% of SPY 1-Month Return % | 0 |
| Underperforms SPY 1-Month Return % by > 10% | -1 |

- Data Source: FMP sector performance (spyChange1m) + stock quote

---

**Q29: 5-Day Relative Strength (Alpha)**
- Fields: Stock 5-Day Price Change %, QQQ 5-Day Price Change %
- Formula: Alpha = Stock 5D % minus QQQ 5D %
- Category: Momentum
- Max Points: +3 
- Min Points: -3
- **Evaluate in order listed (stop at first match):**

| Condition | Points |
|-----------|--------|
| Stock UP & Market DOWN (true alpha) | +3 |
| Alpha ≥ +5% (beating market by 5%+) | +2 |
| Alpha ≥ 0% (beating market) | +1 |
| Alpha -5% to 0% (slightly lagging) | 0 |
| Alpha < -5% (badly lagging market) | -2 |
| Stock DOWN & Market UP (stock-specific problem) | -3 |

- Data Source: FMP quote (stock 5D change) + QQQ quote (market 5D change)
- Rationale: Stock move relative to market isolates stock-specific strength (alpha). Stocks up while market is down had 82.1% win rate. Stocks down while market is up had 47.8% win rate. Combined with Q15 change, improved SA correlation from r=0.152 to r=0.173 (+14%).

---

**Q30: Trend Structure (Lower Lows & Lower Highs)**
- Fields: Daily OHLC (last 30 trading days)
- Category: Momentum Bonus
- Max Points: +3
- Min Points: 0

**Calculation:**
1. Find swing highs: days where the high > highs of 2 days before and 2 days after
2. Find swing lows: days where the low < lows of 2 days before and 2 days after
3. Compare last 2-3 swing highs: are they decreasing?
4. Compare last 2-3 swing lows: are they decreasing?
5. Both decreasing → penalty

| Condition | Points |
|-----------|--------|
| Lower highs AND lower lows (2+ swing points each) | +3 |
| Otherwise | 0 |

- Data Source: FMP `/api/v3/historical-price-full/{symbol}` (daily OHLC)
- Rationale: Stocks making lower lows and lower highs are in a structural downtrend regardless of other indicators. Detects topping patterns that momentum questions miss.

---

### Pending Backtest Questions
*These questions are placeholders scoring 0 until backtested and points assigned.*

**Q31: Price-to-Sales Ratio**
- Fields: Price-to-Sales Ratio (TTM), Sector
- FMP Endpoint: `/api/v3/ratios/{symbol}` → `priceToSalesRatio`
- Max Points: 0 (pending)
- Min Points: 0 (pending)
- Note: Requires sector-adjusted thresholds. Do not score until points defined.

---

**Q32: Earnings Surprise**
- Fields: Actual EPS vs Estimated EPS (most recent quarter)
- FMP Endpoint: `/api/v3/earnings-surprises/{symbol}`
- Max Points: 0 (pending)
- Min Points: 0 (pending)
- Note: Measures beat/miss vs consensus, not absolute growth. Not redundant with Q12.

---

**Q33: Gross Margin Trend**
- Fields: Gross Profit / Revenue — current quarter vs prior quarter
- FMP Endpoint: `/api/v3/income-statement/{symbol}` quarterly
- Max Points: +1 (proposed)
- Min Points: 0
- Scoring: +1 if gross margin is improving quarter over quarter. 0 otherwise.

---

**Q34: Insider Buying**
- Fields: Net insider transactions (open market buys vs sells, last 90 days)
- FMP Endpoint: `/api/v3/insider-trading/{symbol}`
- Max Points: 0 (pending)
- Min Points: 0 (pending)
- Note: Filter scheduled/compensation purchases. Look for open market buys only.

---

**Q35: Volume Surge on Up Day**
- Fields: Today's Volume, 20-Day Average Volume, 1-Day Price Change %
- FMP Endpoint: `/api/v3/quote/{symbol}` → `volume`, `avgVolume`
- Max Points: +2 (proposed)
- Min Points: 0
- Scoring: +2 if volume > 2x 20D average AND price up. 0 otherwise.

---

**Q36: Revenue Acceleration**
- Fields: Quarterly Revenue Growth % — last 3-4 quarters
- FMP Endpoint: `/api/v3/income-statement/{symbol}` quarterly
- Max Points: +1 (proposed)
- Min Points: 0
- Scoring: +1 if quarterly revenue growth rate is accelerating (each quarter higher than previous). 0 otherwise.

---

**Q37: 52-Week High Proximity**
- Fields: Current Price, 52-Week High
- FMP Endpoint: `/api/v3/quote/{symbol}` → `price`, `yearHigh`
- Max Points: +1 (proposed)
- Min Points: 0
- Scoring: +1 if stock is within 5% of 52-week high. 0 otherwise.

---

**Q38: Institutional Accumulation**
- Fields: Institutional Ownership % — current quarter vs prior quarter
- FMP Endpoint: `/api/v3/institutional-holder/{symbol}`
- Max Points: +1 (proposed)
- Min Points: 0
- Scoring: +1 if institutional ownership % is increasing quarter over quarter. 0 otherwise.
- Note: Not redundant with Q8 which only checks presence, not trend.

---

### Market Environment

### Market Integration (Applied to each stock equally based on market conditions)

**Note:** These questions use QQQ and market ETF data — not individual stock data. All stocks analyzed on the same day receive the same points from M-01 through M-11. Half-point scoring (0.5x weight) is used to prevent market conditions from overwhelming stock-specific signals.

**Required Data:** QQQ Price, 20D/50D/100D/200D SMAs, 52-Week High/Low, 52-Week %Chg, VIX Level, SPY 1M %Chg, EFA 1M %Chg, XLE 1M %Chg, GLD 1M %Chg, IWM 1M %Chg, XLY 1M %Chg, XLP 1M %Chg

---

**M-01: VIX Level**
- Field: VIX Current Price (^VIX)
- Max Points: 3
- Min Points: -3

| VIX Level | Points |
|-----------|--------|
| ≥ 30 | +3 |
| 24–29 | +1 |
| 21–24 | +2 |
| 17–21 | +1 |
| 14–17 | 0 |
| < 14 | -3 |

---

**M-02: QQQ Price vs Moving Averages**
- Fields: QQQ Price, QQQ 50D SMA, QQQ 200D SMA
- Max Points: 1.5
- Min Points: -1

| Position | Points |
|----------|--------|
| Above 200MA only (below 50MA — pullback within uptrend) | +1.5 |
| At/near both MAs (±1%) | +1 |
| Below both 50MA and 200MA | +0.5 |
| Above both 50MA and 200MA (extended) | -0.5 |
| Below 200MA only (above 50MA) | -1 |

---

**M-03: Trend Confirmation (50MA–200MA Spread)**
- Fields: QQQ 50D SMA, QQQ 200D SMA
- Formula: `(50D SMA - 200D SMA) / 200D SMA × 100`
- Max Points: 2
- Min Points: -1

| Spread % | Points |
|----------|--------|
| > 5% (overextended uptrend) | -1 |
| 3% to 5% (healthy uptrend) | +2 |
| 1% to 3% (mild uptrend) | +1.5 |
| 0% to 1% (flat/converging) | 0 |
| -5% to 0% (below, recovering) | 0 |
| ≤ -5% (deep downtrend) | -1 |

---

**M-04: QQQ 52-Week Strength**
- Field: QQQ 52-Week Price Change %
- Max Points: 2
- Min Points: -1.5

| 52W Change | Points |
|------------|--------|
| -10% to 0% (slight loss — best opportunity) | +2 |
| 0% to 10% (early recovery) | +1 |
| 10% to 20% (good gain) | +0.5 |
| < -20% (severe loss) | +0.5 |
| ≥ 20% (extended) | -0.5 |
| -20% to -10% (moderate loss — weak) | -1.5 |

---

**M-05: QQQ Range Position**
- Fields: QQQ Price, QQQ 52-Week High, QQQ 52-Week Low
- Formula: `(Price - 52W Low) / (52W High - 52W Low)`
- Max Points: 1.5
- Min Points: -1.5

| Range Position | Points |
|----------------|--------|
| < 20% (near 52W low) | +1.5 |
| 20–40% | +1 |
| 40–60% (mid-range) | +0.5 |
| 60–80% | +1 |
| > 80% (near 52W high — extended) | -1.5 |

---

**M-06: International Markets (EFA vs SPY)**
- Fields: EFA 1-Month %Chg, SPY 1-Month %Chg
- Formula: `EFA 1M %Chg - SPY 1M %Chg`
- Max Points: 1.5
- Min Points: -1

| Spread | Points |
|--------|--------|
| EFA lags SPY by 0–3% (slight US lead — best) | +1.5 |
| EFA leads SPY by 0–3% | +0.5 |
| EFA lags SPY by > 3% (US isolation) | +0.5 |
| EFA leads SPY by > 3% (global strength) | 0 |
| EFA within ±1% (neutral) | -1 |

---

**M-07: Commodities Trend (XLE + GLD)**
- Fields: XLE 1-Month %Chg, GLD 1-Month %Chg
- Definitions: "Up" = > +3%. "Down" = < -3%. "Stable" = -3% to +3%.
- Max Points: 0.5
- Min Points: -0.5

| Condition | Points |
|-----------|--------|
| XLE Down AND GLD Up (risk-off — buy opportunity) | +0.5 |
| XLE Down AND GLD Stable | 0 |
| XLE Down AND GLD Down | 0 |
| Both Stable / Mixed | 0 |
| XLE Up AND GLD Up | 0 |
| XLE Up AND GLD Stable | 0 |
| XLE Up AND GLD Down (risk-on — extended) | -0.5 |

---

**M-08: Small-Cap Breadth (IWM vs QQQ)**
- Fields: IWM 1-Month %Chg, QQQ 1-Month %Chg
- Formula: `IWM 1M %Chg - QQQ 1M %Chg`
- Max Points: 1.5
- Min Points: -1

| Spread | Points |
|--------|--------|
| IWM beats QQQ by > 3% (broad risk appetite) | +1.5 |
| Within ±3% (neutral) | 0 |
| IWM lags QQQ by > 3% (flight to safety) | -1 |

---

**M-09: Sector Rotation (XLY vs XLP)**
- Fields: XLY 1-Month %Chg, XLP 1-Month %Chg
- Formula: `XLY 1M %Chg - XLP 1M %Chg`
- Max Points: 0.5
- Min Points: -0.5

| Spread | Points |
|--------|--------|
| XLY lags XLP by > 3% (defensive rotation) | 0 |
| Within ±3% (neutral) | +0.5 |
| XLY beats XLP by > 3% (consumer confidence — extended) | -0.5 |

---

**M-10: Short-Term Trend (20D–50D MA Spread)**
- Fields: QQQ 20D SMA, QQQ 50D SMA
- Formula: `(20D SMA - 50D SMA) / 50D SMA × 100`
- Max Points: 1.5
- Min Points: -0.5

| Spread % | Points |
|----------|--------|
| -2% to -1% (mild dip — best entry) | +1.5 |
| -5% to -2% (pullback) | +1 |
| ≤ -5% (deep short-term weakness) | +0.5 |
| -1% to +1% (flat) | +0.5 |
| > +5% (extreme extension) | +0.5 |
| +1% to +2% (mild extension) | 0 |
| +2% to +5% (extended) | -0.5 |

---

**M-11: Medium-Term Trend (20D–100D MA Spread)**
- Fields: QQQ 20D SMA, QQQ 100D SMA
- Formula: `(20D SMA - 100D SMA) / 100D SMA × 100`
- Max Points: 1.5
- Min Points: -0.5

| Spread % | Points |
|----------|--------|
| -2% to -1% (mild dip — best entry) | +1.5 |
| -1% to +1% (flat/converging) | +1 |
| ≤ -5% (deep medium-term weakness) | +0.5 |
| -5% to -2% (pullback) | +0.5 |
| +1% to +2% (mild extension) | +0.5 |
| > +5% (extreme extension) | 0 |
| +2% to +5% (extended) | -0.5 |

---

## Final Score Calculation
- **Raw Score** = Sum of all question points (Q1–Q38 + M-01 through M-11)

**Current Config Reference:**
- **Q1–Q30 (Stock):** Max +70 / Min -42
- **Q31–Q38 (Pending Backtest):** Max 0 / Min 0
- **M-01 (VIX):** Max +3 / Min -3
- **M-02–M-11 (Market, 0.5x weight):** Max +9 / Min -7.5
- **Total Max Raw Score:** 82 points
- **Total Min Raw Score:** -52.5 points
- **Span:** 134.5 points

**Normalization Formula:**
`((Raw Score + 52.5) / 134.5) × 100`

---

**Changes from V17 to V18:**
- SA Score Color Codes moved to Signals module
- Alerts Section details moved to Signals module
- Dynamic normalization formula replaced with static version
- Q28 (Low Float Risk) removed — zero predictive value, confirmed by backtest
- Q30 (Trend Structure) flipped from -3 penalty to +3 bonus — backtested: 75% WR vs 65.3% for clean stocks at 80+, 3.9:1 winner-to-FP ratio
- Q31–Q38 added as placeholder questions scoring 0 — pending backtest data before points assigned
- M-01 (VIX Level) added — integer scoring, -3 to +3
- M-02–M-11 added: 10 Market Integration questions (half-point scoring, 0.5x weight)
- Non-linear scoring derived from backtest of 81,222 stock observations against 1-month forward returns
- Normalization formula updated: `((Raw + 52.5) / 134.5) × 100`

---

**End of Stock Analysis Test Instructions**
