# MC Master — Market Condition Scoring System
V1 questions marked **(V1)**. Candidate additions marked with source version.
V1 philosophy: **CONTRARIAN** — high fear = buy opportunity, complacency = caution.

---

## Technical Indicators

**Q1: QQQ Price vs Moving Averages (V1)** — CONTRARIAN
-5 to 5 pts | Inputs: QQQ price, sma50, sma200 | Missing: zero
| Position | Pts | Interpretation |
|---|---|---|
| QQQ below both 50MA and 200MA | +5 | Oversold — Buy Opportunity |
| QQQ below 200MA only (above 50MA) | +2 | Partial Oversold |
| QQQ at/near both MAs (±1%) | 0 | Neutral |
| QQQ above 200MA only (below 50MA) | -2 | Partial Extended |
| QQQ above both 50MA and 200MA | -5 | Extended — Caution |

---

**Q2: Trend Confirmation — 50MA vs 200MA Spread (V1)** — CONTRARIAN
-3 to 5 pts | Inputs: QQQ sma50, sma200 | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| MAs flat or converging (±1%) | +5 | Inflection Point |
| 50MA below 200MA, <5% spread | +3 | Early Recovery |
| 50MA above 200MA, <5% spread | +1 | Mild Uptrend |
| 50MA >= 5% above 200MA | -3 | Extended Uptrend |
| 50MA >= 5% below 200MA | -3 | Deep Downtrend |

---

**Q3: RSI Momentum (V1)**
-3 to 5 pts | Inputs: QQQ RSI (14) | Missing: zero
| RSI | Pts | Interpretation |
|---|---|---|
| < 30 | +5 | Oversold Opportunity |
| 30–40 | +1 | Low Momentum |
| 40–50 | +2 | Below Average |
| 50–60 | +3 | Healthy |
| 60–70 | +1 | Above Average |
| > 70 | -3 | Overbought Risk |

---

**Q4: VIX vs 3-Month Average (V1)** — CONTRARIAN
-5 to 5 pts | Inputs: VIX 3-Month Price Change % | Missing: zero
| VIX 3M %Chg | Pts | Interpretation |
|---|---|---|
| > +20% | +5 | VIX spiking — Buy Opportunity |
| +10% to +20% | +3 | VIX rising |
| -10% to +10% | 0 | VIX near avg |
| -20% to -10% | -3 | VIX falling |
| < -20% | -5 | VIX well below avg — Complacency |

---

**Q5: VIX Absolute Level (V1)** — CONTRARIAN
-3 to 5 pts | Inputs: VIX current price | Missing: zero
| VIX Level | Pts | Interpretation |
|---|---|---|
| > 22 | +5 | High Fear — Buy Opportunity |
| 14–22 | 0 | Normal Range |
| < 14 | -3 | Complacency — Caution |

---

**Q6: QQQ 52-Week Strength (V1)** — CONTRARIAN
-3 to 5 pts | Inputs: QQQ 52-Week Price Change % | Missing: zero
| 52W Change | Pts | Interpretation |
|---|---|---|
| -10% to 0% | +5 | Slight Loss — Best Buy Opportunity |
| 0% to 10% | +3 | Slight Gain — Early Recovery |
| -20% to -10% | +1 | Moderate Loss |
| < -20% | 0 | Severe Loss |
| 10% to 20% | 0 | Good Yearly Gain |
| >= 20% | -3 | Strong Yearly Gain — Extended |

---

**Q7: MACD Score (V1)** — CONTRARIAN
-3 to 3 pts | Inputs: QQQ MACD Histogram (12, 26, 9) | Missing: zero
*(Contrarian: Sell signal = good, Buy signal = extended)*
| Signal | Direction | Pts |
|---|---|---|
| Sell | Strengthening | +3 |
| Sell | Weakening | +3 |
| Sell | Weakest (Near Zero) | 0 |
| Buy | Weakest (Near Zero) | 0 |
| Buy | Weakening | -3 |
| Buy | Strengthening | -3 |

---

