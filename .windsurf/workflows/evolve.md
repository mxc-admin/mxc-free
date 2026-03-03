---
description: Consolidate accumulated session learnings into skills and rules. Run periodically (weekly or after 5+ /learn sessions) to promote patterns to permanent architecture.
---

# /evolve — Knowledge Consolidation

Review all accumulated learnings across reference files, identify patterns, and promote the most important ones to rules or skills. This is the compaction step that prevents reference files from becoming bloated and ensures the best knowledge becomes permanent.

## Step 1: Read all reference files

Read these files in full:

**Skill knowledge (if skills are configured):**
<!-- TODO: Add your skill reference file paths here -->
<!-- Example: -->
<!-- - `.claude/skills/signal-researcher/references/rejected-signals.md` -->
<!-- - `.claude/skills/indicator-scorer/references/scoring-rubric.md` -->

**Current rules (to avoid duplication):**
- `.claude/rules/sacred-formulas.md`
- `.claude/rules/quant-quality.md`
- `.claude/rules/code-quality.md`
- `.claude/rules/dev-rules.md`
- `.claude/rules/indicators.md`
- `.claude/rules/strategies.md`

**Project context:**
- `.claude/CLAUDE.md`

## Step 2: Identify consolidation opportunities

Look for these patterns across all files:

**A. Promote to rule** — if a pattern appears in reference files AND has been confirmed multiple times, it belongs in `.claude/rules/` where it is always enforced:
- Example: A constraint violation that keeps appearing → add to `code-quality.md`
- Example: A proven formula that's referenced everywhere → confirm it's in `sacred-formulas.md`

**B. Retire stale rejections** — if a rejected signal is more than 6 months old AND conditions have changed (new library functions, new architecture), flag it for reconsideration rather than permanent rejection

**C. Merge duplicates** — if the same constraint or decision appears in multiple files, keep the most complete version, delete the rest

**D. Update scoring rubric** — if skill reference files have new high-score examples, check that scoring criteria still correctly describes what makes them excellent

**E. Identify new skill candidates** — if there is a repeated task in sessions that has no skill yet (e.g., "how to refactor a library function"), flag it as a candidate for a new SKILL.md

**F. CLAUDE.md drift** — check if `CLAUDE.md` still accurately describes the current architecture. If the project has evolved, update it.

## Step 3: Propose changes

Before making any edits, report the proposed changes:

```
## /evolve Proposal

### Promote to rules:
- [rule file] + [what to add] — reason: [why it's now a permanent rule]

### Retire/update stale entries:
- [file] line [X]: [entry] — suggest: [update or remove]

### Merge duplicates:
- [entry] appears in [file A] and [file B] — keep [A/B], delete other

### Scoring rubric updates:
- [dimension]: update criteria because [reason]

### New skill candidates:
- [task name]: appears [N] times in sessions, would benefit from SKILL.md

### CLAUDE.md updates:
- [section]: outdated, should read [new content]

### Nothing to change:
- [any category that is clean]
```

## Step 4: Execute approved changes

After user confirms the proposal (or approves all):

1. Make each edit using the edit tool
2. Keep the git mental model in mind — these are append/update operations, not rewrites
3. For any new rule promoted from reference files, add it in the existing format of that rule file
4. For CLAUDE.md changes, preserve the lean ~55-line target — don't expand it
5. **Dual-file rule**: `code-quality.md`, `quant-quality.md`, `dev-rules.md` exist in BOTH `.claude/rules/` AND `.windsurf/rules/` — update BOTH when promoting to these files

## Step 5: Confirm

```
## /evolve Complete

### Files updated:
- [file]: [what changed]

### Net result:
- Rules added: N
- Reference entries retired: N  
- Duplicates merged: N
- New skill candidates flagged: N

### Next /evolve: suggested after [N more /learn sessions or date]
```
