---
description: Push local commits to a remote git repository (GitHub, etc). Use after committing when the user wants to sync to remote.
---

# /git-push — Push to Remote

Push local commits to the configured remote.

## Step 1: Check remote config

Run `git remote -v` to show configured remotes.

If no remote exists, guide the user:
```
No remote configured. To add GitHub remote:
  git remote add origin https://github.com/[username]/[repo].git
  git branch -M main
  git push -u origin main
```
Stop here and ask user to configure remote first.

## Step 2: Check what will be pushed

Run `git log origin/main..HEAD --oneline` (or `git log --oneline -5` if no upstream set).
Show the user the commits that will be pushed.

## Step 3: Push

// turbo
Run: `git push origin main`

If upstream not set yet, run: `git push -u origin main`

## Step 4: Confirm

Report:
```
✅ Pushed to [remote]/[branch]
   [N] commit(s) pushed
```
