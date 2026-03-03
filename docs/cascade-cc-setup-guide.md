---
⚠️ BEFORE USING THIS GUIDE:
Find-and-replace in this document before pasting into Cascade:
  YOUR_USERNAME → your actual macOS username (e.g., johndoe)
  YOUR_REPO_URL → git URL for the mxc-claude-mcp server (github.com/your-org/mxc-claude-mcp, or fork it from the original)
  YOUR_PROJECT → your project folder name (e.g., my-project)
  YOUR_SOURCE_FILE → a representative source file in your project root (e.g., main.py, index.ts)
  YOUR_RULES_FILE → a .claude/rules/ filename you want to verify auto-loads (e.g., conventions.md)
  YOUR_RULE_CONTENT → a phrase or value from that rules file, to verify it loaded

After replacing, you can either:
  A) Read it as a reference guide
  B) Execute in two Cascade sessions (required — Windsurf restart is a hard break):
     SESSION 1: Paste Phase 1 Steps 1–3 into a fresh Cascade chat. Cascade runs clone/build/config,
                then stops at the ⚠️ MANUAL STEP restart. Quit and restart Windsurf.
     SESSION 2: Open a new Cascade chat, paste Steps 4–8. Cascade creates all files, memory, and runs tests.
---

# Windsurf Cascade + Claude Code: Complete Setup Guide

> **Status**: Verified working Feb 2026. All 9 health checks pass. Run `/test_cc_config` after any Windsurf restart to re-confirm.

---

## Why This Setup

**The cost problem** — Windsurf's Cascade uses Claude Sonnet by default. Every code review burns Windsurf credits and caps quality at Sonnet. With a **Claude Max subscription** (~$100/month flat rate), you already have Claude Opus with no per-token billing. This setup eliminates the double-billing.

**The capability problem** — Windsurf won't let you use Claude Code natively inside Cascade. Claude Code Max has file system access, runs bash, chains multi-step operations, and auto-loads your `.claude/rules/` on every call. Your project constraints are always active without re-pasting.

### 3-Tier Architecture

```
Cascade (instant, Windsurf native)
  → CC mcp0_* (fast, focused, Opus quality)
    → CC2 mcp1_claude_code (full autonomy, Claude Code Max)
```

- **CC** (`mcp0_*`) — Claude in `--print` mode via a custom Node.js bridge. Cascade provides context, Claude processes and returns. Good for targeted analysis, refactoring, web research. No file system access in the subprocess.
- **CC2** (`mcp1_claude_code`) — `@steipete/claude-code-mcp` wrapper. Runs Claude Code as a true sub-agent: reads files, writes changes, runs scripts, auto-loads `.claude/rules/`. Use for heavy workflows or when you say "use cc2".

Each tier escalates only when needed. Cascade handles ~80% (file reads, simple edits, grep). CC handles ~15% (code analysis, generation, research). CC2 handles ~5% (full delegation, autonomous workflows).

### Architecture Diagram

```
User Request
     │
     ▼
┌─────────────────────────────────────────┐
│   Cascade (Windsurf)                     │  Tier 1 — Orchestrator
│   file reads, grep, edits ≤5 lines      │
│   shell commands, memory, Linear         │
└──────────┬────────────────┬─────────────┘
           │                │
           ▼                ▼
┌──────────────────┐  ┌──────────────────────────────┐
│  CC (mcp0_*)      │  │  CC2 (mcp1_claude_code)       │
│  Tier 2           │  │  Tier 3                       │
│                   │  │                               │
│  Claude Opus via  │  │  Full Claude Code Max         │
│  --print mode     │  │  Reads files autonomously     │
│  Cascade provides │  │  Runs bash, scripts           │
│  context          │  │  Auto-loads .claude/rules/    │
│                   │  │                               │
│  mcp0_analyze_code│  │  Trigger: "use cc2"           │
│  mcp0_refactor_code│  │  OR: heavy workflow           │
│  mcp0_web_search  │  │                               │
│  mcp0_multi_file  │  │  PWD → /YOUR_PROJECT          │
│  mcp0_batch_tool  │  │  Timeout: 300s               │
└──────────────────┘  └──────────────────────────────┘
```

### CC Tool Inventory

**14 Native Tools (instant, zero Claude calls):**

