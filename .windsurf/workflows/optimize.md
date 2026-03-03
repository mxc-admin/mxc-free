---
description: Convert Pine Script indicators to Python and optimize parameters using VectorBT PRO
---

# /optimize - Parameter Optimization Workflow

# TODO: Customize
# Update the parameter extraction heuristics and example file names for your project.
# Replace library mapping references with your own project's library aliases.

## Trigger
`/optimize [file.pine]` or `/optimize [code block]`

## Overview
This workflow converts Pine Script indicators to Python, extracts the top 5-10 critical parameters, and runs VectorBT PRO parameter optimization with walk-forward validation.

## Architecture

```
┌─────────────────────────────────────────────────────────────────────────┐
│                     OPTIMIZATION PIPELINE                               │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐              │
│  │   /pine      │───▶│ /code-score  │───▶│ /code-evolve │              │
│  │ Development  │    │  Analysis    │    │  Refinement  │              │
│  └──────────────┘    └──────────────┘    └──────────────┘              │
│         │                                       │                       │
│         ▼                                       ▼                       │
│  ┌──────────────────────────────────────────────────────────┐          │
│  │                    /optimize                              │          │
│  │  ┌────────────┐  ┌────────────┐  ┌────────────┐          │          │
│  │  │ 1. EXTRACT │─▶│ 2. CONVERT │─▶│ 3. OPTIMIZE│          │          │
│  │  │ Parameters │  │ Pine→Python│  │ VBT PRO    │          │          │
│  │  └────────────┘  └────────────┘  └────────────┘          │          │
│  │         │              │               │                  │          │
│  │         ▼              ▼               ▼                  │          │
│  │  ┌────────────┐  ┌────────────┐  ┌────────────┐          │          │
│  │  │ Top 5-10   │  │ mxc_ta_py  │  │ Walk-Fwd   │          │          │
│  │  │ Params     │  │ Library    │  │ Validation │          │          │
│  │  └────────────┘  └────────────┘  └────────────┘          │          │
│  └──────────────────────────────────────────────────────────┘          │
│         │                                                               │
│         ▼                                                               │
│  ┌──────────────┐    ┌──────────────┐                                  │
│  │  Export to   │───▶│QuantConnect │                                  │
│  │  CSV/JSON    │    │  Execution   │                                  │
│  └──────────────┘    └──────────────┘                                  │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

## Process

### Stage 1: Parameter Extraction
Analyze Pine Script and identify optimizable parameters:

**Priority Categories:**
1. **Lookback periods** (e.g., `lookback`, `kama_len`, `atr_len`)
2. **Thresholds** (e.g., `er_threshold`, `vol_threshold`, `conf_threshold`)
3. **Multipliers** (e.g., `atr_mult`, `smoothing_coef`)
4. **Regime boundaries** (e.g., `choppy_threshold`, `trending_threshold`)

**Extraction Rules:**
- Skip hardcoded constants (EPSILON, plot limits)
- Skip proven formulas (valrank division formula)
- Focus on `input.*` parameters with numeric ranges
- Prioritize parameters that affect entry/exit logic

### Stage 2: Pine → Python Conversion
Convert core indicator logic using mapping table:

| Pine Pattern | Python Equivalent | Notes |
|--------------|-------------------|-------|
| `ta.ema(src, len)` | `pd.Series.ewm(span=len).mean()` | Direct |
| `ta.sma(src, len)` | `pd.Series.rolling(len).mean()` | Direct |
| `ta.atr(len)` | `vbt.ATR.run(high, low, close, len)` | VBT native |
| `ta.percentrank(src, len)` | `rolling_percentrank()` | Custom |
| `tal.drankpct(src, ...)` | `dynamic_percentrank()` | Custom |
| `tal.gma_fb(src, l, d)` | `gaussian_ma(src, l, d)` | Custom |
| `tal.gaussianFilter(...)` | `gaussian_filter()` | SciPy |
| `var float x = 0` | Class attribute / closure | State |
| `src[i]` | `src.shift(i)` | Pandas |
| `math.tanh(x)` | `np.tanh(x)` | NumPy |

### Stage 3: VBT PRO Optimization
Run parameter optimization with anti-overfitting measures:

```python
# Optimization Configuration
optimization_config = {
    "method": "grid",           # grid, random, or bayesian
    "target_metric": "sharpe",  # sharpe, calmar, sortino
    "constraints": {
        "max_drawdown": 0.25,   # Hard constraint
        "min_trades": 30,       # Statistical significance
        "min_win_rate": 0.35,   # Minimum viability
    },
    "walk_forward": {
        "enabled": True,
        "in_sample_ratio": 0.7,
        "num_splits": 4,
        "purge_days": 5,        # Gap between train/test
    },
    "chunking": {
        "enabled": True,
        "chunk_size": 1000,     # Combinations per chunk
    }
}
```

### Stage 4: Validation & Export
Generate optimized parameters and export for QuantConnect:

**Output Artifacts:**
1. `optimized_params.json` - Best parameters found
2. `optimization_report.md` - Full analysis with charts
3. `strategy.py` - VBT-compatible Python code
4. `qc_signals.csv` - Signal export for QuantConnect

## Parameter Extraction Heuristics

### For `your_indicator.pine`:
```
TOP 10 OPTIMIZABLE PARAMETERS:
<!-- TODO: Replace with your indicator's parameters -->
1. lookback                      Range: [15, 60]    Impact: HIGH
2. threshold_1                   Range: [0.2, 0.5]  Impact: HIGH
3. atr_mult                      Range: [1.0, 2.5]  Impact: HIGH
4. vol_threshold                 Range: [0.3, 0.7]  Impact: HIGH
5. conf_threshold                Range: [0.45, 0.75] Impact: MEDIUM
6. indicator_len_1               Range: [7, 18]     Impact: MEDIUM
7. indicator_len_2               Range: [15, 35]    Impact: MEDIUM
8. smoothing_len                 Range: [2, 8]      Impact: LOW
9. smoothing_sigma               Range: [1.0, 2.5]  Impact: LOW
10. cycle_threshold              Range: [0.25, 0.5] Impact: LOW

