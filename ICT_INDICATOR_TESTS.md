# ICT Indicator Test Cases and Validation

## Manual Testing Checklist

### 1. Power of Three (PO3) Level Testing
- [ ] Test with PO3 Multiplier = 3
  - Verify 3 levels appear above and below price
  - Confirm levels are evenly spaced based on ATR
  
- [ ] Test with PO3 Multiplier = 27
  - Verify levels are wider than multiplier 3
  - Check dynamic adjustment with volatility
  
- [ ] Test with PO3 Multiplier = 243
  - Verify very wide levels for swing trading
  - Confirm no plotting errors

- [ ] Test Number of Levels (1-5)
  - Set to 1: Only first level appears
  - Set to 3: Three levels on each side
  - Set to 5: Maximum five levels plotted

### 2. Huddleston Levels Testing
- [ ] Default lookback (100 periods)
  - Verify High/Low markers appear
  - Check Midpoint is exactly between High and Low
  - Confirm Q1 at 25% and Q3 at 75% of range
  
- [ ] Adjust lookback period
  - Short lookback (20): More responsive to recent price
  - Long lookback (500): Captures major structure

### 3. IPDA Testing
- [ ] IPDA levels calculation
  - High = Highest of lookback period
  - Low = Lowest of lookback period
  - Mid = Exactly between High and Low
  - Premium = Mid + 61.8% of upper half
  - Discount = Mid - 61.8% of lower half

- [ ] Visual verification
  - Premium zone above equilibrium
  - Discount zone below equilibrium
  - Levels update dynamically with new highs/lows

### 4. AMD Cycle Testing
- [ ] Session detection logic
  - Accumulation: Background turns green during 00:00-09:00
  - Manipulation: Background turns blue during 09:00-15:00
  - Distribution: Background turns red during 15:00-00:00

- [ ] Custom session times
  - Change Accumulation start to 6:00
  - Change Manipulation duration to 4 hours
  - Verify background colors shift correctly

- [ ] Session labels
  - "A" labels appear during Accumulation (every 10 bars)
  - "M" labels appear during Manipulation
  - "D" labels appear during Distribution

### 5. Lookback Period Testing (20-40-60)
- [ ] Enable 20-period lookback
  - Blue lines appear at 20-period high/low
  - Lines update frequently with recent swings

- [ ] Enable 40-period lookback
  - Purple lines appear at 40-period high/low
  - Lines are more stable than 20-period

- [ ] Enable 60-period lookback
  - Orange lines appear at 60-period high/low
  - Lines capture longer-term structure

- [ ] Disable each individually
  - Verify corresponding lines disappear

### 6. Order Block Detection
- [ ] Bullish Order Block
  - Previous candle is bearish (close < open)
  - Current candle closes above previous close
  - Candle range > 1.5x ATR
  - Green box drawn from previous candle's high to low

- [ ] Bearish Order Block
  - Previous candle is bullish (close > open)
  - Current candle closes below previous close
  - Candle range > 1.5x ATR
  - Red box drawn from previous candle's high to low

- [ ] Order Block persistence
  - Box remains visible for duration of lookback period
  - Old boxes disappear after lookback period expires

### 7. Fair Value Gap (FVG) Testing
- [ ] Bullish FVG
  - Current low > high of 2 candles ago
  - Previous candle low > high of 2 candles ago
  - Blue box drawn showing the gap

- [ ] Bearish FVG
  - Current high < low of 2 candles ago
  - Previous candle high < low of 2 candles ago
  - Orange box drawn showing the gap

- [ ] FVG persistence
  - Gap box remains visible for lookback period
  - Multiple gaps can be active simultaneously

### 8. External Range Testing
- [ ] External upper target
  - Calculated as: High + (Range * 0.382)
  - Purple circles plot above recent high
  - Updates with new highs

- [ ] External lower target
  - Calculated as: Low - (Range * 0.382)
  - Yellow circles plot below recent low
  - Updates with new lows

