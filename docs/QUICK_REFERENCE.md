# Quick Reference Guide

Fast lookup for parameters, entry conditions, and trading checklist.

## Pre-Trade Checklist

Before every trade execution:

- [ ] Are moving averages properly aligned (5 > 20 > 60 or reverse)?
- [ ] Is entry point near support/resistance level?
- [ ] Is volume clearly increased above average?
- [ ] Is MACD/RSI signal clear and aligned with trend?
- [ ] Was previous trade profitable or within acceptable loss?
- [ ] Is account balance above minimum requirement?
- [ ] Have you calculated position size correctly?

## Core Parameters Summary

| Parameter | Value | Range | Notes |
|-----------|-------|-------|-------|
| Fast MA | 5 | 3-20 | Do not change |
| Mid MA | 20 | 10-50 | Do not change |
| Slow MA | 60 | 30-200 | Do not change |
| MACD | 12,26,9 | Standard | Industry standard |
| RSI | 14 | 5-50 | Do not change |
| RSI Overbought | 70 | 50-90 | Adjust by 5-10 |
| RSI Oversold | 30 | 10-50 | Adjust by 5-10 |
| ATR Period | 14 | 5-50 | Standard setting |
| Stop Loss Multiple | 2.0 | 1.0-3.0 | Varies with style |
| Take Profit Multiple | 3.0 | 1.5-5.0 | Maintain 1.5x ratio |
| Min Volume Ratio | 1.5 | 1.2-2.0 | Higher = stricter |
| Risk Per Trade | 2% | 1-3% | Account based |

## Entry Conditions

### Long Entry (All Required)

- 5MA > 20MA > 60MA (uptrend alignment)
- MACD bullish crossover OR RSI crosses above 30
- Volume > 20-bar average * 1.5
- Optional: Hammer pattern, bullish engulfing, or divergence

### Short Entry (All Required)

- 5MA < 20MA < 60MA (downtrend alignment)
- MACD bearish crossover OR RSI crosses below 70
- Volume > 20-bar average * 1.5
- Optional: Inverted hammer, bearish engulfing, or divergence

## Position Sizing Formula

```
Stop Loss Distance = ATR(14) * 2.0
Risk Amount = Account * 2% (default)
Position Size = Risk Amount / Stop Loss Distance
Take Profit = Entry + (Stop Loss Distance * 1.5)
```

Example:
- Account: $1,000
- Risk: $20 (2%)
- ATR: $50
- Stop Distance: $100
- Position: $20/$100 = 0.2 lot
- TP: Entry + $150

## Risk Management Rules

- Single trade risk: Never exceed 2% of account
- Consecutive losses: Stop after 3 losses, review strategy
- Daily loss limit: 3% of account triggers full stop
- Always set stop loss before entering
- Never move stop loss against your trade
- Use trailing stop to protect profits

## Market Condition Assessment

### Uptrend Status
- ATR ratio > 1.0: Strong momentum
- ATR ratio 0.8-1.0: Normal trend
- ATR ratio < 0.8: Consolidation (low probability)

### Volume Assessment
- Volume ratio > 3.0: Volume climax (strong signal)
- Volume ratio 1.5-3.0: Normal breakout confirmation
- Volume ratio < 1.5: Insufficient (avoid trading)

### Momentum Confirmation
- RSI > 50 during uptrend: Bullish
- RSI < 50 during downtrend: Bearish
- RSI 30-70: Neutral (use MACD)
- MACD above signal: Bullish
- MACD below signal: Bearish

## Diagnostic Guide

### Problem: Win Rate Below 50%

Likely Cause:
- Trading in consolidation periods
- Volume filter too low
- Entering on weak signals

Solution:
- Increase volume ratio to 2.0
- Enable divergence detection
- Wait for clear trend formation

### Problem: No Entry Signals

Likely Cause:
- Market in consolidation (ATR < 0.8)
- Filters too strict
- Wrong trading pair

Solution:
- Check ATR ratio status
- Reduce volume requirement to 1.2
- Switch to higher liquidity pair

### Problem: Frequent Losses

Likely Cause:
- Market environment unsuitable
- Position sizing too large
- Stop loss placement incorrect

Solution:
- Reduce risk per trade to 1%
- Verify stop loss is 2.0 ATR away
- Review previous 10 trades for patterns

### Problem: Excessive Drawdown

Likely Cause:
- Risk per trade too high
- Trading during volatility spikes
- Stop loss too far (slippage)

