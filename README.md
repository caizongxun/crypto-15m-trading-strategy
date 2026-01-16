# Cryptocurrency 15-Minute Multi-Layer Trading Strategy

A professional-grade Pine Script trading strategy designed for 15-minute cryptocurrency trading using a three-layer confirmation system targeting a 1:1.5 risk-reward ratio and Sharpe ratio approaching 1.0.

## Strategy Overview

This strategy implements a multi-layer confirmation system to balance high win rates with sufficient trading signals, eliminating the traditional trade-off between being overly strict (no signals) and overly permissive (false signals).

### Core Architecture

The strategy employs three independent confirmation layers:

1. **Trend Confirmation Layer**: Moving Average alignment (5, 20, 60)
   - Filters non-trending market environments
   - Rejects choppy consolidation periods

2. **Momentum Confirmation Layer**: MACD + RSI signals
   - Ensures actual momentum exists behind price movement
   - Eliminates mechanical breakouts without follow-through

3. **Volume Confirmation Layer**: Volume and pattern analysis
   - Validates breakouts with volume expansion
   - Confirms pattern formations
   - Detects divergence signals

Only trades where all three layers are satisfied.

## File Structure

```
crypto-15m-trading-strategy/
trading-strategy/
├── crypto_15m_strategy.pine        # Main trading strategy (production)
├── README.md                       # This file
├── docs/
│   ├── IMPLEMENTATION_GUIDE.md    # Setup and usage instructions
│   ├── PARAMETER_TUNING.md        # Optimization methodology
│   └── QUICK_REFERENCE.md         # Trading checklist and parameters
└── backtest_data/
    └── performance_metrics.csv     # Sample backtest results
```

## Quick Start

### 1. Import Strategy to TradingView

1. Open TradingView, navigate to Pine Editor
2. Create new script and copy entire content from `crypto_15m_strategy.pine`
3. Click "Add to Chart"
4. Configure parameters as needed

### 2. Key Parameters

| Parameter | Default | Range | Description |
|-----------|---------|-------|-------------|
| Initial Capital | 1000 | - | Backtest starting capital |
| Risk Per Trade | 2.0% | 0.5-5% | Maximum loss per trade |
| Risk/Reward Ratio | 1.5 | 0.5-3.0 | Profit target vs stop loss ratio |
| Fast MA | 5 | 3-20 | Ultra-short term trend |
| Mid MA | 20 | 10-50 | Short-term trend |
| Slow MA | 60 | 30-200 | Long-term trend baseline |
| Stop Loss Multiple | 2.0 | 1.0-3.0 | ATR multiplier for stops |
| Take Profit Multiple | 3.0 | 1.5-5.0 | ATR multiplier for targets |

### 3. Entry Signals

**Long Entry Requirements**:
- Fast MA > Mid MA > Slow MA (uptrend alignment)
- MACD bullish crossover OR RSI crosses above oversold level
- Volume > 20-bar average × 1.5
- Optional: Bullish pattern (hammer, engulfing) or divergence

**Short Entry Requirements**:
- Fast MA < Mid MA < Slow MA (downtrend alignment)
- MACD bearish crossover OR RSI crosses below overbought level
- Volume > 20-bar average × 1.5
- Optional: Bearish pattern (inverted hammer, engulfing) or divergence

### 4. Risk Management

**Position Sizing Formula**:
```
Stop Loss Distance = ATR(14) × 2.0
Take Profit Distance = ATR(14) × 3.0
Position Size = (Account × Risk %) / Stop Loss Distance

Example with $1000 account, ATR=$50:
Stop Loss Distance = $100
Take Profit Distance = $150
Position Size = $20 / $100 = 0.2 lot
Risk/Reward = 150/100 = 1.5
```

**Drawdown Protection**:
- Maximum consecutive losses: 3 trades then pause
- Daily maximum loss: 3% of account (default, configurable)
- Trailing stop loss enabled by default

## Performance Targets

| Metric | Target | Interpretation |
|--------|--------|----------------|
| Win Rate | 55-65% | Higher win rates may indicate overfitting |
| Sharpe Ratio | 0.8+ | Risk-adjusted returns metric |
| Profit Factor | 1.5+ | Gross profit / Gross loss |
| Maximum Drawdown | <15% | Largest peak-to-trough decline |
| Monthly Return | 1-3% | Sustainable growth rate |

## Best Practices

### Trading Environment

**Recommended Pairs**:
- BTC/USDT (highest liquidity)
- ETH/USDT (high liquidity)
- SOL/USDT (moderate liquidity)