**Q8: QQQ Range Position (V1)**
-2 to 3 pts | Inputs: QQQ price, 52W High, 52W Low | Missing: zero
_rangePos = (price - 52wLow) / (52wHigh - 52wLow)
| Range Position | Pts | Interpretation |
|---|---|---|
| < 0.10 (Bottom 10%) | +3 | Near Support — Bounce Potential |
| 0.10–0.45 | +1 | Lower Half |
| 0.45–0.55 | 0 | Near Middle |
| 0.55–0.90 | +1 | Upper Half |
| > 0.90 (Top 10%) | -2 | Near Resistance — Extended |

---

**Q18: VIX Trend 5D** *(candidate — from V2 Simple Engine)*
-2 to 2 pts | Inputs: vixChange5D | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| vixChange5D < -3 | +2 | Fear declining fast |
| vixChange5D >= -3 AND vixChange5D <= 3 | 0 | Stable |
| vixChange5D > 3 | -2 | Fear rising fast |

---

## Macro Indicators

**Q9: GDP Growth Proxy — SPY 3M (V1)** — CONTRARIAN
-3 to 3 pts | Inputs: SPY 3-Month Price Change % | Missing: zero
| SPY 3M %Chg | Pts | Interpretation |
|---|---|---|
| Negative | +3 | Contraction — Buy Opportunity |
| 0–6% | 0 | Moderate / Stalling |
| > 6% | -3 | Strong Growth — Extended |

---

**Q10: Unemployment Trend — XLI Momentum (V1)** — CONTRARIAN
-1 to 2 pts | Inputs: XLI 1-Month Price Change % | Missing: zero
| XLI 1M %Chg | Pts | Interpretation |
|---|---|---|
| < -2% | +2 | Industrial Weakness — Buy Opportunity |
| -2% to +3% | 0 | Stable |
| > +3% | -1 | Industrial Expansion — Extended |

*Variant: Some versions (V12) use XLY-XLP spread instead of XLI direct.*

---

**Q13: Treasury Yield Curve (V1)**
0 to 3 pts negative | Inputs: 10Y rate, 2Y rate | Missing: zero
_yieldCurve = 10Y - 2Y
| Spread | Pts | Interpretation |
|---|---|---|
| > 1% | +3 | Healthy Curve |
| 0–1% | +1 | Flat |
| -0.5% to 0% | 0 | Flattening |
| -1% to -0.5% | -2 | Inverted |
| < -1% | -3 | Deeply Inverted/Recession Warning |

---

**Q21: Yield Curve (10Y-2Y) — Tiered** *(candidate — from V12)*
0 to 6.5 pts | Inputs: rate10Y, rate2Y | Missing: zero
_yieldCurve = rate10Y - rate2Y
| Condition | Pts | Interpretation |
|---|---|---|
| _yieldCurve > 1 | +6.5 | Healthy Curve |
| _yieldCurve >= 0 AND <= 1 | +3.5 | Flat |
| _yieldCurve >= -0.5 AND < 0 | +1.5 | Flattening |
| default | 0 | Inverted |

*Note: V2 simple version uses binary: >= 0 → +1, < 0 → -1*

---

**Q23: Federal Reserve Policy — TLT-IEF Spread** *(candidate — from V12)*
0 to 7 pts | Inputs: tlt1mChange, ief1mChange | Missing: zero
_fedSpread = tlt1mChange - ief1mChange
| Condition | Pts | Interpretation |
|---|---|---|
| _fedSpread > 2 | +7 | Dovish / Rates Falling |
| _fedSpread >= 0 AND <= 2 | +4.5 | Neutral-Dovish |
| _fedSpread >= -1 AND < 0 | +2 | Stable |
| default | 0 | Hawkish |

*V1 version of this question (Q11) uses same formula but with negative points for hawkish conditions.*

**Q11: Federal Reserve Policy — TLT-IEF Spread (V1)**
-3 to 3 pts | Inputs: TLT 1M %Chg, IEF 1M %Chg | Missing: zero
_fedSpread = tlt1mChange - ief1mChange
| Spread | Pts | Interpretation |
|---|---|---|
| > 2% | +3 | Dovish / Rates Falling |
| 0% to 2% | +2 | Neutral-Dovish |
| -1% to 0% | 0 | Stable |
| -2% to -1% | -1 | Hawkish lean |
| < -2% | -3 | Hawkish / Rates Rising |

---

## Breadth & Intermarket

