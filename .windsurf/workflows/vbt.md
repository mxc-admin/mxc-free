---
description: Backtest trading strategies using VectorBT with DSPy-style structured reasoning and optimization
---

# /vbt - VectorBT Strategy Backtesting Workflow

## Trigger
`/vbt [strategy description]` or `/vbt quick [entry] [exit]`

## Overview
This workflow uses DSPy-inspired structured reasoning to design, backtest, and optimize trading strategies using VectorBT. Includes parameter optimization and optional walk-forward analysis.

## Process

### 1. Parse Request
Extract from user message:
- **Strategy description**: Entry/exit logic concept
- **Asset**: Symbol to test (default: BTC-USD)
- **Date range**: Backtest period
- **Options**: optimize, walk_forward

### 2. Call MCP Tool
Based on request type:

**For full backtest:**
```
vbt_backtest(
  description: [strategy concept],
  asset: [symbol],
  date_range: "2020-01-01 to 2024-01-01",
  optimize: true,
  walk_forward: false  // Set true for production strategies
)
```

**For quick test:**
```
vbt_quick(
  entry: [entry condition],
  exit: [exit condition],
  asset: [symbol]
)
```

**For parameter optimization:**
```
vbt_optimize(
  code: [existing strategy code],
  param_ranges: "fast_ma: 5-30, slow_ma: 20-100",
  target: "sharpe"
)
```

### 3. Present Results
Show:
1. **Score**: Quality score out of 1.0
2. **Metrics**: Sharpe, Max DD, Win Rate, Profit Factor, Returns, Trades
3. **Validation**: Pass/fail for each constraint
4. **Optimization**: Best parameters found (if enabled)
5. **Walk-Forward**: OOS performance (if enabled)
6. **Code**: Complete VectorBT Python code

## DSPy Concepts Applied

| DSPy Concept | Implementation |
|--------------|----------------|
| **Signature** | Typed I/O for StrategyDesign, BacktestExecution, Optimization |
| **ChainOfThought** | Strategy architecture reasoning |
| **ProgramOfThought** | Write AND execute Python/VectorBT code |
| **Assertions** | Hard constraints (drawdown, bias) with retry |
| **Suggestions** | Soft constraints (Sharpe, win rate) logged |
| **Metrics** | Custom scoring based on Sharpe, DD, win rate |
| **DemoCache** | Store successful strategies for few-shot learning |

## Validation Rules (Assertions)

### Hard Constraints (Assert - halt on failure):
- ✅ Max drawdown ≤ 25%
- ✅ No look-ahead bias (negative shifts, future data)

### Soft Constraints (Suggest - log and continue):
- ⚠️ Sharpe ratio ≥ 1.0
- ⚠️ Win rate ≥ 40%
- ⚠️ At least 30 trades for statistical significance

## Performance Metrics

| Metric | Target | Weight |
|--------|--------|--------|
| Sharpe Ratio | > 1.0 | 40% |
| Max Drawdown | < 25% | 30% |
| Win Rate | > 45% | 30% |

**Score Formula:**
```python
score = min(1.0,
  min(0.4, sharpe * 0.2) +           # Sharpe contribution
  (0.25 - max_dd) * 1.2 +            # Drawdown contribution
  min(0.3, (win_rate - 0.45) * 2)    # Win rate contribution
)
```

## VectorBT Quick Reference

```python
import vectorbt as vbt
import yfinance as yf
import numpy as np

# Load data
data = yf.download("BTC-USD", start="2020-01-01", end="2024-01-01")
close = data['Close']

# Generate signals
fast_ma = vbt.MA.run(close, 10)
slow_ma = vbt.MA.run(close, 30)
entries = fast_ma.ma_crossed_above(slow_ma)
exits = fast_ma.ma_crossed_below(slow_ma)

# Backtest
pf = vbt.Portfolio.from_signals(
    close, entries, exits,
    init_cash=10000,
    fees=0.001,
    slippage=0.001
)

# Metrics
print(f"Sharpe: {pf.sharpe_ratio():.2f}")
print(f"Max DD: {pf.max_drawdown():.1%}")
print(f"Win Rate: {pf.trades.win_rate():.1%}")
print(f"Profit Factor: {pf.trades.profit_factor():.2f}")
print(f"Total Return: {pf.total_return():.1%}")
print(f"Trades: {pf.trades.count()}")

# Parameter optimization
fast_windows = np.arange(5, 30, 5)
slow_windows = np.arange(20, 100, 10)
# ... grid search
```

## Examples

### Full Strategy Backtest
```
/vbt RSI mean reversion strategy: Buy when RSI drops below 30 and price 
is above 200-day MA (trend filter). Sell when RSI rises above 70 or 
hits 10% trailing stop. Test on BTC-USD from 2020-2024.
```

### Quick Entry/Exit Test
```
/vbt quick "RSI < 30" "RSI > 70" BTC-USD
```

### With Walk-Forward
```
/vbt Bollinger Band breakout with ATR stops. Use walk-forward validation 
to check for overfitting.
```

### Parameter Optimization Only
```
/vbt optimize [paste existing code]
Optimize: fast_ma 5-25, slow_ma 20-80
Target: sharpe
```

## Walk-Forward Analysis

When enabled, performs rolling out-of-sample validation:
1. Split data into 4 windows (70% train / 30% test each)
2. Optimize parameters on training set
3. Test on out-of-sample period
4. Report OOS Sharpe and parameter stability

**Interpretation:**
- OOS Sharpe within 20% of IS = Good
- Parameters stable across windows = Robust
- Large IS/OOS gap = Likely overfitting

## Notes
- Uses Claude Code CLI (no API costs - uses Max subscription)
- Backtests execute ACTUAL Python code (not simulated)
- Heavy optimization may take 5-10 minutes
- Always use fees=0.001, slippage=0.001 minimum
- Require 30+ trades for statistical significance
- Walk-forward adds ~5 minutes but catches overfitting
