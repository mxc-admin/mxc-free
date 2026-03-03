# Quant Development Quality Rules
# Read by: Cascade (Always On) | Mirror: .windsurf/rules/quant-quality.md

## Core Principles

1. **Verify library constraints before analyzing** — grep the source, read implementation, confirm return value ranges. Never assume.
2. **Proven formulas are sacred** — Don't fix or optimize without extensive backtesting proof. If it works in live trading, don't touch it.
3. **Check your reference implementation first** — It's the battle-tested baseline for your core metrics.
4. **Code changes require evidence, not intuition** — Show backtests, show edge cases, show why the change improves live trading.
5. **Simplicity beats complexity when edge is equal** — Only add complexity if it materially improves performance.
6. **When in doubt, verify against your reference implementation** — If it's working live, that's your answer.

## Pine Script Hard Limits

- **64-plot limit PER SCRIPT** — not per chart. Dynamic colors count as 2 plots. Plan before adding visuals.
- `bgcolor()` and `alertcondition()` do NOT count toward plot limit.

## Constraint Ranges (ENFORCE — violations compile but trade wrong)

| Variable | Range | Description |
|---|---|---|
| `atr_pct` | [0.0, 1.0] | ATR percentile |
| `atr_vzn` | [0.0, 1.0] | Normalized velocity (0=contracting, 1=expanding) |
| `atr_vz` | [-3.0, 3.0] | Raw z-score, clamped |
| `val` | [0, 100] | Before percentile ranking |
| `valrank` | [0.0, 1.0] | After percentile ranking |

Test with realistic values only.

## Signal & Regime Rules

- **Percentile ranking normalizes extremes** — [0, 100] becomes [0, 1] after ranking. Extreme ranges create better regime separation.
- **Breakout detection is the edge** — Low vol + high velocity = money. Prioritize over stability or elegance.
- **Regime transitions are where profits happen** — Low→high vol (breakouts) and high→low vol (exhaustion). Steady states are noise.
- **Always check if percentile ranking makes the concern irrelevant** — Many problems disappear after normalization.

## Library Rules

- **Read the library code, not the documentation** — Source IS the documentation. Comments can be outdated.
- **Library files are READ ONLY** — Shared across published indicators. Any modification breaks things downstream.

## Rejected Approaches (Do Not Re-Suggest)
<!-- TODO: Add your project's tested-and-rejected approaches here -->
<!-- Example: "RVFI in signal fusion — tested, no P&L improvement" -->

## Reference Files

- Libraries: `pine/libraries/` (READ ONLY)
- Reference implementation: `pine/` — your main indicator files
- Sacred formulas: `.claude/rules/sacred-formulas.md`

**Remember: This code runs on live accounts with real money. Verify everything.**
