# Module3 - Signals

**Lovable Trade V16 — Updated 2/13/2026**

## Signals Overview
- Conditions and rules that determines output format and content of results.
- Analysis and Market Scores as well as VIX are needed before the Signals are determined and issued.
- Holding AS (Analysis Score) and MS (Market Score) and VIX follow the decisoin flowchart below
  

## Decision Flowchart

```
START
  │
  ├─ Check VIX
  │   ├─ VIX ≥ 25 → Aggressive Buy (AS and MS are disregarded)
  │   └─ VIX < 25 → Continue ↓
  │
  ├─ Check MC Zone
  │   ├─ MS < 10 → Sell All. Keep cash ready.
  │   ├─ MS 10–30 → Good market buy stocks with Analysis Score ≥ 75  
  │   ├─ MS 30–55 → Great market buy stocks with Analysis Score ≥ 65 [B2]
  │   ├─ MS 55–70 → Potential over extenssion. No new buys, but hold existing 
  │   └─ MS ≥ 70 (3+ days) → Put a 5% stop loss order on everything 
  │
  ├─ When to seLL stocks you hold as long as above is not an overwrite 
  │   ├─ AS ≥ 75 → Hold, no stop 
  │   ├─ AS 65–75 → 10% trailing stop 
  │   ├─ AS 55–65 → 5% trailing stop 
  │   └─ AS < 55 → Sell immediately 
  │
  └─ END
```
