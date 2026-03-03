---
trigger: glob
globs: **/*.pine
---
# Pine Script Code Quality Rules
# Read by: Cascade (Glob: **/*.pine) | Mirror: .claude/rules/code-quality.md

## Conventions

- Use `math.sum()` for summation — NOT `ta.sum()` (deprecated in v6)
- Percentile output: always divide by 100 → `ta.percentrank(value, 100) / 100`
- Import pattern: define your aliases once at the top, never deviate

## Safety Guards (always apply)

- **Division protection**: `result = numerator / math.max(0.01, denominator)`
- **Lookback bounds after smoothing**: ensure adaptive lengths are clamped to `math.max(1, ...)`
- **Timeframe-adaptive period cap**: `math.max(3, math.min(TARGET_DAYS, math.round(TARGET_DAYS / tf_days)))` — prevents blowup on low TFs
- **Rolling sum bar cap**: `math.max(5, math.min(500, math.round(days / tf_days)))` — very long lookbacks on low TFs kill performance

## Series Function Rules

- **Series functions must run every bar** — hoist `ta.stdev`, `ta.sma` etc. outside `if`-blocks. Gate result with ternary, not the calculation.
- **Gating conditions survive parameter tuning** — after any edit, verify ALL gates (timeframe gates, warmup checks) are still present. Gating regression is a common copy-paste bug.

## Known Bugs to Avoid

- **JMA na-propagation**: `jma := e2 + jma` permanently propagates `na`. Protect accumulative var formulas with `nz()` or `na(src) ? prev : calc`.
- **nz() with booleans**: Pine doesn't allow it — use `barstate.isfirst ? false : state[1]` instead.
- **Label tooltips**: `text=""` creates invisible hover target. Use `text="•"` with `textcolor=color.new(color.white, 100)`.
- **Tooltip gates**: always show tooltip, conditionally include content — don't block tooltip when one source is na.

## Visualization Completeness

- Every new event type needs: (1) detection logic, (2) visualization, (3) `alertcondition()`
- Table coloring: use decay-active state for persistence, not transient event flag

## Library var State

- Library function `var` state is SAFE per call site — each call gets independent scope.
- Series self-reference (`float x = ... nz(x[1])`) does NOT work in library functions.

## Prohibited Patterns

- `nz()` with boolean series — Pine doesn't allow it
- `barstate.isconfirmed` omission on signal-generating logic
- Features with <20% likelihood of use — keep code simple
- AI-generated Pine behavior claims without empirical verification in TradingView
