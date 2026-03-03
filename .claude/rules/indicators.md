---
globs: ["pine/*.pine"]
---

# Indicator Files — Development Rules

## Plot Limit
- Pine Script has a **64-plot limit PER SCRIPT** (not per chart)
- Dynamic colors count as **2 plots**
- `bgcolor()` and `alertcondition()` do NOT count
- Plan plot budget before adding visual elements

## Constraint Ranges (MUST enforce)
- `atr_pct` ∈ [0.0, 1.0] — ATR percentile
- `atr_vzn` ∈ [0.0, 1.0] — Normalized velocity (0=contracting, 1=expanding)
- `atr_vz` ∈ [-3.0, 3.0] — Raw z-score, clamped
- `val` ∈ [0, 100] — Before percentile ranking
- `valrank` ∈ [0.0, 1.0] — After percentile ranking
<!-- TODO: Add your project-specific constraint ranges -->

## Testing
- Test with realistic constraint values only
- Many "problems" disappear after percentile normalization — verify the full pipeline
- Breakout detection is the edge: low vol + high velocity = money
- Regime transitions (low→high vol, high→low vol) are where profits happen
