---
description: Example skill template. Copy this folder to create a new skill. Skills are Claude Code sub-agents invoked via CLI for specialized tasks.
---

# Example Skill — Template

This is a template. Copy `.claude/skills/example-skill/` to `.claude/skills/your-skill-name/` and fill in.

## Purpose
[What this skill does — 1 sentence]

## Usage
```bash
claude -p "/your-skill-name <target-file>" --permission-mode dontAsk
```

## Invocation from CLAUDE.md
Add to `.claude/CLAUDE.md` Skills section:
```bash
claude -p "/your-skill-name <file>" --permission-mode dontAsk
```

## References
This skill reads from `references/` on every invocation:
- `references/your-knowledge-file.md` — domain knowledge for this skill

## Structure
```
.claude/skills/your-skill-name/
├── SKILL.md              ← This file (skill definition + invocation)
└── references/
    └── your-knowledge.md ← Knowledge files read by this skill
```
