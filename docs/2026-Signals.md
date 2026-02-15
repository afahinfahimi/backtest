# Module3 - Signals

**Lovable Trade V16 — Updated 2/13/2026**

## Signals Overview
- This module considers all available results and information and issues Action Signals
- Analysis and Market Scores as well as VIX are needed before the Signals are determined and issued.
- Follow the phases below to determine the final signal to be issued
- Each phase/condition has defenition of the condition, Signals about actions to take, and how to manage your current holdings.

## PHASE 1: VIX Override 

If VIX is over 25, that overrides everything else. Take actions below.

| VIX Condition | MS Condition | AS Condition | Signal Title | Signal Details | Manage Holdings | Cash % | Color | 
|---------------|--------------|--------------|--------------|----------------|-----------------|--------|-------|
| VIX ≥ 30 | Any | > 65 | Aggressive Buy | Combine 80% Stocks + 20% QQQ | Keep holdings + Add | 5% Cash | t-green | 
| VIX ≥ 25 | Any | > 65 | Combine 70% Stocks + 30% QQQ | Keep holdings + Add | 20% Cash | t-green |

---

## PHASE 2: Market Score Override

The second group of overrides is based on Market Scores below. They trigger after VIX is checked and it is under 25.

| VIX Condition | MS Condition | AS Condition | Signal Title | Signal Details | Manage Holdings | Cash % | Color | 
|---------------|--------------|--------------|--------------|----------------|-----------------|--------|-------|
| < 25 | < 10 | Any | Weak Market | Sell everything. Ignore AS. | Consider selling most, especially if over invested | 90% |  t-red |
| < 25 | ≥ 80 | Any | No New Buys | Market seems over heated | Set 5% stop loss orders on all. Trim if under 50% cash | 50% | t-yellow |

---

## PHASE 3: Regular Market

If no override triggered, look for the combination of Market and Analysis Scores below

| VIX Condition | MS Condition | AS Condition | Signal Title | Signal Details | Manage Holdings | Cash % | Color | 
|---------------|--------------|--------------|--------------|----------------|-----------------|--------|-------|
| < 25 | 10 to 30 | ≥ 75 | Buy Opportunity | Healthy market to add quality positions | Hold quality and add | 25% | t-green | 
| < 25 | 30 to 55 | ≥ 65 | Buy good stocks | Mormal market good time to add decent stocks | Keep quality add new positions | 25% | t-green |
| < 25 | 55 to 70 | ≥ 65 | Selective Buys | Avoid overextended stocks | Put stop loss | 50% | t-teal | 
| < 25 | 70 to 80 | ≥ 75 | Careful Buy | Overheated market. Stay away of 'expensive' stocks. | Tight stop loss | 50% | t-blue |

---


## PHASE 4: Holding Rules Based on Analysis Score
When overrides apply or other market rules trigger sales, they overrules this phase. 
In a regular market and buying and selling, these are rules that apply to your holdings based on Analysis score changes.

| Current Analysis Score | Action |
|------------------------|--------|
| ≥ 75 | None | 
| 65 to 75 | 10% trailing stop | 
| 55 to 65 | 5% trailing stop | 
| < 55 | Sell immediately |

---

**End of Master Action Table**

