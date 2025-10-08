# Goldbach AMD-PO3 Levels Indicator

## Overview

This TradingView Pine Script indicator implements the concepts from the **Goldbach Fundamentals** trading methodology, combining Power of Three (PO3) levels with intraday AMD (Accumulation, Manipulation, Distribution) cycles to identify high-probability trading zones.

## Key Features

### 1. **Goldbach Levels (PO3)**
- Calculates and plots support/resistance levels using Powers of Three (3^n)
- Configurable PO3 ranges: 27, 81, 243, or custom values
- Dynamically adjusts to market volatility
- Plots levels both above and below current price

### 2. **AMD Cycles**
The indicator divides the trading day into three distinct phases:
- **Accumulation Phase**: Smart money accumulates positions (typically 9 hours, aligned with Asia session)
- **Manipulation Phase**: Price moves to trigger stops and create liquidity (typically 6 hours, London open)
- **Distribution Phase**: Smart money distributes/exits positions (typically 9 hours, NY session)

### 3. **Order Blocks (OB)**
- Detects and visualizes bullish order blocks (last down candle before strong up move)
- Detects and visualizes bearish order blocks (last up candle before strong down move)
- Extends order blocks to the right for future reference

### 4. **Fair Value Gaps (FVG)**
- Identifies bullish fair value gaps (inefficiencies in price action)
- Identifies bearish fair value gaps
- Highlights potential retracement zones

### 5. **External Ranges**
- Plots previous day's high and low
- Provides context for current day's price action
- Useful for identifying key support/resistance levels

## Installation

1. Open TradingView and navigate to the Pine Editor
2. Copy the entire contents of `goldbach_amd_indicator.pine`
3. Paste into the Pine Editor
4. Click "Save" and give it a name
5. Click "Add to Chart"

## Configuration

### PO3 Range Settings

**PO3 Range (27/81/243)**
- Default: 81
- Recommended values:
  - **27**: Low volatility assets (forex majors, large-cap stocks)
  - **81**: Medium volatility assets (most crypto, mid-cap stocks)
  - **243**: High volatility assets (small-cap crypto, penny stocks)
  - **729**: Extreme volatility (microcaps, highly volatile crypto)

**Levels Above/Below Price**
- Default: 3 each
- Increase for longer-term trading
- Decrease for cleaner charts on lower timeframes

### AMD Cycle Time Settings

Configure the three phases to match your trading sessions:

**Accumulation Start Hour** (Default: 0)
- When the accumulation phase begins (24-hour format)
- Typically aligned with Asia session start

**Accumulation Duration** (Default: 9 hours)
- Length of accumulation phase
- Asia session: typically 9 hours

**Manipulation Duration** (Default: 6 hours)
- Length of manipulation phase
- London session: typically 6 hours

**Distribution Duration** (Default: 9 hours)
- Length of distribution phase
- NY session: typically 9 hours

### Session Times

**Asia Session** (Default: 0000-0900)
- Visual reference for Asian trading hours

**London Session** (Default: 0300-1200)
- Visual reference for London trading hours

**New York Session** (Default: 0800-1700)
- Visual reference for NY trading hours

### Display Options

Toggle visibility of various indicator components:
- **Show Goldbach Levels**: Main PO3 support/resistance levels
- **Show Order Blocks**: Bullish/bearish order block zones
- **Show Fair Value Gaps**: Price inefficiency zones
- **Show External Ranges**: Previous day high/low
- **Show AMD Blocks**: Phase-specific background colors and equilibrium lines

**Equilibrium Mode**
- **Midpoint** (Default): Uses 50% level of phase range
- **High**: Uses the high of the phase range
- **Low**: Uses the low of the phase range

### Color Settings

Fully customizable colors for all indicator elements:
- Accumulation, Manipulation, Distribution backgrounds
- Goldbach levels (bullish/bearish)
- Order blocks (bullish/bearish)
- Fair value gaps

## Trading Methodology

### Goldbach Fundamentals Approach

1. **Identify the Current AMD Phase**
   - Observe the background color and current phase label
   - Understand where you are in the daily cycle

2. **Accumulation Phase Strategy**
   - Look for price testing Goldbach levels
   - Watch for order blocks forming near levels
   - Anticipate manipulation phase moves
   - **Entry**: Near Goldbach support levels or bullish order blocks
   - **Stop**: Below the accumulation low

3. **Manipulation Phase Strategy**
   - Expect volatile price action
   - Watch for false breakouts and stop hunts
   - Look for fair value gaps being created
   - **Caution**: This phase often traps retail traders
   - Consider waiting for distribution phase confirmation

4. **Distribution Phase Strategy**
   - Look for exits at Goldbach resistance levels
   - Watch for bearish order blocks forming
   - Target FVG fills or external range highs/lows
   - **Exit**: At Goldbach resistance or during reversal signals

### Level Confluence

The strongest trading opportunities occur when multiple factors align:

1. **Price at Goldbach Level** + **AMD Phase Transition** = High probability setup
2. **Order Block** + **Fair Value Gap** + **Goldbach Level** = Maximum confluence
3. **External Range** + **Goldbach Level** = Strong support/resistance

### Timeframe Recommendations

- **Scalping (1m-5m)**: Use PO3 range of 27, focus on manipulation phase
- **Intraday (15m-1h)**: Use PO3 range of 81 (default), trade all AMD phases
- **Swing Trading (4h-Daily)**: Use PO3 range of 243, focus on phase transitions

