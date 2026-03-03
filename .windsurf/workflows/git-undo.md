---
description: Undo the last git commit or unstage files. Use when you need to roll back a commit or fix a staging mistake. Handles soft/mixed/hard resets safely.
---

# /git-undo — Undo Last Commit or Unstage

Safely roll back git changes. Always shows what will be undone before executing.

## Step 1: Show current state

Run `git log --oneline -5` and `git status` to display:
- Last 5 commits (so user can see what will be affected)
- Current working tree state

## Step 2: Determine undo mode

Ask the user which mode they want (or infer from context):

| Mode | Command | Effect |
|------|---------|--------|
| **soft** | `git reset --soft HEAD~1` | Undo commit, keep changes **staged** |
| **mixed** (default) | `git reset HEAD~1` | Undo commit, keep changes **unstaged** |
| **hard** | `git reset --hard HEAD~1` | Undo commit, **discard all changes** ⚠️ |
| **unstage** | `git restore --staged <file>` | Unstage specific file(s) only |
| **discard file** | `git restore <file>` | Discard working tree changes for file ⚠️ |

Default to **mixed** if user just says "undo last commit" without specifying.

⚠️ **Hard reset and discard are destructive** — always confirm with the user before running these. Never auto-run them.

## Step 3: Execute

For soft or mixed reset:
```bash
git reset [--soft | ] HEAD~1
git status
```

For hard reset (only after explicit user confirmation):
```bash
git reset --hard HEAD~1
git status
```

For unstaging files:
```bash
git restore --staged <files>
git status
```

## Step 4: Confirm

Report what was undone:
```
✅ Undone: [commit hash] — [commit message]
   Mode: [soft/mixed/hard]
   Working tree: [N files changed / clean]
```

## Notes
- To undo multiple commits: `git reset HEAD~N` (replace N with count)
- To undo a push to remote: requires `git push --force` — proceed with extreme caution
- Checkpoint commits from /git-checkpoint can be bulk-squashed: `git rebase -i HEAD~N`
- If you need to recover a hard-reset commit: `git reflog` shows all recent HEADs
