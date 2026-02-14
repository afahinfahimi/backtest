# Signal Engine V16
**Lovable Trade — "The Brain"**
**Updated: February 13, 2026**

---

## Purpose

This file contains **pure decision logic only**. No colors, no tokens, no UI labels.
It consumes pre-calculated scores (SA, MC, VIX, Alerts) and outputs a **Signal Key**.
The Rules file maps each key to its visual representation.

---

## Inputs (assumed available)

| Input | Source | Type |
|-------|--------|------|
| `SA` | SA Test V15 | Number 0–100 |
| `MC` | MC Test V15 | Number 0–100 |
| `VIX` | FMP API (^VIX price) | Number |
| `isHeld` | Portfolio state | Boolean |
| `currentSA` | Latest SA re-score for held stock | Number 0–100 |
| `mcConsecutiveDaysAbove70` | MC history tracker | Integer |
| `trailingStopHit` | Broker/portfolio state | Boolean |
| `alerts` | Alerts engine | Array of alert codes |
| `daysSinceLastSell` | Portfolio state | Integer |
| `priorSellReason` | Portfolio state | String (key) |

---

## Output

A single **Signal Key** string. One of:

`B1` | `B2` | `B3` | `H1` | `H2` | `H3` | `S1` | `S2` | `S3` | `W1` | `X1`

Plus metadata object:

```
{
  key: "B1",
  capitalDeploy: 0.80,       // only for O1a/O1b
  maxPositions: 5,            // context-dependent
  stopPercent: null,           // null = no stop
  saThreshold: 75,            // minimum SA for this signal
  reEntryBlocked: false,      // true if after-sell lockout active
  reason: "VIX Override 25+"  // human-readable reason for logs
}
```

---

## Decision Logic

**Evaluate top-to-bottom. First match wins. Stop evaluating.**

---

### PHASE 1: KILL SWITCH

```
IF alerts CONTAINS "SEC":
  → Key: X1
  → reason: "SEC Kill Switch"
  → STOP
```

---

### PHASE 2: OVERRIDES (VIX + Panic + Euphoria)

**Priority: O1 > O2 > O3**

```
IF VIX >= 30:
  → Key: B1
  → capitalDeploy: 0.95
  → saThreshold: 75
  → maxPositions: unlimited (SA 75+ first, remainder QQQ)
  → reason: "VIX Override 30+ — Deploy 95%"
  → STOP

IF VIX >= 25:
  → Key: B1
  → capitalDeploy: 0.80
  → saThreshold: 75
  → maxPositions: unlimited (SA 75+ first, remainder QQQ)
  → reason: "VIX Override 25+ — Deploy 80%"
  → STOP

IF MC < 10:
  → Key: X1
  → reason: "Panic — All Cash"
  → STOP

IF MC >= 70 AND mcConsecutiveDaysAbove70 >= 3:
  → Key: W1
  → stopPercent: 5
  → reason: "Euphoria 3+ days — No new buys, 5% stops on all"
  → STOP
```

---

### PHASE 3: RE-ENTRY LOCKOUT CHECK

```
IF priorSellReason == "SA_below_55":
  IF SA < saThreshold(currentMCzone) OR MC NOT IN [Fear, Normal]:
    → reEntryBlocked: true

IF priorSellReason == "stop_hit":
  IF daysSinceLastSell < 5:
    → reEntryBlocked: true

IF priorSellReason == "panic_O2":
  IF MC < 10:
    → reEntryBlocked: true
```

If `reEntryBlocked == true`:
```
  → Key: W1
  → reason: "Re-entry blocked — [priorSellReason] lockout active"
  → STOP
```

---

### PHASE 4: HELD POSITIONS (Re-Score)

Only runs if `isHeld == true`.

```
IF currentSA >= 75:
  → Key: H1
  → stopPercent: null
  → reason: "Hold with conviction"
  → STOP

IF currentSA >= 65:
  → Key: H2
  → stopPercent: 10
  → reason: "Hold with caution — 10% trailing stop"
  → STOP

IF currentSA >= 55:
  → Key: H3
  → stopPercent: 5
  → reason: "Hold tight — 5% trailing stop"
  → STOP

IF currentSA < 55:
  → Key: S1
  → reason: "SA below 55 — Sell immediately"
  → STOP
```

