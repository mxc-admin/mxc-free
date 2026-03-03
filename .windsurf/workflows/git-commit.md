---
description: Stage and commit changed files to local git. Use after any editing session or when the user asks to save/commit work.
---

# /git-commit — Stage & Commit

Commit the current working changes to local git with a meaningful message.

## Step 1: Check status

Run `git status` and `git diff --stat` to summarize what changed.
Show the user a brief summary: which files changed, how many insertions/deletions.

## Step 2: Determine commit scope

Ask the user (or infer from context) what scope to commit:
- **All changes** — `git add -A`
- **Specific files** — `git add [files...]`
- **Pine files only** — `git add "*.pine" "**/*.pine"`
- **Libraries only** — `git add pine/libraries/`

If the user already specified files or scope in their request, use that directly without asking.

## Step 3: Craft commit message

Use conventional commit format: `type(scope): description`

Types:
- `feat` — new indicator or major new feature
- `fix` — bug fix
- `refactor` — restructuring without behavior change
- `chore` — tooling, workflows, non-code changes
- `docs` — documentation only
- `perf` — performance improvement

Examples:
- `feat(duo-base): add HMM crossover forecast gating`
- `fix(mxc-ta): correct vel_zscore clamp range`
- `refactor(regime): simplify T2 early-fire logic`
- `chore(workflows): add git-commit workflow`

If the user provides a message, use it verbatim. Otherwise generate one from context.

## Step 4: Stage and commit

// turbo
Run: `git add [scope] && git commit -m "[message]"`

Show the commit hash and summary line on completion.

## Step 5: Confirm

Report:
```
✅ Committed: [hash] — [message]
   [N] files changed, [X] insertions(+), [Y] deletions(-)
```
