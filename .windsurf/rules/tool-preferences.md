# Tool Preferences: 3-Tier Architecture

## Tier 1 — Cascade (orchestrator)
File reads, grep, simple edits ≤5 lines, shell commands, memory, Linear, deployment.

## Tier 2 — CC (`mcp0_*`) — standard code intelligence
| Task | Tool |
|------|------|
| Code analysis, reviews, scoring | `mcp0_analyze_code` |
| Code generation, refactoring (>10 lines) | `mcp0_refactor_code` |
| Multi-file coordinated changes | `mcp0_multi_file_edit` |
| Web research, documentation | `mcp0_web_search` |
| Parallel independent operations | `mcp0_batch_tool` |

## Tier 3 — CC2 (`mcp1_claude_code`) — full Claude Code Max delegation
Use when:
- User explicitly says **"use cc2"**
- Heavy workflows: `/indicator-review`, `/deep-bug`, full indicator build from scratch
- Task requires autonomous multi-file exploration (unknown scope)
- Claude Code needs to run scripts, validators, or bash autonomously

> **Always prepend workFolder:** `"Your work folder is /Users/YOUR_USERNAME/dev projects/YOUR_PROJECT\n\nTask: ..."`
> Mention `.pine` file paths explicitly to trigger `code-quality.md` auto-loading.
> cc2 auto-loads `.claude/CLAUDE.md` + `.claude/rules/` via `PWD` env (set in mcp_config.json). **Verified working.**
> Timeout: 300s (configured). Prefix `mcp1_` — verify after any Windsurf restart with `/test_cc_config`.