**Q11: International Markets — EFA vs SPY (V1)**
-2 to 2 pts | Inputs: EFA 1M %Chg, SPY 1M %Chg | Missing: zero
_spread = efa1m - spy1m
| Spread | Pts | Interpretation |
|---|---|---|
| EFA beats SPY by 1–3% | +2 | Slight Outperformance |
| EFA beats SPY by > 3% | +1 | Global Strength |
| Within ±1% | 0 | Neutral |
| EFA lags SPY by 1–3% | -1 | Slight Underperformance |
| EFA lags SPY by > 3% | -2 | US Isolation |

---

**Q12: Commodities Trend — XLE + GLD (V1)** — CONTRARIAN
-2 to 2 pts | Inputs: XLE 1M %Chg, GLD 1M %Chg | Missing: zero
*(Up = >+3%, Down = <-3%, Stable = between)*
| Condition | Pts | Interpretation |
|---|---|---|
| XLE Down AND GLD Up | +2 | Risk-Off / Fear — Buy Opportunity |
| XLE Down AND GLD Stable | +1 | Mild Risk-Off |
| Mixed / Both Stable | 0 | Neutral |
| XLE Up AND GLD Stable | -1 | Mild Risk-On |
| XLE Up AND GLD Down | -2 | Risk-On — Extended |

---

**Q13: Small-Cap Breadth — IWM vs QQQ (V1)**
-1 to 1 pts | Inputs: IWM 1M %Chg, QQQ 1M %Chg | Missing: zero
| Spread | Pts | Interpretation |
|---|---|---|
| IWM beats QQQ by > 3% | +1 | High Risk Appetite |
| Within ±3% | 0 | Neutral |
| IWM lags QQQ by > 3% | -1 | Flight to Safety |

---

**Q14: Sector Rotation — XLY vs XLP (V1)** — CONTRARIAN
-1 to 1 pts | Inputs: XLY 1M %Chg, XLP 1M %Chg | Missing: zero
| Spread | Pts | Interpretation |
|---|---|---|
| XLY lags XLP by > 3% | +1 | Defensive Rotation — Buy Opportunity |
| Within ±3% | 0 | Neutral |
| XLY beats XLP by > 3% | -1 | Consumer Confidence — Extended |

---

**Q15: Equal-Weight Breadth — RSP vs SPY (V1)** — CONTRARIAN
-1 to 1 pts | Inputs: RSP 1M %Chg, SPY 1M %Chg | Missing: zero
| Spread | Pts | Interpretation |
|---|---|---|
| RSP lags SPY by > 0.5% | +1 | Narrow Rally — Reversal Risk |
| Within ±0.5% | 0 | Neutral |
| RSP beats SPY by 0.5% to 2% | 0 | Mild Breadth — Neutral |
| RSP beats SPY by > 2% | -1 | Broad Participation — Extended |

---

**Q19: Market Breadth % Above 200 SMA** *(candidate — from V2 Simple Engine)*
-2 to 3 pts | Inputs: breadth200 (% of stocks above 200 SMA) | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| breadth200 > 70 | +3 | Strong breadth |
| breadth200 >= 50 AND <= 70 | +1 | Healthy |
| breadth200 >= 30 AND < 50 | -1 | Weak |
| breadth200 < 30 | -2 | Very weak breadth |

---

**Q24: Transportation — IYT vs SPY** *(candidate — from V12)*
0 to 3.5 pts | Inputs: iyt1mChange, spy1mChange | Missing: zero
_iytSpread = iyt1mChange - spy1mChange
| Condition | Pts | Interpretation |
|---|---|---|
| _iytSpread > 2 | +3.5 | Economic Activity High |
| _iytSpread >= 0.5 AND <= 2 | +2 | Positive Signal |
| _iytSpread >= -0.5 AND < 0.5 | +1 | Neutral |
| default | 0 | Transport Lagging |

---

## Credit & Sentiment

**Q16: Credit Spreads — HYG Performance (V1)** — CONTRARIAN
0 to 2 pts | Inputs: HYG 1M %Chg | Missing: zero
| HYG 1M %Chg | Pts | Interpretation |
|---|---|---|
| < -1% | +2 | Credit Stress — Buy Opportunity |
| >= -1% | 0 | No Signal |

