---
description: Generate PineScript v6 indicators using DSPy-style structured reasoning with library patterns
---

# /pine - PineScript Indicator Development Workflow

# TODO: Customize
# Replace the library import patterns and DSPy examples below with your own
# project's library aliases and conventions.

## Trigger
`/pine [description]` or `/pine refine [existing code]`

## Overview
This workflow uses DSPy-inspired structured reasoning to generate production-quality PineScript v6 indicators that follow MXC library patterns.

## Process

### 1. Parse Request
Extract from user message:
- **Description**: What the indicator should do
- **Type**: momentum, volatility, trend, volume, or composite
- **Existing code**: If refining existing indicator

### 2. Call MCP Tool
Based on request type:

**For new indicators:**
```
pine_generate(
  description: [extracted description],
  indicator_type: [detected type],
  refine: true  // Always refine for quality
)
```

**For refining existing code:**
```
pine_refine(
  code: [extracted code block],
  feedback: [user's specific feedback],
  iterations: 2
)
```

**For validation only:**
```
pine_validate(
  code: [code to validate]
)
```

### 3. Present Results
Show:
1. **Score**: Quality score out of 1.0
2. **Validation**: Pass/fail for each MXC rule
3. **Code**: Final PineScript in fenced block
4. **Suggestions**: If score < 0.8, suggest improvements

## DSPy Concepts Applied

| DSPy Concept | Implementation |
|--------------|----------------|
| **Signature** | Typed I/O for IndicatorDesign, CodeGeneration |
| **ChainOfThought** | Multi-step reasoning before code generation |
| **ProgramOfThought** | Generate code, validate, use results |
| **Assertions** | Hard constraints (v6, plot limit) with retry |
| **Suggestions** | Soft constraints (MXC patterns) logged but continue |
| **Refine** | Iterative improvement with feedback |
| **DemoCache** | Store successful examples for few-shot learning |

## Validation Rules (Assertions)

### Hard Constraints (Assert - halt on failure):
- ✅ `//@version=6` required
- ✅ Plot count < 64 (dynamic colors count as 2)

### Soft Constraints (Suggest - log and continue):
- ⚠️ No repainting patterns (security without lookahead_off, barstate.isrealtime)
- ⚠️ Use MXC library patterns (tal.drankpct, tal.gma_fb, etc.)

## MXC Library Quick Reference

```pinescript
import momentumX_capital/mxc_ta/76 as tal

// Volatility (PROVEN - don't modify)
atr_pct = tal.drankpct(ta.atr(14), bar_index+1, 15, 1000) / 100
[atr_v, atr_vz, atr_vzn] = tal.vel_zscore(atr_pct)
val = atr_vzn / math.max(0.01, 1 - atr_pct)
valrank = tal.drankpct(val, bar_index+1, 15, 1000) / 100

// Smoothing
smoothed = tal.gma_fb(src, levels, depth)

// Timeframe aware
bars = tal.tf_lookback(target_days)

// Momentum
mom = tal.mom_score(src, lookback)
```

## Examples

### Generate New Indicator
```
/pine Create a momentum indicator that detects RSI divergence with volume confirmation. 
Should highlight potential reversals when RSI makes new low but price doesn't, 
with volume declining.
```

### Refine Existing Code
```
/pine refine
```pinescript
//@version=6
indicator("My RSI", overlay=false)
rsi = ta.rsi(close, 14)
plot(rsi)
```
Add MXC library patterns and improve signal quality.
```

### Validate Only
```
/pine validate [paste code]
```

## Notes
- Uses Claude Code CLI (no API costs - uses Max subscription)
- Successful generations are cached for few-shot learning
- Heavy operations may take 2-5 minutes
- If rate-limited, wait for 5-hour window to reset
