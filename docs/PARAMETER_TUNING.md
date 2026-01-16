# Parameter Tuning Guide

Systematic approach to optimizing strategy parameters based on backtesting results.

## Core Tuning Philosophy

1. Test defaults first before any modifications
2. Change only ONE parameter at a time
3. Run backtest with minimum 3 months of data
4. Document all changes and results
5. Never overtrain on historical data
6. Validate against out-of-sample data

## Parameter Categories

### Tier 1: Never Change

These are industry-standard indicators:
- Fast MA: 5 (ultra-short term trend)
- Mid MA: 20 (short-term trend)
- Slow MA: 60 (long-term trend baseline)
- MACD: 12,26,9 (standard settings worldwide)
- RSI: 14 (standard period)
- ATR: 14 (standard period)

### Tier 2: Safe to Adjust

These parameters can be tuned based on strategy performance:
- Risk per trade: 1-3% (account dependent)
- Stop loss multiple: 1.5-2.5 (volatility dependent)
- Take profit multiple: 2.0-4.0 (maintain 1.5x ratio)
- Volume confirmation: 1.2-2.0 (market condition dependent)
- Divergence lookback: 3-7 bars (signal frequency)

### Tier 3: Market Specific

Optional settings based on trading pair characteristics:
- RSI overbought: 65-75 (adjust by 5)
- RSI oversold: 25-35 (adjust by 5)
- Trailing stop: Enable/disable based on preference

## Step-by-Step Tuning Process

### Phase 1: Establish Baseline

1. Run backtest with all default parameters
2. Document baseline metrics:
   - Win rate %
   - Profit factor
   - Sharpe ratio
   - Maximum drawdown
   - Total trades
3. Save backtest results as reference

Default Baseline Expected (BTC/USDT 15m):
- Win Rate: 56-62%
- Profit Factor: 1.4-1.8
- Sharpe Ratio: 0.7-1.1
- Max Drawdown: 8-12%

### Phase 2: Identify Problem Areas

Based on baseline, identify which metric needs improvement:

**Issue: Win Rate < 55%**
- Adjust: Increase volume ratio first
- Then: Enable divergence detection
- Finally: Increase stop loss multiple

**Issue: Sharpe Ratio < 0.8**
- Adjust: Reduce risk per trade to 1%
- Then: Increase stop loss to 2.5 ATR
- Finally: Review drawdown severity

**Issue: Too Few Signals (< 5 per week)**
- Adjust: Reduce volume requirement to 1.2
- Then: Disable divergence requirement
- Finally: Reduce RSI levels by 5 points

**Issue: Excessive Drawdown (> 15%)**
- Adjust: Reduce risk per trade to 1%
- Then: Increase stop loss multiple to 2.5
- Finally: Review market condition fit

### Phase 3: Parameter Adjustment Protocol

#### Adjusting Risk Per Trade

Current: 2%

Test sequence:
1. Test 1.5% for 3 months data
2. Compare Sharpe ratio (should improve)
3. If improvement > 10%, keep change
4. Continue to 1% if needed

Expected effect:
- Lower risk: Smoother equity curve, lower returns
- Higher risk: Spikier equity curve, higher returns

#### Adjusting Stop Loss Multiple

Current: 2.0

Test sequence:
1. Test 1.8 for volatility reduction
2. Test 2.2 for stability improvement
3. Compare max drawdown
4. Select value balancing drawdown and profitability

Expected effect:
- Tighter stop (1.5): More losses but smaller drawdowns
- Wider stop (2.5): Fewer losses but larger drawdowns

#### Adjusting Volume Ratio

Current: 1.5

Test sequence:
1. Test 1.2 for more signals
2. Test 2.0 for higher quality signals
3. Compare win rate impact
4. Trade-off: quantity vs quality

Expected effect:
- Lower ratio (1.2): More trades, potentially lower win rate
- Higher ratio (2.0): Fewer trades, potentially higher win rate

#### Adjusting RSI Levels

Current: 30 oversold, 70 overbought

Test sequence:
1. Test 25/75 for more aggressive entries
2. Test 35/65 for more conservative entries
3. Compare entry timing vs price movement
4. Select based on win rate preference

Expected effect:
- Lower threshold (25/75): Earlier entries, more reversal catches
- Higher threshold (35/65): Later entries, fewer false reversals

## Backtesting Protocol

### Data Requirements

- Minimum: 3 months historical data
- Optimal: 6-12 months for validation
- Preferred: Multiple market conditions (bull, bear, consolidation)

### Commission Settings

```
Exchange: Binance/Bybit
Commission: 0.05% (taker fee)
Slippage: Built into backtest
```

### Test Scenarios

Test each parameter change across scenarios:

**Scenario 1: Strong Uptrend (30 days)
- Example: Jan 2024 crypto bull run
- Expect: High win rates, good profits
- Problem: May not handle bear markets

**Scenario 2: Downtrend (30 days)
- Example: Market crash period
- Expect: Profitable shorts or minimal longs
- Problem: May be too conservative

**Scenario 3: Consolidation (30 days)
- Example: Sideways trading period
- Expect: Lower win rates, choppy trades
- Problem: Reveals false breakout catches

