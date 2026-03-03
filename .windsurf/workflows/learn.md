---
description: Extract session learnings and write them to the right reference files. Use at the end of any session where new signals, bugs, architecture decisions, or patterns were discovered.
---

# /learn — Session Pattern Extraction

Extract what was learned this session and write it to the appropriate knowledge files. Run this at the end of any session where something new was decided, tested, rejected, or proven.

## Step 1: Extract from session context

Review the current conversation and identify all learnings in these categories:

**A. Signal ideas tested and their verdict**
- Any signal approach that was analyzed, tested, or backtested
- Include: what it was, what was tested, why it was accepted or rejected
- Target file: your signal research skill references (if configured)
<!-- TODO: e.g., `.claude/skills/signal-researcher/references/rejected-signals.md` -->

**B. Architecture decisions made**
- Any choice about how indicators should be structured
- Include: what the decision was, what alternatives were considered, why this was chosen
- Target file: your skill references or `.claude/CLAUDE.md`
<!-- TODO: e.g., `.claude/skills/signal-researcher/references/architecture-decisions.md` -->

**C. Bugs found and their fix pattern**
- Any Pine Script bug, Pine constraint violation, or code quality issue discovered
- Include: the pattern (not just the one-off fix), so future code avoids it
- Target file: `.claude/rules/code-quality.md` AND `.windsurf/rules/code-quality.md` (update BOTH — shared file)

**D. Proven patterns confirmed**
- Any formula, threshold, or approach that was re-verified in live trading or backtesting
- Include: the exact formula/value and why it's proven
- Target file: `.claude/rules/sacred-formulas.md` or `.claude/CLAUDE.md`

**F. Quant/algo rule changes**
- Any new constraint range, rejected approach, or algo design principle discovered
- Target file: `.claude/rules/quant-quality.md` AND `.windsurf/rules/quant-quality.md` (update BOTH — shared file)

**E. Constraint discoveries**
- Any new constraint range, library function behavior, or Pine Script limitation discovered
- Target file: your validator skill references (if configured) or `.claude/rules/indicators.md`
<!-- TODO: e.g., `.claude/skills/pine-validator/references/constraint-table.md` -->

## Step 2: Write to reference files

For each learning identified:

1. Read the target file first to avoid duplicating existing content
2. Append the new entry in the existing format of that file
3. Keep entries concise: what + verdict + reason (3 lines max per entry)
4. Tag with date if the file has dates

For `rejected-signals.md` use this format:
```
### [Signal Name]
- **What**: Brief description of the approach
- **Tested**: How it was evaluated (backtest/analysis/live)
- **Verdict**: REJECTED
- **Reason**: Why it doesn't work or fit the architecture
```

For `architecture-decisions.md` use this format:
```
### [Decision Title]
- **Decision**: What was chosen
- **Alternatives**: What was rejected
- **Rationale**: Why (1-2 lines)
```

## Step 3: Save to Windsurf memory

For any learning that is critical (proven formula change, new architectural constraint, major bug pattern):
- Use `create_memory` to persist it with appropriate tags
- Check if an existing memory should be updated rather than creating a duplicate

## Step 4: Confirm

Report what was written and where:
```
## /learn Summary

### Written to reference files:
- [file]: [what was added]

### Windsurf memories updated:
- [title]: [what was stored]

### Nothing found to record:
- [any category with no new learnings]
```