**Avoid**:
- Low-volume altcoins
- New tokens (manipulation risk)
- During major news events

### Backtesting

- Minimum 3 months of historical data
- Test multiple market conditions (uptrend, downtrend, consolidation)
- Commission set to 0.05% per round trip
- Review equity drawdown curves

### Parameter Optimization

**Do NOT**:
- Change MA periods
- Modify MACD(12,26,9) or RSI(14) - these are industry standard
- Over-optimize to historical data

**Safe to Adjust**:
- ATR multiples (stop loss, take profit)
- Volume confirmation ratio
- Risk per trade percentage
- Divergence lookback period

### Common Issues and Solutions

**Issue: Win Rate Below 50%**
- Increase minimum volume ratio from 1.5 to 2.0
- Enable divergence detection
- Switch trading pair to higher liquidity instrument

**Issue: No Entry Signals**
- Reduce minimum volume ratio to 1.2
- Disable optional pattern requirements
- Check if market is in consolidation (ATR ratio < 0.8)

**Issue: Consecutive Losses**
- Reduce position size (risk per trade)
- Check market volatility (ATR ratio)
- Verify trading pair liquidity
- Pause trading if 3+ losses occur

**Issue: High Drawdown**
- Reduce risk per trade from 2% to 1%
- Increase stop loss multiple from 2.0 to 2.5
- Check for news events or market gaps

## Technical Specifications

### Indicators Used

1. **Moving Averages** (SMA)
   - 5-period: Ultra-short trend detection
   - 20-period: Short-term support/resistance
   - 60-period: Long-term trend direction

2. **MACD** (12, 26, 9)
   - Momentum and trend confirmation
   - Divergence detection for reversals
   - Crossover signals for entries

3. **RSI** (14)
   - Overbought/oversold conditions
   - Divergence signals
   - Momentum strength assessment

4. **ATR** (14)
   - Dynamic position sizing
   - Stop loss and take profit levels
   - Volatility-adjusted entries

5. **Volume**
   - 20-bar simple moving average
   - Entry signal confirmation
   - Breakout validation

### Pattern Recognition

The strategy identifies and confirms entry signals using:

- **Hammer**: Lower shadow > 60% of range, upper shadow < 10%
- **Inverted Hammer**: Upper shadow > 60% of range, lower shadow < 10%
- **Bullish Engulfing**: Red candle followed by green candle containing it
- **Bearish Engulfing**: Green candle followed by red candle containing it
- **Divergence**: Price new extreme vs. indicator failing to confirm

## Commission and Slippage Considerations

Default settings assume:
- Commission: 0.05% per round trip (typical crypto exchange)
- Slippage: Already factored into backtest results
- Spread: Negligible for major pairs on liquid exchanges

For lower-liquidity pairs, increase expected slippage by 0.1-0.5%.

## Risk Disclaimer

This strategy is provided for educational and research purposes only. Past performance does not guarantee future results. Cryptocurrency trading involves substantial risk of loss and is not suitable for all investors.

Key risks include:
- Liquidity risk (especially for altcoins)
- Gap risk during market opening
- Flash crash risk in volatile markets
- Regulatory risk
- Exchange risk

Always start with small position sizes and thoroughly backtest on historical data before deploying real capital.

## Configuration Examples

### Conservative (Low Drawdown)
```
Risk Per Trade: 1%
Stop Loss Multiple: 2.5
Take Profit Multiple: 4.0
Min Volume Ratio: 2.0
Divergence Detection: Enabled
```

### Balanced (Recommended)
```
Risk Per Trade: 2%
Stop Loss Multiple: 2.0
Take Profit Multiple: 3.0
Min Volume Ratio: 1.5
Divergence Detection: Enabled
```

### Aggressive (High Signals)
```
Risk Per Trade: 3%
Stop Loss Multiple: 1.5
Take Profit Multiple: 2.0
Min Volume Ratio: 1.2
Divergence Detection: Optional
```

## Additional Resources

- See `docs/IMPLEMENTATION_GUIDE.md` for detailed setup instructions
- See `docs/PARAMETER_TUNING.md` for optimization methodology
- See `docs/QUICK_REFERENCE.md` for trading checklists and parameter quick lookup

## Version History

**Current Version**: 1.0
- Three-layer confirmation system
- Advanced divergence detection
- Pattern recognition (hammer, engulfing)
- Dynamic trailing stop
- Professional statistics display

## License

MIT License - Free to use and modify for personal trading purposes. Attribution appreciated.

## Support and Updates

For issues, improvements, or suggestions, please review the documentation or contact the maintainer.

Last Updated: January 16, 2026
