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

From your loaded .claude/rules/ files — confirm you can see the sacred-formulas.md content. Quote one formula name.
```
**Pass:** mentions a formula name from sacred-formulas.md
**Fail:** "I don't have that" or generic answer → `.claude/` not found. Check `PWD` env in `mcp_config.json`, verify it points to the correct project dir.

---

## Test 3 — CC2 autonomous file access
Call `mcp1_claude_code`:
```
Your work folder is /Users/YOUR_USERNAME/dev projects/YOUR_PROJECT

Read pine/YOUR_SOURCE_FILE.pine and tell me: how many lines does it have and what is the current version comment at the top?
```
**Pass:** returns a line count and version/title from the actual file header
**Fail:** can't read file → subprocess CWD issue or file permissions. Check `claude --dangerously-skip-permissions` was accepted.

---

## Test 4 — CC2 timeout headroom (medium task)
Call `mcp1_claude_code`:
```
Your work folder is /Users/YOUR_USERNAME/dev projects/YOUR_PROJECT

List all .pine files in the pine/ directory with their line counts. Sort by size descending.
```
**Pass:** returns full sorted table, no timeout
**Fail:** timeout error → `MCP_TOOL_TIMEOUT` not applied. Verify `mcp_config.json` cc2 entry has `"MCP_TOOL_TIMEOUT": "300000"` and restart Windsurf.

---

## Test 5 — CC (`mcp0_*`) analysis tool
Call `mcp0_analyze_code`:
```
path: /Users/YOUR_USERNAME/dev projects/YOUR_PROJECT/pine/YOUR_SOURCE_FILE.pine
query: Summarize what this file does in 2 sentences.
```
**Pass:** returns a coherent 2-sentence summary of the file
**Fail:** tool error or timeout → cc server issue. Check `ps aux | grep "node.*mxc-claude-mcp"`. Rebuild if needed: `cd "/Users/YOUR_USERNAME/dev projects/mxc-claude-mcp" && npm run build`

---

## Test 6 — CC web search
Call `mcp0_web_search`:
```
query: Pine Script v6 indicator plot limit
```
**Pass:** returns relevant results mentioning 64 plots or TradingView documentation
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
| 2 | Rules loaded | `mcp1_claude_code` | formula name from sacred-formulas.md |
| 3 | File access | `mcp1_claude_code` | Line count + header from YOUR_SOURCE_FILE.pine |
| 4 | Timeout headroom | `mcp1_claude_code` | Full sorted table, no timeout |
| 5 | CC analysis | `mcp0_analyze_code` | 2-sentence summary of YOUR_SOURCE_FILE |
| 6 | CC web search | `mcp0_web_search` | Pine Script plot limit results |
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
| Guide stale (T9) | Guide not updated after config change | Open `docs/cascade-cc-setup-guide.md`, find the failing section, update to match current verified values (prefixes, version, timeout, routing) |

---

## Notes
- **Prefix shifting** is the most common issue after restarts — cc2 prefix is most likely to shift
- cc (`mcp0_*`) is the most stable — custom Node.js server, prefix never shifts
- Run this workflow at start of any session where MCP tools will be heavily used
- T9 catches guide drift — if you update `.windsurfrules`, `mcp_config.json`, or routing philosophy but forget to update the guide, T9 will flag it
