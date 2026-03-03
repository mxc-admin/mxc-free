---
description: solve pesky deep bug
---

# Deep Bug Investigation Workflow

## When to Use
When facing a complex bug that requires deep analysis across multiple files or understanding of intricate Pine Script behavior.

## Steps

1. Gather context about the bug:
   - What is the expected behavior?
   - What is the actual behavior?
   - Which indicator/file is affected?

2. Use cc2 for deep investigation (`mcp1_claude_code`):
   ```
   Your work folder is /Users/YOUR_USERNAME/dev projects/YOUR_PROJECT

   Investigate this Pine Script bug:

   BUG DESCRIPTION: {description}
   AFFECTED FILE: {file}
   EXPECTED: {expected}
   ACTUAL: {actual}

   INVESTIGATION STEPS:
   1. Read the affected file and trace the logic
   2. Check library dependencies in pine/libraries/
   3. Verify constraint ranges are respected
   4. Check for common Pine Script issues:
      - nz() with boolean series
      - Tuple destructuring with := instead of =
      - Division by zero without protection
      - Lookback values becoming 0 after smoothing
   5. Compare against reference implementation
   6. Identify root cause (not symptoms)

   Provide minimal upstream fix, not downstream workaround.
   ```

3. Review the analysis and proposed fix

4. Apply the fix and verify

## Key Principles
- Prefer minimal upstream fixes over downstream workarounds
- Identify root cause before implementing
- Avoid over-engineering—use single-line changes when sufficient
- Add regression tests but keep implementation minimal
