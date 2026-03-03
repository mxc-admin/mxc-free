# Knowledge File Template

Add domain knowledge, reference tables, and proven patterns here.

This file is automatically read by the skill on every invocation.

## How Skills Use Reference Files

Skills load these files on startup to have context before analyzing any target file. Use them for:
- Constraint tables (valid ranges for key variables)
- Proven patterns to look for
- Anti-patterns to flag
- Scoring rubrics

## Example: Constraint Table

| Variable | Range | Notes |
|---|---|---|
| `signal_score` | [0.0, 1.0] | After percentile ranking |
| `atr_pct` | [0.0, 1.0] | ATR percentile |

<!-- TODO: Replace with your project's actual constraint ranges -->