SKIP (Proven/Sacred — see .claude/rules/sacred-formulas.md):
- Any formula listed in sacred-formulas.md
- Percentile ranking lookbacks
```

## DSPy Concepts Applied

| DSPy Concept | Implementation |
|--------------|----------------|
| **Signature** | Typed I/O for ParameterExtraction, CodeConversion, Optimization |
| **ChainOfThought** | Multi-step reasoning for parameter prioritization |
| **ProgramOfThought** | Generate AND execute Python/VBT code |
| **Assertions** | Hard constraints (drawdown, bias) with retry |
| **Suggestions** | Soft constraints (Sharpe, win rate) logged |
| **Metrics** | Custom scoring: Sharpe × (1 - DD) × stability |
| **DemoCache** | Store successful optimizations for future reference |

## Validation Rules

### Hard Constraints (Assert - halt on failure):
- ✅ Max drawdown ≤ 25%
- ✅ No look-ahead bias in Python code
- ✅ Parameter ranges respect Pine Script constraints
- ✅ Walk-forward OOS Sharpe within 30% of IS

### Soft Constraints (Suggest - log and continue):
- ⚠️ Sharpe ratio ≥ 1.0
- ⚠️ Win rate ≥ 40%
- ⚠️ At least 30 trades for statistical significance
- ⚠️ Parameter stability across walk-forward windows

## Anti-Overfitting Measures

1. **Walk-Forward Validation**: 70/30 train/test with 4 rolling windows
2. **Purging**: 5-day gap between train and test periods
3. **Parameter Stability**: Flag if optimal params vary >20% across windows
4. **IS/OOS Gap Check**: Alert if OOS performance drops >30% vs IS
5. **Minimum Trade Count**: Require 30+ trades for significance

## Output Format

```markdown
## /optimize Results: your_indicator.pine

### Parameter Extraction
| Parameter | Current | Range | Impact | Optimized |
|-----------|---------|-------|--------|-----------|
| lookback | 30 | [15, 60] | HIGH | 42 |
| er_threshold | 0.3 | [0.2, 0.5] | HIGH | 0.35 |
| ... | ... | ... | ... | ... |

### Optimization Summary
- **Combinations Tested**: 12,500
- **Best IS Sharpe**: 1.85
- **Best OOS Sharpe**: 1.52 (-18% vs IS ✓)
- **Max Drawdown**: 18.3% ✓
- **Win Rate**: 52.1% ✓
- **Total Trades**: 147 ✓

### Walk-Forward Stability
| Window | IS Sharpe | OOS Sharpe | Params Stable |
|--------|-----------|------------|---------------|
| 1 | 1.72 | 1.45 | ✓ |
| 2 | 1.91 | 1.58 | ✓ |
| 3 | 1.88 | 1.61 | ✓ |
| 4 | 1.79 | 1.44 | ✓ |

### Recommendation
✅ **GO** - Parameters are robust, OOS performance acceptable.

### Files Generated
- `optimized_params.json`
- `your_indicator_optimized.py`
- `qc_signals.csv`
```

## Examples

### Optimize Pine File
```
/optimize your_indicator.pine
```

### Optimize with Custom Ranges
```
/optimize your_indicator.pine
Override: lookback=[20,80], er_threshold=[0.15,0.6]
Asset: BTC-USD
Period: 2020-2024
```

### Optimize Code Block
```
/optimize
```pinescript
// paste code here
```
Focus: entry/exit thresholds only
```

## Integration with Other Workflows

### Recommended Flow
```
1. /pine [description]        → Generate initial indicator
2. /code-score               → Analyze and score (target 8+)
3. /code-evolve [feedback]   → Refine based on score
4. /optimize [file.pine]     → Parameter optimization
5. Export to QuantConnect    → Live execution
```

### Workflow Chaining
```bash
# Full pipeline example
/pine "momentum indicator with regime detection"
# Review output, then:
/code-score
# If score < 8, then:
/code-evolve "improve regime detection sensitivity"
# When satisfied:
/optimize your_indicator.pine
```

## Technical Implementation

### Core Python Modules Required
```python
# optimize/
├── __init__.py
├── extractor.py      # Parameter extraction from Pine
├── converter.py      # Pine → Python conversion
├── indicators.py     # Indicator implementations
├── optimizer.py      # VBT PRO optimization wrapper
├── validator.py      # Walk-forward validation
└── exporter.py       # QuantConnect export
```

### Key Dependencies
```
vectorbt>=0.26.0      # Or VBT PRO
pandas>=2.0.0
numpy>=1.24.0
numba>=0.57.0
scipy>=1.10.0
optuna>=3.0.0         # For Bayesian optimization (optional)
```

## Notes
- Uses Claude Code CLI for analysis (no API costs with Max subscription)
- Heavy optimization may take 5-15 minutes depending on parameter space
- Walk-forward adds ~5 minutes but essential for production strategies
- Always validate Python output matches Pine Script behavior on sample data
- VBT PRO license ($240/yr) recommended for 10,000+ parameter combinations