| Tool | Purpose |
|------|---------|
| `read_file` | Read file with optional line range |
| `write_file` | Create or overwrite files |
| `edit_file` | Search/replace within files |
| `list_directory` | List directory contents |
| `find_files` | Find files by glob pattern |
| `search_files` | Grep/ripgrep within files |
| `run_command` | Execute shell commands |
| `get_file_info` | File metadata |
| `create_directory` | Create directories recursively |
| `move_file` | Move or rename files |
| `delete_file` | Delete files or directories |
| `git_status` | Repository status |
| `git_diff` | Diff (staged or unstaged) |
| `git_commit` | Commit staged changes |

**5 Claude-Powered Tools (routes through Claude CLI, Opus quality):**

| Tool | Purpose |
|------|---------|
| `analyze_code` | Deep analysis, reviews, bug finding |
| `refactor_code` | Rewrite code with natural language instructions |
| `multi_file_edit` | Coordinated changes across multiple files |
| `web_search` | Research and documentation lookup |
| `batch_tool` | Parallel independent operations |

### CC2 — Claude Code Max via Steipete Wrapper

`@steipete/claude-code-mcp` runs Claude Code as a proper MCP server. When `PWD` is set, Claude Code auto-discovers `.claude/CLAUDE.md` and `.claude/rules/` on every call. Runs via `npx` — Windsurf downloads automatically.

**Critical**: Never pin to a specific version (e.g., `@1.10.5`). No pinnable versions exist on npm — specific version tags cause "transport closed" errors. Always use `@latest`.

**How to use CC2** — always prepend the work folder:
```
Your work folder is /Users/YOUR_USERNAME/dev projects/YOUR_PROJECT

[Your instruction here]
```

---

# PHASE 0 — MANUAL PREREQUISITES

> Complete these in your terminal BEFORE pasting Phase 1 into Cascade. They require interactive input that Cascade cannot perform.

### Step 0.1 — Install Node.js

⚠️ MANUAL STEP (cannot be automated): Ensure Node.js 18+ is installed.

```bash
node --version
# Should output: v18.x.x or higher
# If missing: brew install node (or https://nodejs.org)
```

### Step 0.2 — Install Claude CLI

⚠️ MANUAL STEP (cannot be automated): Install the Claude CLI globally.

```bash
claude --version
# If missing:
npm install -g @anthropic-ai/claude-code
```

### Step 0.3 — Authenticate Claude CLI

⚠️ MANUAL STEP (cannot be automated): Run `claude auth login` and complete the interactive login flow.

```bash
claude auth login
# Select your Max subscription plan. Decline API credit options — you want flat-rate Max.
claude auth status  # Verify
```

### Step 0.4 — Accept `--dangerously-skip-permissions`

⚠️ MANUAL STEP (cannot be automated): Both CC and CC2 need this accepted once per machine.

```bash
claude --dangerously-skip-permissions
# Read and accept the prompt, then Ctrl+C to exit
```

Without this, Claude-powered tools hang on first invocation.

### Step 0.5 — Verify Claude CLI Works

⚠️ MANUAL STEP (cannot be automated): Confirm Claude responds via print mode.

```bash
echo "Say hello" | claude --print
# Should return a response within 10 seconds
```

> **macOS paths**: MCP config lives at `~/.codeium/windsurf/mcp_config.json`. Claude CLI is typically at `/usr/local/bin/claude` or `/opt/homebrew/bin/claude`. Claude Max gives ~225 Opus messages per 5-hour window; native tools (read, list, edit) have no limit.

---

# PHASE 1 — PASTE INTO CASCADE

> Everything below can be executed by Cascade autonomously. Paste into a fresh Windsurf Cascade chat. Execute each step marked with "Run this command:" or "Create file:" in order.

---

## Step 1 — Clone & Build CC Server (Tier 2)

Run these commands to verify prerequisites:

```bash
node --version
claude auth status
```

Run this command:

```bash
git clone YOUR_REPO_URL "/Users/YOUR_USERNAME/dev projects/mxc-claude-mcp"
```

Run this command:

```bash
cd "/Users/YOUR_USERNAME/dev projects/mxc-claude-mcp" && npm install && npm run build
```

Run this command to verify the build:

```bash
ls "/Users/YOUR_USERNAME/dev projects/mxc-claude-mcp/dist/index.js"
```

> **What is mxc-claude-mcp?** A custom Node.js MCP server bridging Windsurf to the Claude CLI. Registers 19 tools: 14 native (instant) + 5 Claude-powered (Opus quality via `--print` mode). Fix any build errors here before configuring Windsurf — Windsurf won't surface them clearly.

---

## Step 2 — Create MCP Config

Create file `~/.codeium/windsurf/mcp_config.json` with this exact content:

