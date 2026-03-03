# [Your Project Name] — Claude Code Context

## Project
<!-- TODO: Replace with your project description -->
Pine Script v6 indicators for TradingView. Live trading accounts. Verify everything, respect proven patterns, don't fix what isn't broken.

## Libraries (READ ONLY)
<!-- TODO: List your library files and their import aliases -->
<!-- Example: -->
<!-- - `pine/libraries/your_lib.pine` → imported as `lib` -->

## Key Files
<!-- TODO: List your main indicator/strategy files -->
<!-- Example: -->
<!-- - `pine/your_main_indicator.pine` — description -->

## Current Architecture
<!-- TODO: Describe your indicator architecture -->
<!-- Example: -->
<!-- 1. **Trend Engine** — describe your core trend detection -->
<!-- 2. **Signal** — describe your signal fusion approach -->
<!-- 3. **Risk Logic** — describe entry/exit conditions -->

## Rules (auto-loaded per file type)
`.claude/rules/` — loaded automatically, no need to repeat here:
- `sacred-formulas.md` — proven formulas (NEVER modify)
- `quant-quality.md` — algo rules, constraints, rejected approaches (always)
- `code-quality.md` — Pine patterns, known bugs (globs: *.pine)
- `dev-rules.md` — behavior rules, dual-file update protocol (always)
- `libraries.md` — import conventions, READ ONLY enforcement (globs: pine/libraries/*.pine)
- `strategies.md` — strategy architecture constraints (globs: pine/your_strategy*.pine)
- `indicators.md` — 64-plot limit, constraint ranges (globs: pine/your_ind*.pine)

## Dual-File Rule
`quant-quality.md`, `code-quality.md`, `dev-rules.md` exist in BOTH:
- `.claude/rules/` — CC2 reads this
- `.windsurf/rules/` — Cascade reads this
When updating any of these, update BOTH locations.

## Skills (CLI invocation)
```bash
# TODO: Add your skills once created
# claude -p "/your-skill <file>" --permission-mode dontAsk
```

## Timeframe Context
<!-- TODO: Describe your typical timeframes -->
<!-- Example: Crypto: 2-4 day bars | Traditional: 2w-1m -->