Solution:
- Reduce risk to 1% per trade
- Skip trading 30 min after news
- Increase stop loss to 2.5 ATR

## Performance Targets

| Metric | Target | Check Frequency |
|--------|--------|----------------|
| Win Rate | 55-65% | Monthly |
| Sharpe Ratio | 0.8+ | Monthly |
| Profit Factor | 1.5+ | Monthly |
| Monthly Return | 1-3% | Monthly |
| Max Drawdown | <15% | Weekly |
| Consecutive Losses | <3 | Every trade |

## Daily Trading Routine

### Morning (Before Market Open)

- Review prior day trades in journal
- Check market news and events
- Identify support/resistance levels
- Note any unusual market conditions
- Confirm strategy is enabled and ready

### During Trading

- Monitor 15-minute chart for signals
- Enter only when all conditions satisfied
- Set stop and limit orders immediately
- Do not watch open positions constantly
- Maintain trading discipline

### After Trading

- Record all trades with details
- Note any slippage or execution issues
- Update running statistics
- Plan next session

## K-Line Pattern Quick Reference

### Bullish Patterns
- Hammer: Lower shadow > 60% of range, small body
- Engulfing: Red candle followed by larger green candle
- Morning Star: Low-small-high pattern over 3 candles

### Bearish Patterns
- Inverted Hammer: Upper shadow > 60%, small body
- Engulfing: Green candle followed by larger red candle
- Evening Star: High-small-low pattern over 3 candles

## Indicator Signals Quick Lookup

### MACD
- Bullish: Line crosses above signal line
- Bearish: Line crosses below signal line
- Divergence: Price new extreme but MACD doesn't

### RSI
- Oversold: Below 30 (potential reversal)
- Overbought: Above 70 (potential reversal)
- Divergence: Price new extreme but RSI doesn't
- Crossover: Crosses 50 line (momentum change)

### Volume
- Climax: Ratio > 3.0 (strong impulse)
- Confirmation: Ratio 1.5-3.0 (normal breakout)
- Weak: Ratio < 1.5 (avoid trading)

## Position Management

### On Entry
- Immediately set stop loss
- Calculate take profit level
- Record entry reason
- Document position size

### While Holding
- Monitor for early exit signals
- Consider partial profit taking at 2:1 ratio
- Adjust trailing stop as price moves favorably
- Do not add to position

### At Exit
- Record exit price and reason
- Calculate P&L percentage
- Update trade journal
- Review for lessons

## Common Mistakes to Avoid

- Do NOT: Change parameters after every loss
- Do NOT: Hold losing trades hoping for reversal
- Do NOT: Add to losing positions
- Do NOT: Move stop loss against your trade
- Do NOT: Trade without predetermined plan
- Do NOT: Overtrade during low liquidity periods
- Do NOT: Ignore consecutive loss warnings

## Parameter Optimization Decision Tree

```
If Win Rate < 55%
  Then: Increase volume ratio, enable divergence
  
Else If Win Rate > 70%
  Then: Likely overfitting, retest with new data
  
Else If Signals < 5 per week
  Then: Reduce volume ratio to 1.2, disable advanced filters
  
Else If Drawdown > 15%
  Then: Reduce risk per trade to 1%, increase stop multiple to 2.5
  
Else If Sharpe < 0.8
  Then: Review trade logging, check for data errors
  
Else: Strategy performing as expected
```

## Monthly Review Checklist

- [ ] Total trades executed
- [ ] Win rate percentage
- [ ] Profit factor calculation
- [ ] Sharpe ratio measurement
- [ ] Maximum drawdown peak-to-trough
- [ ] Total monthly return
- [ ] Performance vs market index
- [ ] Any parameter changes needed
- [ ] Market condition changes noted
- [ ] Execution quality issues
- [ ] Plan adjustments for next month

## Trading Pair Liquidity Guide

### High Liquidity (Recommended)
- BTC/USDT: Tightest spreads, best execution
- ETH/USDT: Consistent volume, reliable signals

### Medium Liquidity (Acceptable)
- SOL/USDT: Good volume, moderate spreads
- MATIC/USDT: Adequate liquidity, watch slippage

### Low Liquidity (Avoid)
- Small market cap tokens
- Pairs with < $1M daily volume
- New token listings

## Critical Rules

1. Always use stop loss - no exceptions
2. Never exceed 2% risk per trade
3. Stop after 3 consecutive losses
4. Follow your plan mechanically
5. Document every trade
6. Review monthly performance
7. Adjust parameters only based on data
8. Never trade on emotions

Last Updated: January 16, 2026