## Examples

### Example 1: Bullish Setup in Accumulation Phase

```
Scenario:
- Price is in Accumulation phase (blue background)
- Price tests Goldbach level -2 (below reference)
- Bullish order block forms at the level
- Fair value gap below indicates previous inefficiency

Action:
- Enter long near Goldbach level with order block confirmation
- Stop loss below accumulation low
- Target: Next Goldbach level above or manipulation phase high
```

### Example 2: Distribution Phase Exit

```
Scenario:
- Price is in Distribution phase (red background)
- Price reaches Goldbach level +2 (above reference)
- Bearish order block forms
- External range high is nearby

Action:
- Exit long positions or enter short
- Stop above distribution high
- Target: Goldbach level 0 (reference) or accumulation phase low
```

## Understanding the Indicators

### Goldbach Levels
- **Green lines** (when price above reference): Bullish market structure
- **Red lines** (when price below reference): Bearish market structure
- **Gray circles**: Reference price (typically daily open)
- Spacing based on PO3 range setting

### AMD Phase Visualization
- **Blue background**: Accumulation phase - look for longs
- **Yellow background**: Manipulation phase - be cautious
- **Red background**: Distribution phase - look for exits/shorts
- **Colored lines**: Equilibrium levels for each phase

### Order Blocks
- **Green boxes**: Bullish order blocks (potential support)
- **Red boxes**: Bearish order blocks (potential resistance)
- Extend to the right until price reacts

### Fair Value Gaps
- **Purple boxes**: Price inefficiency zones
- Often get filled (price returns to gap)
- Can act as support/resistance

### Session Backgrounds
- **Light blue**: Asia session
- **Light yellow**: London session
- **Light green**: New York session
- Very subtle backgrounds for reference only

## Alerts

The indicator includes built-in alerts for:
1. **Price Crosses Reference**: When price crosses the reference price level
2. **AMD Phase Change**: When the market transitions between AMD phases
3. **Order Block Detected**: When a new order block is identified
4. **Fair Value Gap Detected**: When a new FVG is identified

To set up alerts:
1. Right-click the chart
2. Select "Add Alert"
3. Choose the alert condition from the dropdown
4. Configure notification preferences

## Technical Details

### Pine Script Version
- **Version**: Pine Script v5
- **Overlay**: Yes (plots on price chart)
- **Max Boxes**: 500
- **Max Lines**: 500

### Calculation Methods

**PO3 Levels**: 
```
Level = ReferencePrice ± (PO3_Range × Level_Number)
```

**AMD Phase Detection**:
```
Current_Phase = f(Hour, Minute, Phase_Durations)
```

**Order Block Detection**:
- Bullish: Last bearish candle before sustained bullish momentum
- Bearish: Last bullish candle before sustained bearish momentum

**Fair Value Gap Detection**:
- Bullish: Gap between high[2] and low[0] when price moves up
- Bearish: Gap between low[2] and high[0] when price moves down

## Troubleshooting

### Issue: Levels not showing
- **Solution**: Ensure "Show Goldbach Levels" is enabled in settings
- Check that PO3 range is appropriate for the asset's price

### Issue: AMD phases seem wrong
- **Solution**: Adjust accumulation start hour for your timezone
- Verify total duration of 3 phases doesn't exceed 24 hours

### Issue: Too many boxes/lines error
- **Solution**: Reduce number of Goldbach levels
- Disable some display options (FVG, Order Blocks)

### Issue: Colors not visible
- **Solution**: Adjust transparency in color settings
- Change chart background color for better contrast

## Best Practices

1. **Start Simple**: Enable only Goldbach levels and AMD phases initially
2. **Backtest**: Review historical price action to understand how levels interact
3. **Combine Tools**: Use order blocks and FVGs for confluence, not in isolation
4. **Respect Phases**: Don't fight the current AMD phase
5. **Manage Risk**: Always use stop losses at phase extremes
6. **Multiple Timeframes**: Check higher timeframes for additional confluence

## References

- **Goldbach Fundamentals Book**: Core methodology and PO3 concepts
- **ICT Concepts**: Order blocks, fair value gaps, and manipulation theory
- **dmn's ICT AMD-Goldbach**: Inspiration for combining methodologies
- **AMD-PO3-Goldbach levels**: Community implementations and variations

## Version History

**v1.0** (2025)
- Initial release
- Complete implementation of Goldbach Fundamentals concepts
- Full AMD cycle support
- Order blocks, FVG, and external ranges
- Comprehensive customization options

## Support and Contributing

For issues, suggestions, or contributions:
1. Review the existing code in `goldbach_amd_indicator.pine`
2. Test thoroughly on multiple timeframes and assets
3. Document any modifications or improvements

## License

This indicator is provided as-is for educational and trading purposes. Use at your own risk. Trading involves substantial risk of loss.

## Disclaimer

**IMPORTANT**: This indicator is a tool for analysis and does not guarantee trading success. Past performance does not indicate future results. Always:
- Do your own research
- Practice proper risk management
- Never risk more than you can afford to lose
- Consider consulting with a financial advisor

The AMD cycle times and Goldbach levels are theoretical frameworks and may not work in all market conditions.

---

**Happy Trading!** 📈

For questions or feedback, please refer to the code comments in `goldbach_amd_indicator.pine`.
