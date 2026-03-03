---
description: Quick mid-session checkpoint commit. Saves all current changes with an auto-generated timestamped message. Use during long editing sessions to avoid losing work.
---

# /git-checkpoint — Quick Checkpoint Save

Save all current changes as a WIP checkpoint commit. No prompts, fast execution.

## Step 1: Stage all changes

// turbo
Run: `git add -A`

## Step 2: Commit with timestamp

// turbo
Run: `git commit -m "checkpoint: wip $(date '+%Y-%m-%d %H:%M')" --allow-empty`

## Step 3: Confirm

Run `git log --oneline -3` and show the last 3 commits so the user can see the checkpoint was saved.

Report:
```
✅ Checkpoint saved: [hash] checkpoint: wip [timestamp]
```

## Notes
- Checkpoint commits can be squashed later with `git rebase -i HEAD~N`
- To undo the last checkpoint (keep changes): `git reset HEAD~1`
- These are local only — use /git-push to sync to remote