**Scenario 4: Mixed (Full period)
- Best overall assessment
- Accounts for real market variations
- Use for final decisions

## Optimization Example

### Starting Point: Default Parameters
- Win Rate: 54%
- Sharpe Ratio: 0.7
- Profit Factor: 1.3
- Max Drawdown: 18%
- Problem: Low Sharpe ratio, high drawdown

### Step 1: Reduce Risk Per Trade to 1%
Backtest Results:
- Win Rate: 54% (unchanged)
- Sharpe Ratio: 0.85 (improved)
- Max Drawdown: 9% (improved)
- Decision: KEEP THIS CHANGE

### Step 2: Increase Volume Ratio to 2.0
Backtest Results:
- Win Rate: 62% (improved)
- Sharpe Ratio: 0.90 (improved)
- Trades: 40 (reduced from 60)
- Decision: KEEP THIS CHANGE

### Step 3: Increase Stop Loss to 2.5 ATR
Backtest Results:
- Win Rate: 61% (slight decrease)
- Sharpe Ratio: 0.92 (improved)
- Max Drawdown: 8% (improved)
- Decision: KEEP THIS CHANGE

### Final Result: Enhanced Parameters
- Risk per trade: 1%
- Volume ratio: 2.0
- Stop loss multiple: 2.5
- Take profit multiple: 3.75 (maintain 1.5x ratio)
- Win Rate: 61%
- Sharpe Ratio: 0.92 (improved from 0.7)
- Max Drawdown: 8% (improved from 18%)

## Parameter Validation

### In-Sample vs Out-of-Sample

1. Optimize on 6 months historical data (in-sample)
2. Test optimized parameters on 3 months new data (out-of-sample)
3. Acceptable variance: Within 5% of metrics
4. If variance > 10%: Likely overfitted, revert changes

### Walk-Forward Testing

For robust validation:

1. Divide 12 months into 3x4-month periods
2. Optimize on period 1 (months 1-4)
3. Test on period 2 (months 5-8) without optimization
4. Optimize on combined 1+2
5. Test on period 3 (months 9-12)
6. Compare results consistency

## Common Optimization Pitfalls

### Pitfall 1: Overfitting

Problem: Parameters optimized for historical data don't work live.

Solution:
- Test on out-of-sample data
- Use walk-forward testing
- Validate across market conditions
- Keep parameters conservative

### Pitfall 2: Survivorship Bias

Problem: Only testing current assets ignores historical failures.

Solution:
- Test on complete historical period
- Include delisted tokens if possible
- Account for regime changes

### Pitfall 3: Look-Ahead Bias

Problem: Using future data in backtesting.

Solution:
- Verify close times in backtest
- Confirm no forward-looking calculations
- Use conservative signal confirmation

## Seasonal Adjustments

### Market Condition Adjustments

**During High Volatility (VIX > 20 or ATR spike)**
- Increase stop loss to 2.5-3.0 ATR
- Reduce risk per trade to 1%
- Expect lower win rates

**During Low Volatility (Consolidation)**
- Consider disabling strategy
- Or reduce volume requirement
- Expect few high-quality signals

**During Trending Markets**
- Tight stops work well (1.5-2.0 ATR)
- Higher risk acceptable
- Expect high win rates

## Documentation Template

For each parameter change, record:

```
Date: [YYYY-MM-DD]
Parameter Changed: [Name]
Old Value: [Value]
New Value: [Value]
Reason: [Why changed]

Backtest Period: [Dates]
Trades Executed: [Count]

Results:
- Win Rate: [Old]% -> [New]%
- Sharpe Ratio: [Old] -> [New]
- Profit Factor: [Old] -> [New]
- Max Drawdown: [Old]% -> [New]%

Decision: ACCEPT / REJECT
Rationale: [Why accept or reject]

Next Action: [What to test next]
```

## Quarterly Review Process

Every 3 months:

1. Backtest current parameters on recent 3-month data
2. Compare results to baseline expectations
3. If performance degraded:
   - Review market condition changes
   - Retest baseline parameters
   - Adjust if needed
4. If performance improved:
   - Document changes
   - Validate on extended data
   - Consider for live trading
5. Document all findings

## Parameter Presets

### Conservative Profile
For capital preservation:
- Risk per trade: 1%
- Stop loss multiple: 2.5
- Take profit multiple: 3.75
- Volume ratio: 2.0
- Expected: 50-55% win rate, 0.9+ Sharpe

### Balanced Profile
Default recommended:
- Risk per trade: 2%
- Stop loss multiple: 2.0
- Take profit multiple: 3.0
- Volume ratio: 1.5
- Expected: 55-60% win rate, 0.8+ Sharpe

### Aggressive Profile
For higher returns:
- Risk per trade: 3%
- Stop loss multiple: 1.5
- Take profit multiple: 2.25
- Volume ratio: 1.2
- Expected: 58-65% win rate, 0.7+ Sharpe

## Reversion to Baseline

If optimized parameters underperform:

1. Revert to default parameters
2. Run 1-week live trading with defaults
3. Compare live results to backtest
4. If backtest matches live: Issue is execution/conditions
5. If backtest doesn't match: Issue is strategy/market change

Never continue with parameters showing degradation.

Last Updated: January 16, 2026
