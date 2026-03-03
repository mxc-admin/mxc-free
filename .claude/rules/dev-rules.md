# Development Behavior Rules
# Read by: Cascade (Always On) | Mirror: .windsurf/rules/dev-rules.md

## Before Writing Code
1. Describe your approach first and wait for approval before implementing.
2. If requirements are ambiguous, ask clarifying questions — do not assume.

## While Writing Code
3. If a task requires changes to more than 3 files, stop and break it into smaller tasks first.
4. Any change touching `pine/libraries/**` requires explicit confirmation regardless of file count — these are shared across published indicators.

## After Writing Code
5. After finishing any code, list the edge cases and suggest test cases to cover them.

## Debugging
6. When there's a bug, write a test or minimal reproduction case first, then fix it until the test passes.

## Learning from Corrections
7. Every time you are corrected, reflect on what went wrong and state a plan to avoid the same mistake. Write the pattern to the appropriate rules file if it's likely to recur — update BOTH `.windsurf/rules/` AND `.claude/rules/` versions.

## Dual-File Rule: Shared Rules Live in Two Places
When updating `code-quality.md`, `quant-quality.md`, or `dev-rules.md`:
- Always update BOTH `.windsurf/rules/<file>` AND `.claude/rules/<file>`
- These files must stay in sync — one is for Cascade, one is for CC2
