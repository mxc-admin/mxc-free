---
description: Validate Pine Script indicator against core rules using Claude Code
---

# Pine Script Validation Workflow

# TODO: Customize
# Replace MXC validator references with your own .claude/skills/pine-validator/ setup.
# Copy .claude/skills/example-skill/ to .claude/skills/pine-validator/ and add your
# project-specific constraint table in references/constraint-table.md.

## When to Use
When you need to validate an indicator against your project's core development guidelines.

## Steps

1. Identify the target indicator file to validate

2. Use Claude Code MCP to perform comprehensive validation:
   ```
   @cc Validate this Pine Script indicator against project core rules:
   
   FILE: {indicator_file}
   
   CHECK LIST:
   1. Constraint ranges: atr_pct ∈ [0,1], atr_vzn ∈ [0,1], valrank ∈ [0,1]
   2. Import pattern matches project conventions
   3. Use math.sum() not ta.sum()
   4. Plot count < 64 (dynamic colors count as 2)
   5. No modifications to proven formulas (see sacred-formulas.md)
   6. No nz() with boolean series
   7. No library state caching
   8. Division protection (math.max for denominators)
   9. Lookback bounds after smoothing (math.max(1, ...))
   
   Report any violations with line numbers and suggested fixes.
   ```

3. Review the validation results

4. Apply fixes if needed using the edit tool

## Expected Output
- List of violations (if any) with line numbers
- Suggested fixes for each violation
- Confirmation of compliant patterns
