---
globs: ["pine/**/*.pine", "pine/*.pine"]
---
# Pine Script Code Quality Rules
# Read by: CC2 (globs: pine/**/*.pine) | Trimmed mirror: .windsurf/rules/code-quality.md

## Conventions

- Use `math.sum()` for summation — NOT `ta.sum()` (deprecated in v6)
- Percentile output: always divide by 100 → `ta.percentrank(value, 100) / 100`
- Import pattern: define your aliases once at the top, never deviate
- `nz()` replacement: use explicit ternary for booleans: `na(x) ? false : x`

## Safety Guards (always apply)

- **Division protection**: `result = numerator / math.max(0.01, denominator)`
- **Lookback bounds after smoothing**: ensure adaptive lengths are clamped `math.max(1, adaptive_length)`
- **Percentile normalization**: `ta.percentrank(value, lookback) / 100` — always divide by 100
- **Timeframe-adaptive period cap**: `math.max(3, math.min(TARGET_DAYS, math.round(TARGET_DAYS / tf_days)))`
- **Rolling sum bar cap**: `math.max(5, math.min(500, math.round(days / tf_days)))` — 36,000 bars on 1min kills performance

## Series Function Rules

- **Series functions must run every bar** — hoist `ta.stdev`, `ta.sma`, `ta.ema` etc. outside `if`-blocks
- Gate result with ternary AFTER calculation: `result = condition ? computed_value : na`
- **Gating conditions survive parameter tuning** — after any edit, verify ALL gates still present
- Gating regression is a common copy-paste bug — check every `if` block touching series functions

## Known Bugs to Avoid

- **JMA na-propagation**: `jma := e2 + jma` permanently propagates `na`. Protect with `nz()` or `na(src) ? prev : calc`
- **nz() with booleans**: Pine doesn't allow it — use `barstate.isfirst ? false : state[1]` instead
- **Label tooltips**: `text=""` creates invisible hover target. Use `text="•"` with `textcolor=color.new(color.white, 100)`
- **Tooltip gates**: always show tooltip, conditionally include content — don't block tooltip when one source is na
- **AI-generated circular references**: AI sometimes suggests `x = f(x)` patterns in Pine. Test empirically — do not trust claims about Pine behavior without TradingView verification

## Visualization Completeness

- Every new event type needs: (1) detection logic, (2) visualization, (3) `alertcondition()`
- Table coloring: use decay-active state for persistence, not transient event flag (`state_active` not `event_fired`)
- Plot limit: 64 max per script. Dynamic colors = 2 plots. Plan before adding visuals.

## Library var State

- Library function `var` state is SAFE per call site — each call gets independent scope (verified)
- Series self-reference (`float x = ... nz(x[1])`) does NOT work in library functions
- Multiple calls to same library function = independent state, no collision

## Prohibited Patterns

- `nz()` with boolean series — Pine doesn't allow it
- `barstate.isconfirmed` omission on signal-generating logic
- Features with <20% likelihood of use — keep code simple
- AI-generated Pine behavior claims without empirical verification in TradingView
- Caching library state across calls — breaks internal state