### 9. Equilibrium Mode Testing
- [ ] "All" mode
  - All indicators and levels visible
  - Current price plotted as white line
  - PO3 midpoint and quarters visible

- [ ] "High/Low" mode
  - Only extreme levels shown
  - Current price line visible

- [ ] "Midpoint" mode
  - Gray midpoint line visible
  - Focus on equilibrium

- [ ] "Quarters" mode
  - Q1 and Q3 levels visible
  - Silver colored lines

### 10. Alert Testing
- [ ] IPDA equilibrium crossover
  - Alert triggers when price crosses above IPDA mid
  
- [ ] IPDA equilibrium crossunder
  - Alert triggers when price crosses below IPDA mid

- [ ] Order block alerts
  - Bullish OB alert on formation
  - Bearish OB alert on formation

- [ ] FVG alerts
  - Bullish FVG alert on detection
  - Bearish FVG alert on detection

## Performance Testing

### Chart Timeframes
- [ ] 1-minute chart: Indicator loads and updates smoothly
- [ ] 5-minute chart: All features functional
- [ ] 15-minute chart: Optimal performance
- [ ] 1-hour chart: Clean visualization
- [ ] 4-hour chart: Longer-term structure visible
- [ ] Daily chart: Swing trading levels accurate

### Assets to Test
- [ ] Forex pairs (EUR/USD, GBP/USD)
- [ ] Crypto (BTC/USD, ETH/USD)
- [ ] Stocks (SPY, AAPL, TSLA)
- [ ] Futures (ES, NQ)

## Expected Behaviors

### Correct Functionality
✅ PO3 levels scale with volatility (ATR-based)
✅ AMD cycles align with session times
✅ Order blocks appear after strong directional moves
✅ FVGs identify gaps in price action
✅ IPDA levels mark institutional zones
✅ Multiple features can be enabled/disabled independently
✅ No script errors or warnings
✅ Indicator overlays correctly on price chart

### Known Limitations
⚠️ Maximum 500 boxes/lines/labels per chart (Pine Script limit)
⚠️ Very low timeframes (< 1min) may have excessive signals
⚠️ High volatility periods may generate many overlapping boxes
⚠️ Session times are in UTC by default (user must adjust for local time)

## Validation Examples

### Example 1: Bullish Setup
1. Price at IPDA discount zone ✓
2. Bullish order block below current price ✓
3. Unfilled bullish FVG below ✓
4. Accumulation phase active (green background) ✓
5. Price above 20-period low ✓
→ **Strong bullish confluence**

### Example 2: Bearish Setup
1. Price at IPDA premium zone ✓
2. Bearish order block above current price ✓
3. Unfilled bearish FVG above ✓
4. Distribution phase active (red background) ✓
5. Price below 20-period high ✓
→ **Strong bearish confluence**

### Example 3: Neutral/Consolidation
1. Price at IPDA equilibrium (mid level)
2. No recent order blocks
3. FVGs have been filled
4. Manipulation phase active (blue background)
→ **Low conviction, wait for better setup**

## Troubleshooting

### Issue: Levels not appearing
- Check if feature is enabled in settings
- Verify lookback period isn't too large for chart history
- Ensure sufficient data loaded on chart

### Issue: Too many boxes/labels
- Reduce lookback periods for OB/FVG
- Disable AMD labels (showAMDLabels = false)
- Use more selective equilibrium modes

### Issue: Session colors wrong
- Verify timezone setting (default is UTC)
- Adjust session start times for your market
- Check system time is correct

### Issue: Indicator slow/laggy
- Reduce number of PO3 levels
- Disable unused features
- Use higher timeframe charts
- Clear browser cache and reload

## Sign-off Checklist

Before considering the indicator complete:
- [ ] All input parameters functional
- [ ] All visual elements render correctly
- [ ] Alerts trigger as expected
- [ ] No console errors
- [ ] Documentation complete
- [ ] Performance acceptable on multiple timeframes
- [ ] Tested on multiple assets
- [ ] User can customize all key parameters
