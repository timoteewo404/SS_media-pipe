# Goldbach Fundamentals Indicator

## Overview
This TradingView Pine Script indicator implements the concepts from the **Goldbach Fundamentals book by hopiplaka (190-page edition)**. It provides a comprehensive framework for fractal market analysis using mathematical approaches and institutional trading concepts.

## Key Features

### 1. Power of Three (PO3) Sequence
- **Selectable PO3 Values**: 9, 27, 81, 243, 729 (powers of 3: 3², 3³, 3⁴, 3⁵, 3⁶)
- **Goldbach Levels**: Multiple levels above and below the fix price based on PO3 multipliers
- **Fractal Structure**: Implements the mathematical/fractal approach central to Goldbach methodology

### 2. Fix Price (Central Anchor Point)
- **Daily Open**: Uses the start of the trading day as the anchor
- **Previous Day Close**: Uses the close of the previous trading session
- **Current Close**: Dynamic anchor based on current price
- The fix price serves as the central reference point for all Goldbach levels

### 3. IPDA Levels (Institutional Price Delivery Arrays)
- **Premium Zone**: 75%-100% of range (institutional selling zone)
- **Equilibrium**: 50% level (fair value / optimal trade entry)
- **Discount Zone**: 0%-25% of range (institutional buying zone)
- **Visual Zones**: Color-coded fills showing premium (red), equilibrium (gray), and discount (green) areas
- **Dynamic Calculation**: Adapts to recent price action using configurable lookback period

### 4. AMD Cycles (Accumulation, Manipulation, Distribution)
- **Accumulation Phase**: Smart money quietly building positions
  - Background: Blue
  - Typically during low-volume/low-volatility periods
  
- **Manipulation Phase**: Stop hunts and liquidity grabs
  - Background: Yellow
  - Watch for false breakouts and reversals
  
- **Distribution Phase**: Directional moves begin
  - Background: Red
  - Main trending phase
  
- **Preset Sessions**: Asian, London, New York, or Custom time periods

### 5. Order Blocks (OB)
- **Bullish Order Blocks**: Last bearish candle before strong bullish move (demand zone)
- **Bearish Order Blocks**: Last bullish candle before strong bearish move (supply zone)
- **Visual Boxes**: Green for bullish OB, red for bearish OB
- **Institutional Footprint**: Marks where institutions likely placed significant orders

### 6. Fair Value Gaps (FVG)
- **Bullish FVG**: Gap with no overlap between low[0] and high[2]
- **Bearish FVG**: Gap with no overlap between high[0] and low[2]
- **Imbalance Zones**: Areas price likely returns to fill
- **ATR Filter**: Minimum gap size to filter out noise
- **Extended Visualization**: Boxes extend to the right showing unfilled gaps

### 7. Dealing Ranges & External Ranges
- **Dealing Range**: Current session high-low range
- **Dealing Mid**: 50% of dealing range (equilibrium)
- **External Ranges**: Extensions beyond dealing range using Fibonacci 0.618
- **Fractal Structure**: Shows nested ranges for multi-timeframe analysis

## Configuration Options

### Power of Three Settings
- **PO3 Value**: Select from 9, 27, 81, 243, 729 based on asset volatility
- **Number of Levels**: 1-5 levels above/below fix price
- **Fix Price Type**: Choose anchor point calculation method

### IPDA Settings
- **Show IPDA Levels**: Toggle institutional zones
- **Lookback Period**: 5-100 bars for range calculation

### AMD Cycle Settings
- **Show AMD Cycles**: Toggle background coloring
- **Session Type**: Asian, London, New York, or Custom
- **Custom Hours**: Set specific accumulation/manipulation/distribution times

### Order Blocks & FVG Settings
- **Show Order Blocks**: Toggle OB visualization
- **OB Lookback**: How long to keep OB boxes visible
- **Show Fair Value Gaps**: Toggle FVG boxes
- **Min FVG Size**: Filter based on % of ATR

### Dealing Range Settings
- **Show Dealing Range**: Toggle range lines
- **Show External Ranges**: Toggle extended levels
- **Period**: Lookback for range calculation

### Display Settings
- **Equilibrium Mode**: 
  - "All": Show all Goldbach levels
  - "Premium/Discount": Show premium and discount levels only
  - "Midpoint Only": Show only the central equilibrium
- **Show Labels**: Toggle AMD/IPDA status labels
- **Label Distance**: Position labels away from price action

## Alerts

The indicator includes six alert conditions:
1. **Bullish FVG Detected**: New bullish imbalance formed
2. **Bearish FVG Detected**: New bearish imbalance formed
3. **Price Above IPDA EQ**: Entering premium zone
4. **Price Below IPDA EQ**: Entering discount zone
5. **Manipulation Phase**: AMD manipulation cycle active
6. **Distribution Phase**: AMD distribution cycle active

## Usage Guidelines

### Intraday Trading
1. **Identify AMD Phase**: Check background color for current market phase
2. **Locate IPDA Position**: 
   - In discount? Look for long setups
   - In premium? Look for short setups
3. **Find Order Blocks**: Entry zones for high-probability setups
4. **Mark FVGs**: Potential targets or retracement zones
5. **Use Goldbach Levels**: Dynamic support/resistance based on PO3

### Multi-Timeframe Analysis
- **Higher Timeframe**: Identify major IPDA zones and dealing ranges
- **Entry Timeframe**: Find OB and FVG within the higher timeframe zones
- **Confirmation**: AMD cycle should align with directional bias

### Risk Management
- **Fix Price as Reference**: Gauge whether price is extended
- **External Ranges**: Extreme levels for stop placement
- **FVG Fills**: Partial profit targets as imbalances get filled

## Mathematical Foundation

The indicator follows the **Goldbach Fundamentals** approach:
- **Fractal Structure**: Markets exhibit self-similar patterns across timeframes
- **Power of Three**: Base-3 mathematics for level spacing
- **Institutional Logic**: IPDA and AMD concepts model smart money behavior
- **Self-Application**: Framework can be applied to any timeframe or asset

## Supported Timeframes

- **Optimized for**: Intraday timeframes (1m, 5m, 15m, 30m, 1h)
- **Works on**: All timeframes
- **Fix Price Logic**: Adapts behavior on intraday vs daily/weekly charts

## Credits

Based on concepts from:
- **Goldbach Fundamentals** by hopiplaka (190-page edition)
- Focus on mathematical approaches to trading
- Fractal market analysis and institutional order flow

## Version History

- **v1.0**: Initial implementation with all core features
  - PO3 Goldbach levels
  - Fix price anchor
  - IPDA zones
  - AMD cycle detection
  - Order blocks
  - Fair value gaps
  - Dealing and external ranges
  - Comprehensive alerts

---

**Disclaimer**: This indicator is for educational purposes. Past performance does not guarantee future results. Always practice proper risk management and conduct your own analysis before trading.
