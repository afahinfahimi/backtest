STAR RATING
2026-02-16
Copy Markdown
## Star Rating (1–5 ★)

A simple scoring system that awards 1 point for each criterion met:

| Criterion | Condition |
|-----------|-----------|
| P/E Ratio | Between 0 and 25 |
| Net Margin | > 15% |
| ROE | > 15% |
| D/E Ratio | Between 0 and 1 |
| Revenue Growth | > 10% |

**Total stars = count of criteria met (0–5).**

---

### Key Metrics Source

- **Market Cap, P/E, D/E** → from `keyMetrics` or `ratios` (TTM variants prioritized)
- **Net Margin, ROE** → from `ratios` (`netProfitMarginTTM`, `returnOnEquityTTM`)
- **Revenue/EPS/FCF Growth** → manually computed YoY from `incomeAnnual` and `cashFlowAnnual` arrays (current year vs previous year)

The rating is purely informational and independent of the SA scoring engine.
SA Scoring Engine — Q8 & Q29 Replaced
2026-02-16
Copy Markdown
## SA Scoring Engine Update — Q8 & Q29 Replaced

**Date:** February 16, 2026  
**Affects:** Module-2 (Analysis), Backtesting, Vault Documentation

---

### Q8: Market Cap Liquidity Tier *(replaces Analyst & Institutional Ownership)*

**Old Q8:** Ownership & Coverage (0–2 pts) — Based on analyst count and institutional ownership percentage.  
**Problem:** FMP does not reliably provide analyst count or institutional ownership data for historical backtesting. Values often returned as 0 or null, causing "Missing data" scores.

**New Q8:** Market Cap Liquidity Tier (0–2 pts)
- **Fields:** Market Cap, 20-Day Average Volume
- **Category:** Liquidity / Coverage Proxy

| Condition | Points |
|-----------|--------|
| Market Cap > $10B AND Avg Volume > 1M | +2 |
| Market Cap > $2B OR Avg Volume > 500K | +1 |
| Otherwise | 0 |

- **Data Source:** FMP `/api/v3/profile/{symbol}` (mktCap), FMP `/api/v3/quote/{symbol}` (avgVolume)
- **Rationale:** Market cap and volume serve as reliable proxies for institutional interest and coverage. Both fields are fully available in FMP for present and historical backtesting.

---

### Q29: Relative Strength vs SPY — 1-Month *(replaces Sector Performance vs Peers)*

**Old Q29:** Sector Performance vs Peers (-1 to +1 pts) — Compared stock's 1-month return against sector average.  
**Problem:** Required maintaining peer lists and pulling dozens of tickers per sector historically. Data was inconsistent and unavailable for backtesting.

**New Q29:** Relative Strength vs SPY — 1-Month (-1 to +1 pts)
- **Fields:** 1-Month Price Change %, SPY 1-Month Price Change %
- **Category:** Momentum

| Condition | Points |
|-----------|--------|
| Outperforms SPY by > 10% | +1 |
| Within ±10% | 0 |
| Underperforms SPY by > 10% | -1 |

- **Data Source:** FMP `/api/v3/stock-price-change/{symbol}` (1M) + SPY 1M change
- **Rationale:** SPY provides a clean, always-available benchmark. Complements Q30 (5-day alpha vs QQQ) with a 1-month market-relative view.

---

### Other Notable Changes in This Update

#### Nullish Coalescing Fix (All Questions)
- **Problem:** JavaScript `||` operator treated legitimate `0` values as falsy, causing fields like volume and analyst count to fall through to `null`.
- **Fix:** Replaced `||` with `??` (nullish coalescing) across all data mapping in both live analysis and backtest engines.

#### Rule Processor Guard (Q11, Q29, Q30)
- **Problem:** The rule processor's `computeDerived` step was overwriting values already calculated during the `preComputeSADerived` phase (e.g., momentum sums, SPY relative strength, QQQ alpha).
- **Fix:** Added a guard in `rule-processor.ts` to skip derived field computation when a value already exists, preserving backtest-specific calculations.

#### Backtest Engine — SPY Data Fetch
- **Change:** The backtest engine now fetches SPY historical data alongside the target symbol to compute accurate `spyChange1m` for Q29 scoring at any historical date.

---

### Score Impact Summary

| Question | Old Max | New Max | Old Min | New Min | Change |
|----------|---------|---------|---------|---------|--------|
| Q8 | 2 | 2 | 0 | 0 | Same range, different inputs |
| Q29 | +1 | +1 | -1 | -1 | Same range, different inputs |

**Total SA score range unchanged:** Max Raw = 70, Min Raw = -42, Span = 112.  
**Normalization formula unchanged:** ((Raw + 42) / 112) × 100.