```json
{
  "mcpServers": {
    "cc": {
      "command": "node",
      "args": [
        "/Users/YOUR_USERNAME/dev projects/mxc-claude-mcp/dist/index.js"
      ],
      "disabled": false
    },
    "cc2": {
      "command": "npx",
      "args": ["-y", "@steipete/claude-code-mcp@latest"],
      "disabled": false,
      "env": {
        "CLAUDE_CLI_NAME": "claude",
        "MCP_CLAUDE_DEBUG": "false",
        "MCP_TOOL_TIMEOUT": "300000",
        "PWD": "/Users/YOUR_USERNAME/dev projects/YOUR_PROJECT"
      }
    },
    "linear": {
      "disabled": false,
      "serverUrl": "https://mcp.linear.app/sse"
    },
    "memory": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-memory"],
      "disabled": false,
      "env": {
        "MEMORY_FILE_PATH": "/Users/YOUR_USERNAME/.windsurf-memory/memory.jsonl"
      }
    }
  }
}
```

> **Notes**:
> - `MCP_TOOL_TIMEOUT: 300000` — 5 minutes. Required for large generation tasks.
> - `PWD` — sets Claude Code's working directory. This is how `.claude/rules/` gets auto-loaded.
> - `linear` and `memory` are optional — remove if not using.
> - **`alwaysAllow` is NOT supported by Windsurf** — Claude Desktop field, Windsurf rejects it.
> - **Why NOT `claude mcp serve`**: Subagents spawned via `claude mcp serve` fail to inherit file system permissions ([#5465](https://github.com/anthropics/claude-code/issues/5465)). The custom CC server and steipete wrapper both bypass this.

---

## Step 3 — Restart Windsurf

⚠️ MANUAL STEP (cannot be automated): Fully quit and restart Windsurf now. The MCP config is only loaded on startup. After restarting, open a new Cascade chat and continue from Step 4.

---

## Step 4 — Create `.windsurfrules`

Create or update file `/Users/YOUR_USERNAME/dev projects/YOUR_PROJECT/.windsurfrules` — add this block at the very top of the file (before any existing content):

```markdown
## Tool Routing (MANDATORY)
- Code analysis, reviews, refactoring, generation, web research → `mcp0_*` cc tools
- Mechanical edits ≤5 lines, file reads, shell commands → Cascade native tools
- Heavy workflows OR "use cc2" → `mcp1_claude_code` (Claude Code Max — full autonomy, loads .claude/rules/ automatically)
- Always prepend: `"Your work folder is /Users/YOUR_USERNAME/dev projects/YOUR_PROJECT\n\n"` before cc2 prompts

---
```

> `.windsurfrules` is injected as `<user_rules>` — highest priority, marked "MUST ALWAYS FOLLOW". Keep the routing section at the top, ≤6 lines.

---

## Step 5 — Create Tool Preferences

Create directory `.windsurf/rules/` if it doesn't exist, then create file `/Users/YOUR_USERNAME/dev projects/YOUR_PROJECT/.windsurf/rules/tool-preferences.md` with this content:

```markdown
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
- Heavy workflows: deep analysis, full builds from scratch, multi-file investigation
- Task requires autonomous multi-file exploration (unknown scope)
- Claude Code needs to run scripts, validators, or bash autonomously

> **Always prepend workFolder:** `"Your work folder is /Users/YOUR_USERNAME/dev projects/YOUR_PROJECT\n\nTask: ..."`
> cc2 auto-loads `.claude/CLAUDE.md` + `.claude/rules/` via `PWD` env. **Verified working.**
> Timeout: 300s. Prefix `mcp1_` confirmed Feb 2026 — verify after any Windsurf restart.
```

> **Why three enforcement layers**: `.windsurfrules` alone achieves ~90% routing compliance. Adding `tool-preferences.md` + memory brings it to ~99%. Explicit "use cc2" / "use cc" = ~100%.

---

### Step 5b — Configure Rules Activation

In Windsurf Settings → Rules, set the activation mode for each `.windsurf/rules/` file you create:
- Domain/always-on rules → **Always On**
- Language/file-type rules → **Glob**: `**/*.your-extension`
- Development behavior rules → **Always On**
- `tool-preferences.md` → **Always On**

---

## Step 5c — Scaffold `.claude/` Directory (skip if already exists)

> CC2 auto-discovers `.claude/CLAUDE.md` and all `.claude/rules/` files when `PWD` env is set. Without these files, Test 2 (rules auto-loading) will fail.

Run this command to check if `.claude/` already exists:

```bash
ls "/Users/YOUR_USERNAME/dev projects/YOUR_PROJECT/.claude/"
```

If the directory does not exist, create file `/Users/YOUR_USERNAME/dev projects/YOUR_PROJECT/.claude/CLAUDE.md` with this content:

```markdown
# Project Context

## Architecture
[Describe your project architecture — what it does, key components, main patterns]

## Libraries / Dependencies
[Key libraries and any usage constraints]

## Rules
- `.claude/rules/` files are auto-loaded by CC2 based on globs — see individual rule files
```

Create file `/Users/YOUR_USERNAME/dev projects/YOUR_PROJECT/.claude/rules/YOUR_RULES_FILE` with this content:

```markdown
# [Rule file title]

[Replace this with your project-specific rules and constraints.]
[Example value to verify loading: YOUR_RULE_CONTENT]
```

> Populate these files with actual project rules after setup. See the Project Rules Structure reference section below for format and best practices.

---

## Step 6 — Create Test Workflow

Create directory `.windsurf/workflows/` if it doesn't exist, then create file `/Users/YOUR_USERNAME/dev projects/YOUR_PROJECT/.windsurf/workflows/test_cc_config.md` with this content:

```markdown
---
description: Daily verification that all MCP servers (cc, cc2, linear, memory) are working correctly with correct prefixes and capabilities
---

# /test_cc_config — Daily MCP Health Check

## Overview
Runs 9 tests covering prefix verification, rules loading, tool capabilities, integration, and setup guide currency. Takes ~2 minutes. Run after any Windsurf restart or config change.

---

## Test 1 — CC2 prefix discovery
Call `mcp1_claude_code` with minimal prompt:
```
Your work folder is /Users/YOUR_USERNAME/dev projects/YOUR_PROJECT

Reply with exactly one line: "CC2 ONLINE mcp1"
```
**Pass:** responds with "CC2 ONLINE mcp1"
**Fail:** unknown tool → prefix shifted. Check Windsurf MCP panel for cc2 tool name. Update `mcp1_` references in `.windsurfrules` and `tool-preferences.md` to the new prefix.

---

## Test 2 — CC2 rules auto-loading (PWD env)
Call `mcp1_claude_code`:
```
Your work folder is /Users/YOUR_USERNAME/dev projects/YOUR_PROJECT

From your loaded .claude/rules/YOUR_RULES_FILE — quote one specific rule or value from it. One sentence.
```
**Pass:** mentions YOUR_RULE_CONTENT (a value only found in that file, not generic knowledge)
**Fail:** "I don't have that" or generic answer → `.claude/` not found. Check `PWD` env in `mcp_config.json`, verify it points to the correct project dir.

---

## Test 3 — CC2 autonomous file access
Call `mcp1_claude_code`:
```
Your work folder is /Users/YOUR_USERNAME/dev projects/YOUR_PROJECT

Read YOUR_SOURCE_FILE and tell me: how many lines does it have and what is in the first comment or header?
```
**Pass:** returns line count and actual content from the file header
**Fail:** can't read file → subprocess CWD issue or file permissions. Check `claude --dangerously-skip-permissions` was accepted.

---

## Test 4 — CC2 timeout headroom (medium task)
Call `mcp1_claude_code`:
```
Your work folder is /Users/YOUR_USERNAME/dev projects/YOUR_PROJECT

List all source files in the root directory with their line counts. Sort by size descending.
```
**Pass:** returns full sorted table, no timeout
**Fail:** timeout error → `MCP_TOOL_TIMEOUT` not applied. Verify `mcp_config.json` cc2 entry has `"MCP_TOOL_TIMEOUT": "300000"` and restart Windsurf.

---

## Test 5 — CC (`mcp0_*`) analysis tool
Call `mcp0_analyze_code`:
```
path: /Users/YOUR_USERNAME/dev projects/YOUR_PROJECT/YOUR_SOURCE_FILE
query: Summarize what this file does in 2 sentences.
```
**Pass:** returns a coherent 2-sentence summary of the file
**Fail:** tool error or timeout → cc server issue. Check `ps aux | grep "node.*mxc-claude-mcp"`. Rebuild if needed: `cd "/Users/YOUR_USERNAME/dev projects/mxc-claude-mcp" && npm run build`

---

## Test 6 — CC web search
Call `mcp0_web_search`:
```
query: software engineering best practices for code review
```
**Pass:** returns relevant results about code review or engineering practices
**Fail:** tool error → cc server down (see Test 5 fix)

---

## Test 7 — Linear server
Call `mcp3_list_teams` (no parameters needed)

**Pass:** returns your team entry
**Fail:** unknown tool → linear prefix shifted. Check Windsurf MCP panel for current linear prefix, update any hardcoded `mcp3_` references.

---

## Test 8 — Memory server
Call `mcp4_search_nodes`:
```
query: architecture
```
**Pass:** returns nodes or empty result (no error) — both valid, confirms server is alive
**Fail:** unknown tool → memory prefix shifted. Check panel for current prefix.

---

## Test 9 — Setup guide is current
Call `mcp1_claude_code`:
```
Your work folder is /Users/YOUR_USERNAME/dev projects/YOUR_PROJECT

Find the setup guide in the docs/ directory and validate it reflects the current architecture. Check all of the following and report PASS or FAIL for each:

1. cc2 prefix — guide says `mcp1_claude_code` (not mcp2_ or any other prefix)
2. version pinning — guide uses `@steipete/claude-code-mcp@latest` (NOT a specific version like @1.10.5)
3. timeout — guide shows MCP_TOOL_TIMEOUT: 300000
4. PWD env — guide shows PWD set to the project directory
5. 3-tier routing — guide describes Cascade → mcp0_* → mcp1_claude_code tiers (not old 2-tier)
6. linear prefix — guide says mcp3_* for linear
7. memory prefix — guide says mcp4_* for memory
8. no deprecated references — guide does NOT mention `mcp2_claude_code` as the cc2 prefix
9. /test_cc_config — guide references this workflow as the daily health check

Report: PASS/FAIL for each point. Final verdict: GUIDE CURRENT or GUIDE STALE.
```
**Pass:** all 9 points PASS, final verdict GUIDE CURRENT
**Fail:** any point fails → guide has stale content. Update the failing section in `docs/cascade-cc-setup-guide.md` to match current verified values.

---

## Expected Results Summary

| # | Test | Tool | Expected |
|---|---|---|---|
| 1 | CC2 prefix | `mcp1_claude_code` | "CC2 ONLINE mcp1" |
| 2 | Rules loaded | `mcp1_claude_code` | Specific rule content from YOUR_RULES_FILE |
| 3 | File access | `mcp1_claude_code` | Line count + header from YOUR_SOURCE_FILE |
| 4 | Timeout headroom | `mcp1_claude_code` | Full sorted table, no timeout |
| 5 | CC analysis | `mcp0_analyze_code` | 2-sentence summary of YOUR_SOURCE_FILE |
| 6 | CC web search | `mcp0_web_search` | Code review best practices results |
| 7 | Linear | `mcp3_list_teams` | Your team entry |
| 8 | Memory | `mcp4_search_nodes` | No error |
| 9 | Guide current | `mcp1_claude_code` | GUIDE CURRENT, all 9 points pass |

**All 9 pass = 100% confident, ready to work.**

---

## Quick Fix Reference

| Symptom | Likely cause | Fix |
|---|---|---|
| `mcp1_claude_code` unknown | Prefix shifted on restart | Find new cc2 tool name in panel, update `.windsurfrules` + `tool-preferences.md` + memory |
| Rules not loaded (T2 fail) | PWD env wrong or missing | Verify `"PWD": "/Users/YOUR_USERNAME/dev projects/YOUR_PROJECT"` in cc2 env config |
| File access denied (T3 fail) | `--dangerously-skip-permissions` not accepted | Run `claude --dangerously-skip-permissions` in terminal once, accept, Ctrl+C |
| Timeout (T4 fail) | MCP_TOOL_TIMEOUT not 300000 | Verify cc2 env in `mcp_config.json`, restart Windsurf |
| `mcp0_*` tools fail (T5/T6) | cc server not running | Rebuild: `cd "/Users/YOUR_USERNAME/dev projects/mxc-claude-mcp" && npm run build`, restart Windsurf |
| `mcp3_*` unknown (T7) | Linear prefix shifted | Find in panel, no file changes needed (linear tools not hardcoded in routing rules) |
| `mcp4_*` unknown (T8) | Memory prefix shifted | Find in panel, update memory tool calls if needed |
| Guide stale (T9) | Guide not updated after config change | Open `docs/cascade-cc-setup-guide.md`, find the failing section, update to match current verified values |

---

## Notes
- **Prefix shifting** is the most common issue after restarts — cc2 prefix is most likely to shift
- cc (`mcp0_*`) is the most stable — custom Node.js server, prefix never shifts
- Run this workflow at start of any session where MCP tools will be heavily used
- T9 catches guide drift — if you update `.windsurfrules`, `mcp_config.json`, or routing philosophy but forget to update the guide, T9 will flag it
```

---

## Step 7 — Create Windsurf Memory

Tell Cascade to create this memory by pasting this instruction:

```
Create a memory titled "Tool Routing (MANDATORY)" with this content:

## Tool Routing (MANDATORY)
- Code analysis, reviews, refactoring, generation, web research → mcp0_* cc tools
- Mechanical edits ≤5 lines, file reads, shell commands → Cascade native tools
- Heavy workflows OR "use cc2" → mcp1_claude_code (Claude Code Max, loads .claude/rules/ automatically)
- Always prepend workFolder before cc2 prompts

Verified prefixes (Feb 2026): cc=mcp0_*, cc2=mcp1_claude_code, linear=mcp3_*, memory=mcp4_*
⚠️ Verify cc2 prefix after every Windsurf restart with /test_cc_config
```

---

## Step 8 — Verify Setup

Run `/test_cc_config` to execute the 9-test health check created in Step 6. All 9 tests should pass.

> **Tool prefix instability**: Windsurf assigns `mcp0_`, `mcp1_`... prefixes sequentially to enabled+working servers. Prefixes can shift when servers are added, removed, or fail to start. After any restart, run `/test_cc_config` to verify. Quick manual check: call `mcp1_claude_code: "Reply with exactly: CC2 ONLINE mcp1"` — if tool not found, locate the new prefix in the Windsurf MCP tools panel.
>
> | Server | Prefix | Stability |
> |--------|--------|-----------|
> | cc | `mcp0_*` | **STABLE** — custom Node.js server, always first |
> | cc2 (steipete) | `mcp1_claude_code` | ⚠️ Can shift on restart |
> | linear | `mcp3_*` | ⚠️ Can shift on restart |
> | memory | `mcp4_*` | ⚠️ Can shift on restart |

---

# REFERENCE — Project Rules Structure

> ### Directory Structure
>
> ```
> {project-root}/
> ├── .windsurfrules                     ← Layer 1: Mandatory routing rules + project guidelines
> ├── .windsurf/
> │   ├── rules/
> │   │   └── tool-preferences.md       ← Layer 2: Detailed routing table
> │   └── workflows/
> │       ├── test_cc_config.md         ← Daily health check (9 tests)
> │       └── [your-workflows].md       ← Custom workflows using mcp1_claude_code
> ├── .claude/
> │   ├── CLAUDE.md                     ← CC2 project context (auto-loaded via PWD)
> │   └── rules/
> │       ├── domain-rules.md           ← Critical business rules — never modify (no glob, always loads)
> │       ├── code-quality.md           ← Coding conventions (glob: *.ts, *.py, etc.)
> │       ├── libraries.md              ← Library/dependency constraints (glob: lib/**/*)
> │       └── [your-rules].md           ← Additional rules as needed
> ├── src/
> │   ├── index.ts                      ← (example source files)
> │   ├── utils.ts
> │   └── ...
> ```
>
> ### CLAUDE.md Format (≤52 lines)
>
> Keep this concise — it loads on every CC2 call.
>
> ```markdown
> # My Project — Claude Code Context
>
> ## Project
> Brief description of your project. Key constraints and principles.
>
> ## Architecture
> - Entry point: `src/index.ts`
> - Core modules: `src/core/`, `src/api/`
> - Key patterns: [describe your architecture]
>
> ## Libraries / Dependencies (READ ONLY)
> - `lib/auth.ts` → authentication module
> - `lib/db.ts` → database access layer
>
> ## Rules (auto-loaded per file type)
> `.claude/rules/` — loaded automatically:
> - `domain-rules.md` — critical business logic (NEVER modify)
> - `code-quality.md` — coding conventions and safety patterns
> ```
>
> ### Rules File Format
>
> `domain-rules.md` — no frontmatter (loads on every call):
> ```markdown
> # Domain Rules — Never Modify Without Verification
>
> ## Critical Formulas / Business Rules
> [Your critical formulas, algorithms, or business logic that must not be changed]
> WHY: [Explanation of why this is critical]
> ```
>
> `code-quality.md` — with glob (loads for matching files):
> ```markdown
> ---
> globs: ["*.ts"]
> ---
> # Code Quality Rules
> - Use consistent error handling patterns
> - Division: always guard against zero denominators
> - Validate inputs at system boundaries
> - Never use deprecated APIs
> ```

---

# REFERENCE — Daily Usage

> ### Normal Mode — Automatic Routing
>
> Just work. Cascade routes based on task:
>
> ```
> Review src/auth.ts for security issues
> ```
> → Cascade reads file, calls `mcp0_analyze_code` (Opus), returns analysis.
>
> ```
> Refactor the validation logic to use a strategy pattern
> ```
> → Cascade reads context, calls `mcp0_refactor_code`, applies returned edits.
>
> ```
> What do the docs say about this API's rate limits?
> ```
> → Cascade calls `mcp0_web_search`, returns synthesized answer.
>
> ```
> Fix typo on line 42: "calcualte" → "calculate"
> ```
> → Cascade uses `edit` directly. No CC call.
>
> ### CC2 Mode — Full Delegation
>
> For heavy or autonomous tasks, explicitly request CC2:
>
> ```
> use cc2 — do a full review of src/auth.ts and check for security vulnerabilities
> ```
>
> CC2 reads the file itself, loads `.claude/rules/`, applies coding standards, returns detailed analysis.
>
> ```
> use cc2 — build a new module for rate limiting following our existing patterns
> ```
>
> CC2 reads existing modules for reference, understands patterns, generates the full module, and writes it.
>
> ### Standard Workflow Pattern
>
> ```
> Step 1 — Cascade reads:      read_file → load context (for simple tasks)
> Step 2 — CC analyzes:        mcp0_analyze_code → understand the code
> Step 3 — CC generates:       mcp0_refactor_code → produce changes
> Step 4 — Cascade applies:    edit / multi_edit → write to files
> Step 5 — Cascade verifies:   run_command → run tests or validation
>
> --- OR for heavy tasks ---
>
> Step 1 — CC2 does everything: mcp1_claude_code → reads, analyzes, generates, writes
> Step 2 — Cascade verifies:    run_command → confirm result
> ```
>
> ### Force Mode
>
> ```
> use cc — analyze all modules for code quality compliance
> ```
> Forces all operations through `mcp0_*` tools.
>
> ```
> use cc2 — deep investigation of the authentication flow
> ```
> Forces full Claude Code Max delegation with autonomous file access.

---

# REFERENCE — Workflows Integration

> ### Available Workflows
>
> | Workflow | Tool Used | When |
> |----------|-----------|------|
> | `/test_cc_config` | All MCP tools | Daily health check, after restarts |
> | `/[your-review]` | `mcp1_claude_code` | Full code review |
> | `/[your-debug]` | `mcp1_claude_code` | Multi-file bug investigation |
> | `/learn` | Cascade | Extract session learnings to reference files |
>
> ### Creating Workflows That Use CC2
>
> ```markdown
> ---
> description: my workflow description
> ---
>
> ## Steps
>
> 1. Gather context
>
> 2. Use cc2 for analysis (`mcp1_claude_code`):
>    ```
>    Your work folder is /Users/YOUR_USERNAME/dev projects/YOUR_PROJECT
>
>    [Task instructions here.]
>    ```
>
> 3. Review and apply results
> ```

---

# REFERENCE — Health Check & Maintenance

> ### Rebuilding CC After Changes
>
> ```bash
> cd "/Users/YOUR_USERNAME/dev projects/mxc-claude-mcp"
> npm run build
> # Then restart Windsurf
> ```
>
> ### Updating Routing Rules
>
> If routing philosophy changes, update all three layers:
> 1. Edit `.windsurfrules` routing section
> 2. Edit `.windsurf/rules/tool-preferences.md`
> 3. Update Windsurf Memory (ask Cascade to update routing memory)
>
> ### Session Learning Hygiene
>
> End significant sessions with `/learn` — writes discoveries to `.claude/` reference files and updates memories for future sessions.

---

# REFERENCE — Troubleshooting

> ### CC2 red dot / "transport closed" error
>
> ```bash
> # Verify @latest (NOT a specific version):
> cat ~/.codeium/windsurf/mcp_config.json | grep steipete
> # Should show: @steipete/claude-code-mcp@latest
> # NOT: @steipete/claude-code-mcp@1.10.5 (this fails — version doesn't exist)
> ```
> Fix: change to `@latest` in config, restart Windsurf.
>
> ### CC2 prefix not mcp1_claude_code
>
> After restart, prefix shifted. Check Windsurf MCP panel for current cc2 tool name. Update `.windsurfrules` and `tool-preferences.md`:
> ```bash
> # Find current prefix by looking for "claude_code" in Windsurf tool panel
> # Then update routing files:
> sed -i '' 's/mcp1_claude_code/mpcX_claude_code/g' .windsurfrules
> ```
>
> ### CC2 rules not loading (T2 fails)
>
> PWD env not set or wrong path:
> ```json
> "env": {
>   "PWD": "/Users/YOUR_USERNAME/dev projects/YOUR_PROJECT"
> }
> ```
> Verify the path exactly matches your project root (where `.claude/` lives).
>
> ### CC tools hang indefinitely
>
> **Known bug (fixed Feb 2026):** The 5 Claude-powered tools hang if stdin isn't closed.
>
> Fix in `src/index.ts` `executeClaudeCLI`:
> ```typescript
> // WRONG — stdin never closed
> const child = spawn(CLAUDE_PATH, ["--print", "--dangerously-skip-permissions", prompt], ...);
>
> // CORRECT — prompt via stdin, stdin closed
> const child = spawn(CLAUDE_PATH, ["--print", "--dangerously-skip-permissions"], {
>   stdio: ["pipe", "pipe", "pipe"]
> });
> child.stdin.write(prompt);
> child.stdin.end();  // CRITICAL — Claude CLI hangs without this
> ```
> Rebuild: `npm run build`, restart Windsurf.
>
> Other causes:
> ```bash
> # Not authenticated:
> claude auth status
> claude auth login  # if needed
>
> # Permissions not accepted:
> claude --dangerously-skip-permissions
> # Accept the prompt, Ctrl+C
> ```
>
> ### CC tools not appearing in Cascade
>
> ```bash
> # Verify server starts cleanly:
> node "/Users/YOUR_USERNAME/dev projects/mxc-claude-mcp/dist/index.js"
>
> # Verify config is valid JSON:
> cat ~/.codeium/windsurf/mcp_config.json | python3 -m json.tool
>
> # Check logs:
> tail -f ~/Library/Logs/Claude/mcp*.log
> ```
>
> ### Debugging CC tools
>
> ```bash
> # Enable debug mode — add to cc entry in mcp_config.json:
> "env": {"MCP_CLAUDE_DEBUG": "true"}
>
> # Check processes:
> ps aux | grep "node.*mxc-claude-mcp"
> ps aux | grep "claude"
> ```
>
> ### Usage limit hit
>
> Claude Max: ~225 Opus calls per 5-hour window. Native tools (`mcp0_read_file` etc.) have no limit.
>
> Strategies near the limit:
> - Use Cascade native tools for the session
> - Batch remaining work into one focused CC call
> - Wait for 5-hour window to reset

---

# Quick Reference Card

> ```
> SETUP CHECKLIST
> ───────────────────────────────────────────────────────────────
> □ Node.js 18+ installed
> □ Claude CLI installed: npm install -g @anthropic-ai/claude-code
> □ Claude CLI authenticated: claude auth login → claude auth status
> □ --dangerously-skip-permissions accepted (one-time per machine)
> □ MCP server (cc) cloned and built: npm run build
> □ ~/.codeium/windsurf/mcp_config.json — all 4 servers configured
> □ Windsurf restarted
> □ /test_cc_config run — all 9 tests pass
> □ .windsurfrules has Tool Routing section at top
> □ .windsurf/rules/tool-preferences.md created
> □ .windsurf/workflows/test_cc_config.md created
> □ Windsurf Memory created via Cascade
>
>
> 3-TIER ROUTING CHEATSHEET
> ───────────────────────────────────────────────────────────────
> File reads, grep, edits ≤5 lines      → Cascade native (instant)
> Code review / bug analysis             → mcp0_analyze_code
> Generate / refactor (>10 lines)        → mcp0_refactor_code
> Web research                           → mcp0_web_search
> Heavy workflow / "use cc2"             → mcp1_claude_code (full autonomy)
>
>
> KEY PATHS
> ───────────────────────────────────────────────────────────────
> MCP config:      ~/.codeium/windsurf/mcp_config.json
> CC server:       ~/dev projects/mxc-claude-mcp/dist/index.js
> CC2 wrapper:     npx @steipete/claude-code-mcp@latest (auto-downloaded)
> Project rules:   {project}/.windsurfrules
> Tool prefs:      {project}/.windsurf/rules/tool-preferences.md
> CC2 context:     {project}/.claude/CLAUDE.md + .claude/rules/
>
>
> REBUILD CC
> ───────────────────────────────────────────────────────────────
> cd "/Users/YOUR_USERNAME/dev projects/mxc-claude-mcp" && npm run build
> # Then restart Windsurf
>
>
> VERIFY AFTER RESTART
> ───────────────────────────────────────────────────────────────
> Run: /test_cc_config
> All 9 pass = 100% confident, ready to work
> ```