**Trailing Stop Check (runs alongside hold logic):**

```
IF trailingStopHit == true:
  → Key: S2
  → reason: "Trailing stop triggered"
  → STOP
```

---

### PHASE 5: NEW POSITION EVALUATION (Buy / Watch / Wait)

Only runs if `isHeld == false` AND `reEntryBlocked == false`.

```
IF MC >= 10 AND MC < 30:
  IF SA >= 75:
    → Key: B1
    → saThreshold: 75
    → maxPositions: 5
    → reason: "Fear zone buy — SA 75+"
    → STOP
  ELSE:
    → Key: W1
    → reason: "Fear zone — SA below 75 threshold"
    → STOP

IF MC >= 30 AND MC < 55:
  IF SA >= 65:
    → Key: B2
    → saThreshold: 65
    → maxPositions: 10
    → reason: "Normal zone buy — SA 65+"
    → STOP
  ELSE:
    → Key: W1
    → reason: "Normal zone — SA below 65 threshold"
    → STOP

IF MC >= 55 AND MC < 70:
  IF SA >= 75:
    → Key: B3
    → reason: "Extended zone — Watchlist only (SA 75+)"
    → STOP
  ELSE:
    → Key: W1
    → reason: "Extended zone — No new buys"
    → STOP

IF MC >= 70:
  → Key: W1
  → reason: "Euphoria zone — No new buys"
  → STOP
```

---

### PHASE 6: DISCRETIONARY SELL SIGNALS

These run as **secondary evaluations** on held positions (do not override Phase 4 forced sells).

```
IF isHeld AND currentSA >= 65 AND currentSA < 75 AND mcZoneTransition == "Normal→Extended":
  → Key: S3
  → reason: "Discretionary — Weak hold entering Extended zone"

IF isHeld AND unrealizedGainPercent >= 30:
  → Key: S3
  → reason: "Discretionary — Consider partial profit (+30%)"

IF isHeld AND monthsHeld >= 3 AND saTrendDirection == "declining":
  → Key: S3
  → reason: "Discretionary — 3+ months with declining SA"
```

---

## Stock Selection Rules (When B1 or B2 triggers)

These are filtering/sorting rules applied to the buy list, not individual signal logic.

```
1. Sort candidates by SA descending
2. Apply SA minimum: 75 (Fear) or 65 (Normal)
3. Max 2 stocks per sector
4. Reject any stock with SA < 55 regardless of other factors
5. Position sizing: Equal weight across qualifying stocks
```

---

## MC Zone Helper

Utility function — returns zone string from MC score.

```
getZone(MC):
  IF MC < 10:     return "Panic"
  IF MC < 30:     return "Fear"
  IF MC < 55:     return "Normal"
  IF MC < 70:     return "Extended"
  return "Euphoria"
```

---

## Re-Score Frequency Rules

| Condition | Action |
|-----------|--------|
| Normal conditions | Re-score all holdings weekly (Monday or Friday close) |
| MC crosses zone boundary | Re-score within 24 hours |
| VIX spikes above 20 | Re-score all holdings immediately |

---

## Validation Status

| Rule | Key(s) | Status |
|------|--------|--------|
| VIX Override O1 | B1 (override) | ✅ MC-level validated |
| Panic Cash O2 | X1 | ⚠️ Rare (bottom 3%) |
| Euphoria Stop O3 | W1 | ⚠️ Unvalidated |
| Fear Buy | B1 | ✅ Strongly validated |
| Normal Buy | B2 | ✅ Partially validated |
| Extended Hold | B3/W1 | ✅ Validated |
| Hold Tiers | H1/H2/H3 | ❌ Unvalidated |
| Sell Rules | S1/S2/S3 | ❌ Unvalidated |
| Re-entry Lockouts | W1 | ❌ Unvalidated |

---

**End of Signal Engine**
