---
description: Comprehensive indicator review and scoring using Claude Code
---

# Indicator Review Workflow

# TODO: Configure your own indicator-review skill in .claude/skills/
# Copy .claude/skills/example-skill/ to .claude/skills/indicator-scorer/ and
# customize the scoring rubric in references/scoring-rubric.md.

## When to Use
When you need a comprehensive review and score of a Pine Script indicator.

## Steps

1. Identify the indicator file to review

2. Use cc2 for comprehensive analysis (`mcp1_claude_code`):
   ```
   Your work folder is /Users/YOUR_USERNAME/dev projects/YOUR_PROJECT

   Review this Pine Script indicator for institutional-grade quality:

   FILE: {indicator_file}

   REVIEW CRITERIA:

   1. ALGORITHMIC EDGE (2.5 points)
      - Novel signal generation vs standard approaches
      - Adaptive parameters vs static
      - Multi-factor confirmation logic

   2. REGIME ADAPTATION (2.5 points)
      - Volatility-aware thresholds
      - Market condition detection
      - Timeframe optimization

   3. CODE QUALITY (2.0 points)
      - Follows project conventions (math.sum, import patterns)
      - Constraint ranges enforced
      - No common Pine Script bugs
      - Plot count management

   4. ANALYTICAL CORRECTNESS (1.5 points)
      - Proven formulas unchanged
      - Signal logic mathematically sound
      - Edge cases handled

   5. TESTING/CONFIG (1.0 points)
      - Reasonable defaults
      - Input validation
      - Edge case protection

   6. DOCUMENTATION (0.5 points)
      - Clear variable naming
      - Logic comments where needed

   DELIVERABLES:
   - Score breakdown (X/10)
   - Specific strengths
   - Specific weaknesses with line numbers
   - Actionable improvements to reach 9.5+
   ```

3. Review the analysis

4. Prioritize and implement improvements

## Scoring Guide
- 9.5+: Institutional-grade, production ready
- 8.5-9.4: Strong, minor improvements needed
- 7.5-8.4: Good foundation, notable gaps
- <7.5: Significant work needed
