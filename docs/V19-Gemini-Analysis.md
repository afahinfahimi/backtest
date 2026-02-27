# Module-2 - Analysis 

**Lovable Trade V19 - Optimized for Win Rate & Macro Alpha**

## Stock Analysis (SA) Score Overview

- Score each stock provided by the user (via CSV or direct entry).
- Answer each question below and find the points that apply.
- Add all points to calculate the Raw Score and normalize it using the formula at the end of this document.
- Pull the data from connected FMP API. 

**Missing Data Handling:** - For positive-only answers (e.g., 0 to 12): assign middle value.
- For negative-only or penalty ranges: assign 0 (no penalty).

---

## Stock Analysis Score Questions 

### Growth Metrics (High Weight)

**Q1: Sales Growth**
- Max Points: 12
- Min Points: 0

| Points | Condition | Interpretation |
|--------|-----------|----------------|
| 12 | Annual ≥50% AND Quarterly > Annual | Accelerating Exceptional |
| 10 | Annual ≥50% AND Quarterly > 0 but ≤ Annual | Steady Exceptional |
| 10 | Annual 20-49% AND Quarterly > Annual | Accelerating Strong |
| 8 | Annual 20-49% AND Quarterly > 0 but ≤ Annual | Steady Strong |
| 4 | Annual 1-19% AND Quarterly > 0 | Growing |
| 2 | Annual ≥0 AND Quarterly ≤ 0 | Stalling |
| 2 | Annual <0 AND Quarterly > 0 | Recovering |
| 0 | Annual <0 AND Quarterly ≤ 0 | Declining |

**Q2: Operating Income Growth**
- Max Points: 10
- Min Points: 0

| Points | Condition | Interpretation |
|--------|-----------|----------------|
| 10 | Annual ≥50% AND Quarterly > Annual | Accelerating Exceptional |
| 8 | Annual ≥50% AND Quarterly > 0 but ≤ Annual | Steady Exceptional |
| 8 | Annual 20-49% AND Quarterly > Annual | Accelerating Strong |
| 6 | Annual 20-49% AND Quarterly > 0 but ≤ Annual | Steady Strong |
| 3 | Annual 1-19% AND Quarterly > 0 | Growing |
| 1 | Annual ≥0 AND Quarterly ≤ 0 | Stalling |
| 1 | Annual <0 AND Quarterly > 0 | Recovering |
| 0 | Annual <0 AND Quarterly ≤ 0 | Declining |

**Q3: Net Income Growth**
- Max Points: 6
- Min Points: 0

| Points | Condition |
|--------|-----------|
| 6 | Annual ≥20% AND Quarterly > Annual |
| 4 | Annual ≥20% AND Quarterly > 0 |
| 2 | Annual 0-19% |
| 0 | Annual < 0 |

---

### Cash Flow & Efficiency (High Weight)

**Q4: Operating Cash Flow Growth**
- Max Points: 10
- Min Points: 0

| Points | Condition | Interpretation |
|--------|-----------|----------------|
| 10 | Annual ≥50% AND Quarterly > Annual | Exceptional Acceleration |
| 8 | Annual 20-49% AND Quarterly > Annual | Strong Acceleration |
| 6 | Annual >0 AND Quarterly > Annual | Improving |
| 4 | Annual >0 AND Quarterly > 0 but ≤ Annual | Positive but Decelerating |
| 0 | Annual ≤0 OR Quarterly ≤ 0 | Weak/Negative |

**Q5: Net Profit Margin (NPM)**
- Max Points: 5
- Min Points: 0

| Points | Condition |
|--------|-----------|
| 5 | NPM > 20% |
| 3 | NPM 10-20% |
| 1 | NPM 1-10% |
| 0 | NPM ≤ 0% |

**Q6: Return on Equity (ROE)**
- Max Points: 5
- Min Points: 0

| Points | Condition |
|--------|-----------|
| 5 | ROE > 25% |
| 3 | ROE 15-25% |
| 1 | ROE 5-15% |
| 0 | ROE < 5% |

---

### Technical & Momentum

**Q8: Relative Strength (3-Month)**
- Max Points: 7
- Min Points: 0

| Points | Condition | Interpretation |
|--------|-----------|----------------|
| 7 | RS vs S&P 500 ≥15% | Elite Outperformer |
| 4 | RS vs S&P 500 5-14% | Outperformer |
| 2 | RS vs S&P 500 0-4% | Keeping Pace |
| 0 | RS vs S&P 500 <0% | Underperformer |

**Q12: Moving Average Alignment**
- Max Points: 4
- Min Points: 0

| Points | Condition |
|--------|-----------|
| 4 | Price > 20MA > 50MA |
| 2 | Price > 50MA |
| 0 | Price < 50MA |

---

### Risk Penalties (Circuit Breakers)

**Q27: Relative Strength Divergence**
- Min Points: -5

| Points | Condition |
|--------|-----------|
| -5 | RS < -5% AND S&P 500 > 1% (10-day window) |
| 0 | Otherwise |

**Q31: Trend Deterioration (The Deal-Breaker)**
- Min Points: -10

| Points | Condition |
|--------|-----------|
| -10 | Lower highs AND lower lows (Last 30 days) |
| 0 | Otherwise |

---

## Final Score Calculation

1. **Raw Score** = Sum of points from all 31 questions.
2. **Normalized SA Score** = Use the V19 formula below.

**V19 Configuration:**
- **Max Raw Score:** 88 points
- **Min Raw Score:** -52 points
- **Span:** 140 points

**V19 Normalization Formula:**
`SA Score = ((Raw Score + 52) / 140) * 100`

---
**Action Signals:**
- **80 - 100:** Strong Buy (Elite Macro)
- **70 - 79:** Buy / Consider Increasing Position
- **60 - 69:** Hold / Watch Technicals
- **Below 60:** Avoid / Sell
