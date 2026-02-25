
# Stock Analysis Test (SAT)

**Lovable Trade V19 - Updated 2/24/2026**

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

### Growth 

#### Q1: Sales Growth
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

#### Q2: Operating Income Growth
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

#### Q3: Cash Flow Growth
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

##### Cyclical Sector Cap
**Applies to Sectors:** Basic Materials, Energy, Mining
**Rule:** For stocks in these sectors, the maximum score for **Q1, Q2, and Q3** is capped at **4 points** each (instead of 6).

**Exception (Breakout Rule):**
If **Q13 (Range Position)** equals **"Breakout"** (Score 4), the cap is lifted, and the stock may earn the full 6 points for growth.

#### Q4: EPS Growth
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

#### Q5: Net Profit Margin
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

#### Q6: 1-Month Price Change
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

#### Q7: 10-Day Price Change
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

#### Q8: Weighted Momentum Magnitude
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

#### Q9: Momentum Quality
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

#### Q10: 20-Day Average Volume
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

#### Q11: Ownership & Coverage
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

#### Q12: Price vs Moving Averages
- Field: Current Price, 20-Day SMA, 50-Day SMA
- Max Points: 4
- Min Points: 0

| Position | Points |
|----------|--------|
| Above both 20D & 50D | 4 |
| Above 50D only | 3 |
| Above 20D only | 2 |
| Below both | 0 |


#### Q13: Range %B Position (Bollinger Bands — Momentum)
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

#### Q14: Debt-to-Equity Ratio
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

#### Q15: Return on Equity (ROE)
- Field: Return on Equity (TTM)
- Max Points: 2
- Min Points: 0

| ROE | Points |
|-----|--------|
| ≥20% | 2 |
| ≥10% | 1 |
| <10% | 0 |

#### Q16: Return on Assets (ROA)
- Field: Return on Assets (TTM)
- Max Points: 3
- Min Points: 0

| ROA | Points |
|-----|--------|
| ≥15% | 3 |
| ≥10% | 2 |
| ≥5% | 1 |
| <5% | 0 |

#### Q17: Financial Strength
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

#### Q18: Country
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

#### Q19: Cash Burn Risk
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

#### Q20: Deterioration Risk
- Fields: Quarterly Revenue, Quarterly Operating Income, Quarterly Operating Cash Flow (vs Same Qtr Year Ago)
- Max Points: 0
- Min Points: -3

| Condition | Points |
|-----------|--------|
| Quarterly Revenue < Sales(q-4) AND Quarterly Operating Income < OpIncome(q-4) AND Quarterly Operating Cash Flow < CashFlow(q-4) | -3 |
| Otherwise | 0 |

**Combined Penalty Cap:** If both Q19 and Q20 trigger, apply -4 total (not cumulative)

#### Q21: Momentum Divergence Penalty
- Fields: 52-Week Price Change %, 3-Month Price Change %, 1-Month Price Change %, 10-Day Price Change %
- Max Points: 0
- Min Points: -3

| Condition | Points |
|-----------|--------|
| 52-Week Price Change % > 0% AND 3-Month Price Change % < 0% AND 1-Month Price Change % < 0% AND 10-Day Price Change % < 0% | -3 |
| Otherwise | 0 |
 

#### Q22: High P/E Momentum Trap
- Fields: P/E Ratio (TTM), 10-Day Price Change %
- Max Points: 0
- Min Points: -4

| Condition | Points |
|-----------|--------|
| P/E Ratio (TTM) > 50 AND 10-Day Price Change < -5% | -3 |
| P/E > 100 (positive only) | -4 |

**First Match**
Do not Stack Points

#### Q23: Short Interest Risk
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

#### Q24: Sector Preference
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

#### Q25: Biotech Binary Event Burn*
- Max Points: 0 
- Min Points: -3
- Fields: Sector, 10-Day Price Change %
- Applies to: Medical, Pharma 

| Condition | Points |
|-----------|--------|
| Sector is Medical or Pharma AND 10-Day Price Change % > 15% | -3 |
| Otherwise | 0 |

---

#### Q26: Sustained Downtrend
- Fields: 1-Day Price Change %, 5-Day Price Change %, 1-Month Price Change %
- Max Points: 0 
- Min Points: -3

| Condition | Points |
|-----------|--------|
| 1D < 0% AND 5D < 0% AND 1M < 0% | -3 |
| Otherwise | 0 |

---

#### Q27: Sudden Drop / Slide
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

#### Q28: Sector Performance vs SPY
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

#### Q29: 5-Day Relative Strength (Alpha)
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

#### Q30: Trend Structure (Lower Lows & Lower Highs)
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

#### Q31: Price-to-Sales Ratio
- Field: Price-to-Sales Ratio (TTM)
- Max Points: 0
- Min Points: -1

| Condition | Points |
|-----------|--------|
| P/S Ratio > 50 | -1 |
| P/S Ratio ≤ 50 | 0 |
- Note: Requires sector-adjusted thresholds. Do not score until points defined.

---

#### Q32: Earnings Surprise
- Fields: Actual EPS vs Estimated EPS (Most Recent Quarter)
- Max Points: +1
- Min Points: -1

