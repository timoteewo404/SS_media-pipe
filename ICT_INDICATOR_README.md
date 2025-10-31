# ICT Demystifying 2 - Advanced TradingView Indicator

## Overview
This TradingView Pine Script indicator implements key concepts from the "Demystifying ICT 2" book, providing advanced institutional trading analysis tools based on Inner Circle Trader (ICT) methodology.

## Key Features

### 1. Power of Three (PO3) Dealing Ranges
- **Tesla 3-6-9 Inspired**: Based on Nikola Tesla's mathematical principles
- **Multiplier Options**: Choose from 3, 9, 27, 81, or 243
- **Dynamic Support/Resistance**: PO3 levels scale with ATR (Average True Range) for adaptive zones
- **Multiple Levels**: Display 1-5 levels above and below current price

### 2. Huddleston Levels
- Key institutional price delivery points
- Identifies critical support/resistance zones used by smart money
- Includes:
  - High/Low extremes
  - Midpoint equilibrium
  - Quarter levels (Q1 and Q3)

### 3. IPDA (Institutional Price Delivery Arrays)
- Tracks institutional price targets
- Premium/Discount zones using Golden Ratio (0.618)
- Equilibrium level for balanced trading
- Identifies where institutional orders are likely positioned

### 4. AMD Cycles (Accumulation, Manipulation, Distribution)
- **Accumulation Phase**: Smart money builds positions (default: 9 hours)
- **Manipulation Phase**: Price moves to trigger stops and create liquidity (default: 6 hours)
- **Distribution Phase**: Smart money exits positions (default: 9 hours)
- Session alignment with major trading centers (Asia, London, NY)
- Visual background coloring for each phase
- Customizable session times and colors

### 5. 20-40-60 Lookback Periods
- **20-period**: Short-term trend analysis
- **40-period**: Medium-term cycle identification
- **60-period**: Longer-term structural levels
- Identifies highs/lows for each timeframe

### 6. Order Blocks (OB)
- Bullish Order Blocks: Areas where buying pressure accumulated
- Bearish Order Blocks: Areas where selling pressure accumulated
- Visual boxes showing active order block zones
- Customizable lookback period (5-100 bars)

### 7. Fair Value Gaps (FVG)
- Identifies price imbalances between consecutive candles
- Bullish FVG: Gap indicating upward pressure
- Bearish FVG: Gap indicating downward pressure
- These gaps often act as magnets for future price action

### 8. External Ranges
- Projects liquidity zones beyond current price range
- Uses Fibonacci extensions (0.382)
- Identifies where price may seek liquidity outside established ranges

### 9. Equilibrium Modes
- **All**: Display all levels and indicators
- **High/Low**: Focus on extreme levels only
- **Midpoint**: Show equilibrium center points
- **Quarters**: Display quarter-level subdivisions

## Usage Instructions

### Installation
1. Open TradingView
2. Create a new Pine Script indicator
3. Copy the entire code from `goldbach_indicator.pine`
4. Save and add to chart

### Recommended Settings

#### For Day Trading (Intraday)
- PO3 Multiplier: 27
- IPDA Lookback: 60
- Order Block Lookback: 20
- FVG Lookback: 20
- External Range Lookback: 40

#### For Swing Trading
- PO3 Multiplier: 81 or 243
- IPDA Lookback: 100-200
- Order Block Lookback: 40-60
- FVG Lookback: 30-40
- External Range Lookback: 60-100

#### For Scalping (1-5 min charts)
- PO3 Multiplier: 9 or 27
- IPDA Lookback: 40
- Order Block Lookback: 10-15
- FVG Lookback: 10-15
- External Range Lookback: 20-30

### AMD Session Configuration
Default sessions align with major trading centers:
- **Accumulation**: 00:00-09:00 UTC (Asia session)
- **Manipulation**: 09:00-15:00 UTC (London session)
- **Distribution**: 15:00-24:00 UTC (NY session)

Adjust these based on your trading timezone and market focus.

## Alerts
The indicator includes built-in alert conditions for:
- Price crossing IPDA equilibrium (above/below)
- New bullish order block formation
- New bearish order block formation
- Bullish FVG detection
- Bearish FVG detection

## Trading Strategy Guidelines

### Entry Signals
1. **Bullish Setup**:
   - Price at IPDA discount zone
   - Bullish order block present
   - Bullish FVG below current price
   - Accumulation phase active

2. **Bearish Setup**:
   - Price at IPDA premium zone
   - Bearish order block present
   - Bearish FVG above current price
   - Distribution phase active

### Key Principles
- **Power of Three**: Look for setups aligned with PO3 levels
- **AMD Awareness**: Trade in direction of current cycle phase
- **FVG Fills**: Expect price to return and fill fair value gaps
- **Order Block Reactions**: Watch for bounces at order block zones
- **Liquidity Sweeps**: External ranges often get tested before reversals

## Technical Details

### Efficiency
- Optimized for intraday timeframes (1min to 1hour)
- Maximum 500 boxes, lines, and labels for performance
- Dynamic calculations update on each bar

### Calculations
- **PO3 Range**: `ATR(14) * PO3_Value / 100`
- **IPDA Premium**: `Mid + (High - Mid) * 0.618`
- **IPDA Discount**: `Mid - (Mid - Low) * 0.618`
- **External Targets**: `High/Low ± Range * 0.382`

## References
- Based on "Demystifying ICT 2" book concepts
- Inspired by dmn's ICT AMD-Goldbach indicator
- Incorporates algorithmic and institutional trading models
- Tesla's 3-6-9 mathematical principles

## Version
- Pine Script Version: 5
- Indicator Version: 1.0
- Created: 2025

## Disclaimer
This indicator is for educational purposes only. Always conduct your own analysis and risk management before trading. Past performance does not guarantee future results.
