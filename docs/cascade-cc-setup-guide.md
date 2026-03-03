---
⚠️ BEFORE USING THIS GUIDE:
Find-and-replace in this document before pasting into Cascade:
  YOUR_USERNAME → your actual macOS username (e.g., johndoe)
  YOUR_CC_MCP_REPO → git URL for the mxc-claude-mcp server (github.com/your-org/mxc-claude-mcp, or use the public version)
  YOUR_PROJECT → your project folder name (e.g., my-indicators)
  YOUR_SOURCE_FILE → a representative source file in your project (e.g., main_indicator.pine)
  YOUR_RULES_FILE → a .claude/rules/ filename you want to verify auto-loads (e.g., quant-quality.md)
  YOUR_RULE_CONTENT → a phrase from that rules file, to verify it loaded (e.g., "proven formulas are sacred")

After replacing, execute in two Cascade sessions (required — Windsurf restart is a hard break):
  SESSION 1: Paste Phase 1 Steps 1–3 into a fresh Cascade chat. Stop at the ⚠️ MANUAL STEP restart.
  SESSION 2: Open a new Cascade chat, paste Steps 4–8. Cascade creates all files and runs tests.
---

# Windsurf Cascade + Claude Code: Project Setup Guide

> **Status**: Verified working Feb 2026. Run `/test_cc_config` after any Windsurf restart.

---

## Why This Setup

**The problem**: Windsurf's built-in Cascade uses Claude Sonnet by default. Every code review burns Windsurf credits and caps quality at Sonnet. If you have a **Claude Max subscription** (~$100/month flat rate), you already have Claude Opus quality with no per-token billing. This setup routes heavy work through Claude Max, eliminating the double-billing.

**The 3-Tier Design**:
```
Cascade (instant, Windsurf native)
  → CC mcp0_* (fast, focused, Opus quality)
    → CC2 mcp1_claude_code (full autonomy, Claude Code Max)
```

- **CC** (`mcp0_*`) — Claude via `--print` mode. Fast, focused analysis and generation.
- **CC2** (`mcp1_claude_code`) — Claude Code as a true sub-agent. Reads files, writes changes, runs scripts, auto-loads `.claude/rules/`.

---

## Phase 0 — Manual Prerequisites (do in terminal first)

### 0.1 — Install Node.js
```bash
node --version  # Need v18+
# If missing: brew install node
```

### 0.2 — Install Claude CLI
```bash
claude --version
# If missing:
npm install -g @anthropic-ai/claude-code
```

### 0.3 — Authenticate
```bash
claude auth login
# Select your Max subscription plan (flat-rate, not per-token)
claude auth status  # Verify
```

### 0.4 — Accept permissions (once per machine)
```bash
claude --dangerously-skip-permissions
# Accept the prompt, then Ctrl+C
```

### 0.5 — Verify CLI works
```bash
echo "Say hello" | claude --print
# Should respond within 10 seconds
```

---

## Phase 1 — Paste into Cascade (Session 1)

### Step 1 — Clone & Build CC Server

Run:
```bash
git clone YOUR_CC_MCP_REPO "/Users/YOUR_USERNAME/dev projects/mxc-claude-mcp"
cd "/Users/YOUR_USERNAME/dev projects/mxc-claude-mcp" && npm install && npm run build
ls "/Users/YOUR_USERNAME/dev projects/mxc-claude-mcp/dist/index.js"
```

### Step 2 — Create MCP Config

Create `~/.codeium/windsurf/mcp_config.json`:
```json
{
  "mcpServers": {
    "cc": {
      "command": "node",
      "args": ["/Users/YOUR_USERNAME/dev projects/mxc-claude-mcp/dist/index.js"],
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

> **Critical notes**:
> - Never pin `@steipete/claude-code-mcp` to a specific version — use `@latest`. Pinned versions cause transport errors.
> - `PWD` must point to your project root — this is how `.claude/rules/` auto-loads on every CC2 call.
> - `alwaysAllow` is NOT supported by Windsurf — omit it.
> - `linear` and `memory` are optional — remove if not using.

### Step 3 — Restart Windsurf

⚠️ MANUAL STEP: Fully quit (Cmd+Q) and relaunch Windsurf. MCP config only loads on startup. Then open a new Cascade chat for Session 2.

---

## Phase 2 — Paste into Cascade (Session 2)

### Step 4 — Create Windsurf Memory

Tell Cascade:
```
Create a memory titled "Tool Routing (MANDATORY)" with this content:

## Tool Routing (MANDATORY)
- Code analysis, reviews, refactoring, generation, web research → mcp0_* cc tools
- Mechanical edits ≤5 lines, file reads, shell commands → Cascade native tools
- Heavy workflows OR "use cc2" → mcp1_claude_code (Claude Code Max, loads .claude/rules/ automatically)
- Always prepend workFolder before cc2 prompts: "Your work folder is /Users/YOUR_USERNAME/dev projects/YOUR_PROJECT"

Verified prefixes (update after any Windsurf restart): cc=mcp0_*, cc2=mcp1_claude_code, linear=mcp3_*, memory=mcp4_*
```

### Step 5 — Set Windsurf Rules Activation

After Windsurf restarts, go to Settings → Rules and set activation modes:
- `code-quality.md` → **Glob**: `**/*.pine`
- `quant-quality.md` → **Always On**
- `dev-rules.md` → **Always On**
- `tool-preferences.md` → **Always On**

### Step 6 — Run Health Check

Run `/test_cc_config`. All 9 tests should pass.

---

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| `mcp1_claude_code` unknown | Prefix shifted on restart | Find new cc2 prefix in Windsurf MCP panel, update `.windsurfrules` + `tool-preferences.md` |
| Rules not loaded (T2 fail) | PWD env wrong | Verify `"PWD": "/Users/YOUR_USERNAME/dev projects/YOUR_PROJECT"` in cc2 env config |
| File access denied (T3 fail) | `--dangerously-skip-permissions` not accepted | Run in terminal once, accept, Ctrl+C |
| Timeout (T4 fail) | MCP_TOOL_TIMEOUT missing | Verify `"MCP_TOOL_TIMEOUT": "300000"` in cc2 env |
| `mcp0_*` tools fail (T5/T6) | CC server not running | Rebuild: `cd mxc-claude-mcp && npm run build`, restart Windsurf |

> **Prefix shifting** is the most common issue. Run `/test_cc_config` at start of any session where MCP tools will be heavily used.