| Condition | Points |
|-----------|--------|
| Actual EPS > Estimated EPS (Beat) | +1 |
| Actual EPS = Estimated EPS (In Line) | 0 |
| Actual EPS < Estimated EPS (Miss) | -1 |
| No data available | 0 |

---

#### Q33: Gross Margin Trend
- Fields: Gross Profit / Revenue — Current Quarter vs Prior Quarter
- Max Points: +1
- Min Points: 0

| Condition | Points |
|-----------|--------|
| Gross Margin improving QoQ | +1 |
| Otherwise | 0 |

---

#### Q34: Insider Buying
- Fields: Net Insider Transactions (Open Market Buys vs Sells, Last 90 Days)
- Max Points: +1
- Min Points: -1
- Note: Filter scheduled/compensation purchases. Open market buys/sells only.

| Condition | Points |
|-----------|--------|
| Net Insider Buying (Buys > Sells) | +1 |
| Neutral / No Data | 0 |
| Net Insider Selling (Sells > Buys) | -1 |

---

#### Q35: Volume Surge on Up/Down Day
- Fields: Today's Volume, 20-Day Average Volume, 1-Day Price Change %, Current Price, 52-Week High, 52-Week Low
- Max Points: +2
- Min Points: -2
- Evaluate in order listed (stop at first match):

| Condition | Points |
|-----------|--------|
| Volume ≥ 2x Average AND Price Up AND Within 5% of 52-Week High | +2 |
| Volume ≥ 2x Average AND Price Up | +1 |
| Volume ≥ 2x Average AND Price Down AND Within 5% of 52-Week Low | -2 |
| Volume ≥ 2x Average AND Price Down | -1 |
| Otherwise | 0 |

---

#### Q36: Revenue Acceleration
- Fields: Quarterly Revenue Growth % — Last 3-4 Quarters
- Max Points: +1
- Min Points: -1

| Condition | Points |
|-----------|--------|
| Revenue Growth Rate Accelerating (Each Quarter Higher Than Previous) | +1 |
| Flat / Insufficient Data | 0 |
| Revenue Growth Rate Decelerating (Each Quarter Lower Than Previous) | -1 |

---

#### Q37: 52-Week High/Low Proximity
- Fields: Current Price, 52-Week High, 52-Week Low
- Max Points: +1
- Min Points: -1

| Condition | Points |
|-----------|--------|
| Within 5% of 52-Week High | +1 |
| Within 5% of 52-Week Low | -1 |
| Otherwise | 0 |

---

#### Q38: Institutional Accumulation
- Fields: Institutional Ownership % — Current Quarter vs Prior Quarter
- Max Points: +1
- Min Points: -1

| Condition | Points |
|-----------|--------|
| Institutional Ownership % Increased by ≥ 1% QoQ | +1 |
| Institutional Ownership % Decreased by ≥ 1% QoQ | -1 |
| Change < 1% either direction / No Data | 0 |

---

#### Q39: Free Cash Flow Yield
- Fields: Free Cash Flow (TTM), Market Cap
- FMP Endpoint: `/api/v3/key-metrics/{symbol}` → `freeCashFlowYield`
- Formula: `FCF / Market Cap × 100`
- Max Points: +2
- Min Points: -2

| Condition | Points |
|-----------|--------|
| FCF Yield ≥ 8% | +2 |
| FCF Yield ≥ 4% | +1 |
| FCF Yield 0% to 4% | 0 |
| FCF Yield -5% to 0% | -1 |
| FCF Yield < -5% | -2 |

---

#### Q40: Float Turnover
- Fields: 20-Day Average Volume, Float Shares
- FMP Endpoint: `/api/v3/profile/{symbol}` → `floatShares` + `/api/v3/quote/{symbol}` → `avgVolume` (both already fetched)
- Formula: `(Avg Volume / Float Shares) × 100`
- Max Points: +1
- Min Points: 0

| Condition | Points |
|-----------|--------|
| Float Turnover ≥ 2% daily | +1 |
| Float Turnover < 2% | 0 |

---

#### Q41: Post-Earnings Price Reaction
- Fields: Last Earnings Date, Stock Price 1 Day Before Earnings, Stock Price 1 Day After Earnings
- FMP Endpoints: `/api/v3/earnings-surprises/{symbol}` (date) + `/api/v3/historical-price-full/{symbol}` (prices)
- Formula: `((Price Day After - Price Day Before) / Price Day Before) × 100`
- Max Points: +2
- Min Points: -2
- Note: Skip if last earnings date > 90 days ago. Assign 0.

| Condition | Points |
|-----------|--------|
| Post-earnings gap ≥ +5% | +2 |
| Post-earnings gap > 0% | +1 |
| Post-earnings gap 0% to -5% | 0 |
| Post-earnings gap ≤ -5% | -2 |

---

### Final Score Calculation

**Raw Score** = Sum of all question points (Q1–Q41)

**Current Config Reference:**
- **Max Raw Score:** 86 points
- **Min Raw Score:** -50 points (Q19+Q20 combined cap of -4 applied)
- **Span:** 136 points

**Normalization Formula:**
`((Raw Score + 50) / 136) × 100`

---

**End of Stock Analysis Test**









