# Master Score (MS) — Lovable Trade V13
**Updated: February 3, 2026**

---

## Overview

By the time MS is evaluated, SA (stock score) and MC (market score) are already calculated. MS combines them into trading decisions through three layers, evaluated in priority order:

1. **Overrides** — MC or VIX conditions that bypass everything else
2. **Zone Table** — SA + MC rules that don't require calculating MS
3. **MS Formulas** — Calculated score with signals and modifiers

---

## 1. OVERRIDES

Evaluate first. If triggered, skip everything below.

| Condition | Signal | Action |
|-----------|--------|--------|
| VIX ≥ 28 | 🚨 VIX OVERRIDE | Buy QQQ immediately. Ignore SA scores. Fixed position: 50% of T1 max. |
| MC < 20 | 🛑 PANIC | Stand down. All cash. SA unreliable. |

---

## 2. ZONE TABLE (SA + MC Direct Rules)

No MS calculation needed. Evaluate in priority order. Stop at first match.

| Priority | Condition | Signal | Action |
|----------|-----------|--------|--------|
| 1 | MC 20-29 + SA ≥ 55 | 🟢 BUY | Fear. Aggressive buy opportunity. |
| 2 | MC 30-39 + SA ≥ 55 | 🟢 BUY | Oversold. Buy qualifying stocks. |
| 3 | MC 40-49 + SA ≥ 55 | 🟢 BUY | Cautious. Buy qualifying stocks. |
| 4 | MC 50-59 + SA ≥ 65 | 🟡 SELECTIVE BUY | Neutral. Only strong stocks. |
| 5 | MC 60-74 | ⛔ NO NEW BUYS | Overheated. Tighten stops. |
| 6 | MC ≥ 75 | ⛔ NO NEW BUYS | Euphoria. Take profits. |

**When multiple stocks qualify:** Use MS Standard to rank. Buy highest MS first.

**Note:** MC alone is sufficient for QQQ decisions. If MC signals BUY and you're buying QQQ (not individual stocks), SA is not required.

---

## 3. MS FORMULAS

Calculate MS after overrides and zone table are checked. Two formulas run simultaneously for comparison and optimization.

### MS Standard
```
MS = (MC + 3 × SA) / 4
```

- **Purpose:** SA-weighted quality score. Higher = better overall stock + market combination.
- **Rounded** to whole number.

### MS Standard Signals

| MS Range | Signal |
|----------|--------|
| ≥ 70 | BUY |
| 60-69 | LEAN BUY |
| 50-59 | HOLD |
| 40-49 | LEAN SELL |
| < 40 | SELL |

### MS Contrarian (Display Only)
```
MS = SA + 0.75 × (100 - MC)
```

- **Purpose:** Alternative ranking view. Rewards buying quality stocks during market fear.
- **NOT used for signals.** Displayed for comparison only.

| SA | MC | Standard | Contrarian | Interpretation |
|----|----|----|------|----------------|
| 80 | 30 | 68 | 133 | Great stock + fear |
| 80 | 50 | 73 | 118 | Great stock + neutral |
| 80 | 75 | 79 | 99 | Great stock + hot market |
| 65 | 30 | 56 | 118 | Good stock + fear |
| 50 | 30 | 45 | 103 | Average stock + fear |

---

## 4. MS MODIFIERS

Applied to the MS Standard score after calculation, before signals are read.

| Condition | Modifier |
|-----------|----------|
| MC < 30 | +5 |
| MC 30-49 | +3 |
| MC 50-59 | +1 |
| MC ≥ 60 | 0 |
| SA Q23 = Breakout AND MC < 60 | -3 |

**Example:** SA = 65, MC = 35 → Raw MS = (35 + 195) / 4 = 58 → +3 modifier → **MS = 61 (LEAN BUY)**

---

## 5. EXIT RULES

Evaluate in priority order. Stop at first match.

| Priority | Condition | Action |
|----------|-----------|--------|
| 1 | VIX < 18 + QQQ profit > 10% | Exit VIX Override QQQ position only |
| 2 | Down -20% from entry | Sell — emergency stop loss |
| 3 | SA < 45 + down >15% | Sell — deteriorating quality |
| 4 | +20% T1 / +25% T2 / +30% T3 | Sell 50%, let rest run |
| 5 | 60 days held + SA < 55 | Sell — re-evaluation failed |
| 6 | Under 20 days held | Don't exit even if down |

---

## 6. POSITION SIZING

### Tier Limits (Max Position per Stock)

| Tier | Criteria | Max Position |
|------|----------|-------------|
| T1 | SA ≥ 55 + Profitable + Market Cap > $50B | $100,000 |
| T2 | SA ≥ 50 + Profitable + Market Cap > $2B | $50,000 |
| T3 | SA ≥ 50 + Market Cap > $100M + (growth OR small profitable) | $20,000 |
| SELL | Does not qualify for any tier | $0 — Do not buy |

**T3 Qualification Path A (Unprofitable Growth):**
- Unprofitable with at least 2 of 3 growth questions scoring ≥1 pt (Q1, Q2, Q3)
**T3 Qualification Path B (Small Profitable):**
- Profitable with Market Cap $100M–$2B

**Tier Precedence:** If a stock qualifies for multiple tiers, assign the highest tier.
**Note:** Tiers are risk caps, not quality rankings. Score determines quality; tier determines maximum position size based on risk profile.
### Portfolio Concentration Limits
Max 2 positions per restricted sector: Pharma/Medical, Crypto, Mining/Commodities, Oil/Gas/Energy

---

**End of Master Score V13**




