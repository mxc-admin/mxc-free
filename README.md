# Pine Script Quant Dev — Project Template

> A ready-to-use project template for Pine Script v6 quant development with full Windsurf Cascade + Claude Code setup.

---

## What This Template Provides

- **Windsurf Cascade rules** (`.windsurf/rules/`) — always-on development, quant quality, and code quality rules
- **Claude Code rules** (`.claude/rules/`) — auto-loaded context for CC2 with globs for Pine files, libraries, indicators, and strategies
- **Slash-command workflows** (`.windsurf/workflows/`) — indicator generation, review, validation, optimization, git operations, and MCP health checks
- **Skill template** (`.claude/skills/example-skill/`) — copy to create project-specific Claude Code skills
- **3-tier AI routing** — Cascade (instant) → CC mcp0_* (Opus quality) → CC2 mcp1_claude_code (full autonomy)
- **Setup guide** (`docs/cascade-cc-setup-guide.md`) — step-by-step Windsurf + Claude Code configuration

---

## Directory Structure

```
├── .windsurfrules                          ← Mandatory routing rules (Windsurf reads this)
├── .windsurf/
│   ├── rules/
│   │   ├── dev-rules.md                   ← Development behavior (Always On)
│   │   ├── quant-quality.md               ← Algo/trading rules (Always On)
│   │   ├── code-quality.md                ← Pine Script patterns (Glob: **/*.pine)
│   │   └── tool-preferences.md            ← 3-tier routing detail (Always On)
│   └── workflows/
│       ├── test_cc_config.md              ← Daily MCP health check (9 tests)
│       ├── pine.md                        ← Generate Pine indicators
│       ├── pine-validate.md               ← Validate against rules
│       ├── indicator-review.md            ← Score indicators (10-point rubric)
│       ├── optimize.md                    ← Pine→Python + VBT optimization
│       ├── code-score.md                  ← Meta-cognitive code review
│       ├── code-evolve.md                 ← Feedback-driven code evolution
│       ├── deep-bug.md                    ← Multi-file bug investigation
│       ├── learn.md                       ← Session pattern extraction
│       ├── evolve.md                      ← Knowledge consolidation
│       └── git-*.md                       ← Git workflows (commit, push, undo, checkpoint)
├── .claude/
│   ├── CLAUDE.md                          ← Project context (auto-loaded by CC2)
│   ├── rules/
│   │   ├── dev-rules.md                   ← Mirror of .windsurf/rules/ version
│   │   ├── quant-quality.md               ← Mirror of .windsurf/rules/ version
│   │   ├── code-quality.md                ← Extended version (globs: pine/**/*.pine)
│   │   ├── libraries.md                   ← READ ONLY enforcement (globs: pine/libraries/*.pine)
│   │   ├── indicators.md                  ← Plot limits, constraints (globs: pine/*.pine)
│   │   ├── strategies.md                  ← Strategy architecture (globs: pine/*.pine)
│   │   └── sacred-formulas.md             ← Battle-tested formulas (NEVER modify)
│   └── skills/
│       └── example-skill/                 ← Copy to create new skills
│           ├── SKILL.md
│           └── references/knowledge.md
├── pine/
│   ├── indicators/                        ← Your Pine Script indicators
│   └── libraries/                         ← Shared libraries (READ ONLY)
├── python/
│   ├── indicators/                        ← Python ports for backtesting
│   └── libraries/                         ← Python utility libraries
├── ml/                                    ← ML optimization scripts
├── quant_connect/                         ← QuantConnect strategies
└── docs/
    └── cascade-cc-setup-guide.md          ← Full Windsurf + Claude Code setup guide
```

---

## Getting Started

1. **Clone this template** and rename for your project
2. **Fill in TODO sections** in `.claude/CLAUDE.md` — project description, libraries, architecture
3. **Add sacred formulas** to `.claude/rules/sacred-formulas.md` as you validate them in live trading
4. **Set up AI environment** — follow [`docs/cascade-cc-setup-guide.md`](docs/cascade-cc-setup-guide.md)
5. **Create skills** — copy `.claude/skills/example-skill/` for project-specific automation

## Dual-File Rule

Three rules files exist in both `.windsurf/rules/` and `.claude/rules/`:
- `dev-rules.md`, `quant-quality.md`, `code-quality.md`

When updating any of these, **always update both locations**. Windsurf Cascade reads `.windsurf/rules/`, Claude Code reads `.claude/rules/`.

---

## License

MIT — use freely, attribution appreciated.