---

**Q17: Dollar Index — UUP Trend (V1)**
-2 to 2 pts | Inputs: UUP 1M %Chg | Missing: zero
| UUP 1M %Chg | Pts | Interpretation |
|---|---|---|
| < -2% | +2 | Dollar Weakening — Bullish |
| -2% to 0% | +1 | Mild Weakening |
| 0% to +1% | 0 | Neutral |
| +1% to +2% | -1 | Mild Strengthening |
| > +2% | -2 | Dollar Spiking — Headwind |

---

**Q20: Put/Call Ratio** *(candidate — from V2 Simple Engine)*
-2 to 2 pts | Inputs: putCallRatio | Missing: zero
| Condition | Pts | Interpretation |
|---|---|---|
| putCallRatio > 1.2 | +2 | Extreme fear (contrarian bullish) |
| putCallRatio >= 0.7 AND <= 1.2 | 0 | Neutral |
| putCallRatio < 0.7 | -2 | Extreme greed (contrarian bearish) |

---

**Q22: Credit Spreads HY OAS (Level)** *(candidate — from V2 Simple Engine)*
-2 to 1 pts | Inputs: hyOAS (basis points) | Missing: zero
*(Similar to V1 Q16 which uses HYG price change — this uses actual spread level)*
| Condition | Pts | Interpretation |
|---|---|---|
| hyOAS < 350 | +1 | Tight spreads (risk-on) |
| hyOAS >= 350 AND < 500 | 0 | Normal |
| hyOAS >= 500 | -2 | Wide spreads (stress) |

---

## V12 Modifiers & Vetoes *(architectural additions — not in V1)*

**M1: Euphoria Penalty**
Trigger: RSI > 75 → -8 pts (applied post-scoring)

**M2: Breadth Divergence**
Trigger: QQQ > 50SMA BUT Breadth Bucket Score < 10 → -(12 - Breadth Score) pts

**M3: VIX Divergence**
Trigger: QQQ up >1% AND VIX up >5% simultaneously → -8 pts

**M4: Yield Curve Risk**
Trigger: 10Y-2Y < -0.8% AND RSI > 70 → -5 pts

**M5: Momentum Fatigue**
Trigger: MACD Hist < 0 AND QQQ > 50SMA → -5 pts

**V1 Veto: Extreme Fear**
Trigger: VIX > 35 → Override: Max MC Score 30

**V2 Veto: Market Crash**
Trigger: QQQ 52W < -30% → Override: Max MC Score 20

**V3 Veto: Full Capitulation**
Trigger: QQQ below both MAs AND VIX > 30 → PANIC ZONE override

---

## V9 Modifiers *(contrarian — not in V1)*

**M2: Capitulation Buy Signal**
Trigger: VIX > 20 AND RSI < 40 AND GDP > 6% → +5 pts

**M3: Mean Reversion Setup**
Trigger: 3+ consecutive down months → +3 pts

**M4: GDP Strength Override**
Trigger: GDP > 12% AND RSI < 45 → +5 pts

**M6: Yield Curve Euphoria**
Trigger: Curve < -1% AND RSI > 60 → -3 pts

---

## Philosophy Notes

V1 is **contrarian**: Rewards fear, penalizes complacency.
- High VIX = buy, Low VIX = caution
- QQQ down = buy, QQQ up strong = caution
- XLE Down + GLD Up (risk-off) = buy

V12 is **trend-following** (positive scores): Same questions but points only go 0 to max (no negatives in base scoring — penalties applied separately post-scoring).

When selecting questions, confirm which philosophy is in use before combining questions from both versions.

---

## Summary

| Section | V1 Qs | Candidates | Total |
|---|---|---|---|
| Technical | 8 (Q1–Q8) | 1 (Q18) | 9 |
| Macro | 3 (Q9–Q11, Q13) | 2 (Q21, Q23) | 5 |
| Breadth | 5 (Q11–Q15) | 2 (Q19, Q24) | 7 |
| Credit & Sentiment | 2 (Q16–Q17) | 2 (Q20, Q22) | 4 |
| Modifiers/Vetoes | 0 | 9 (V12 + V9) | 9 |
| **Total** | **17** | **16** | **33** |
