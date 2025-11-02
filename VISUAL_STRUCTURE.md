# Goldbach Fundamentals Indicator - Visual Structure

## Indicator Component Hierarchy

```
┌─────────────────────────────────────────────────────────────────┐
│           GOLDBACH FUNDAMENTALS INDICATOR                        │
│                   (Overlay = True)                               │
└─────────────────────────────────────────────────────────────────┘
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
┌───────▼──────┐    ┌─────────▼────────┐    ┌──────▼───────┐
│   FIX PRICE  │    │  GOLDBACH LEVELS │    │  IPDA ZONES  │
│   (Anchor)   │    │   (PO3 Based)    │    │ (Institutional)│
└──────────────┘    └──────────────────┘    └──────────────┘
      │                     │                       │
   ┌──┴──┐           ┌─────┴──────┐         ┌─────┴──────┐
   │Daily│           │  Premium   │         │  Premium   │
   │Open │           │  (3 Levels)│         │   (75%)    │
   │Prev │           │            │         │            │
   │Close│           │  Discount  │         │Equilibrium │
   └─────┘           │  (3 Levels)│         │   (50%)    │
                     └────────────┘         │            │
                                            │  Discount  │
                                            │   (25%)    │
                                            └────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                      AMD CYCLES (Background)                     │
├─────────────────────────────────────────────────────────────────┤
│  🔵 Accumulation  │  🟡 Manipulation  │  🔴 Distribution       │
│  (Range Building) │  (Stop Hunts)     │  (Trending Phase)      │
└─────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                    PRICE ACTION MARKERS                          │
├───────────────────┬─────────────────────┬───────────────────────┤
│   ORDER BLOCKS    │  FAIR VALUE GAPS    │   DEALING RANGES      │
│                   │                     │                       │
│  🟩 Bullish OB    │  🟢 Bullish FVG     │  🟣 Dealing High      │
│  (Demand Zone)    │  (Gap Up)           │  🟣 Dealing Mid       │
│                   │                     │  🟣 Dealing Low       │
│  🟥 Bearish OB    │  🟤 Bearish FVG     │                       │
│  (Supply Zone)    │  (Gap Down)         │  🟪 External High     │
│                   │                     │  🟪 External Low      │
└───────────────────┴─────────────────────┴───────────────────────┘
```

## Layered Visualization

```
Price Chart View (Overlay):

    External High ─────────────────── 🟪 (Fuchsia Cross)
          │
    Premium L3 ────────────────────── 🟢 (Green, 60% transparency)
    Premium L2 ────────────────────── 🟢 (Green, 40% transparency)
    Premium L1 ────────────────────── 🟢 (Green, 20% transparency)
          │
    IPDA Premium Zone ═══════════════ 🔴 (Red Fill, 95% transparency)
          │
    IPDA Equilibrium ─────────────── 🟠 (Orange Line)
          │
    FIX PRICE ═══════════════════════ ⚪ (White Cross) ◄── CENTRAL ANCHOR
          │
    IPDA Equilibrium (cont) ──────── 🟠 (Orange Line)
          │
    IPDA Discount Zone ══════════════ 🟢 (Green Fill, 95% transparency)
          │
    Discount L1 ─────────────────────── 🔴 (Red, 20% transparency)
    Discount L2 ─────────────────────── 🔴 (Red, 40% transparency)
    Discount L3 ─────────────────────── 🔴 (Red, 60% transparency)
          │
    External Low ───────────────────── 🟪 (Fuchsia Cross)

    Background: 🔵/🟡/🔴 (AMD Phase)
    
    Boxes floating: 
    - 🟩/🟥 Order Blocks (price action dependent)
    - 🟢/🟤 Fair Value Gaps (where price left imbalances)
```

## Data Flow Diagram

```
┌──────────────────┐
│   USER INPUTS    │
│  - PO3 Value     │
│  - Fix Price Type│
│  - AMD Sessions  │
│  - Show Toggles  │
└────────┬─────────┘
         │
         ▼
┌─────────────────────────────────────────────────────────────┐
│                    CALCULATIONS ENGINE                       │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  1. Fix Price        ──► Daily Open / Prev Close / Current  │
│  2. Goldbach Levels  ──► Fix Price ± (PO3 × Multiplier)    │
│  3. IPDA Zones       ──► Highest/Lowest over Lookback       │
│  4. AMD Detection    ──► Current Hour vs Session Ranges     │
│  5. Order Blocks     ──► Price Action Pattern Detection     │
│  6. FVG Detection    ──► 3-Candle Gap Analysis             │
│  7. Dealing Range    ──► Session High/Low + Extensions      │
│                                                              │
└────────┬────────────────────────────────────────────────────┘
         │
         ▼
┌─────────────────────────────────────────────────────────────┐
│                    VISUALIZATION LAYER                       │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  • plot() statements for lines                              │
│  • fill() for IPDA zones                                    │
│  • box.new() for OB and FVG                                 │
│  • bgcolor() for AMD phases                                 │
│  • label.new() for status display                           │
│                                                              │
└────────┬────────────────────────────────────────────────────┘
         │
         ▼
┌─────────────────────────────────────────────────────────────┐
│                      CHART DISPLAY                           │
│                   (TradingView Chart)                        │
└─────────────────────────────────────────────────────────────┘
```

## Trading Decision Tree

```
                    ┌──────────────┐
                    │  NEW CANDLE  │
                    └──────┬───────┘
                           │
                    ┌──────▼────────┐
                    │ Check AMD     │
                    │ Background    │
                    └──────┬────────┘
                           │
              ┌────────────┼────────────┐
              │            │            │
          ┌───▼───┐   ┌───▼───┐   ┌───▼───┐
          │ ACCUM │   │ MANIP │   │ DISTR │
          │ 🔵    │   │ 🟡    │   │ 🔴    │
          └───┬───┘   └───┬───┘   └───┬───┘
              │           │            │
              └───────────┼────────────┘
                          │
                   ┌──────▼───────┐
                   │ Check IPDA   │
                   │ Position     │
                   └──────┬───────┘
                          │
             ┌────────────┼─────────────┐
             │            │             │
        ┌────▼────┐  ┌───▼────┐  ┌────▼────┐
        │PREMIUM  │  │  EQ    │  │DISCOUNT │
        │ 🔴      │  │  🟠    │  │  🟢     │
        │(Sell?)  │  │(Wait)  │  │(Buy?)   │
        └────┬────┘  └────────┘  └────┬────┘
             │                         │
        ┌────▼─────┐             ┌────▼─────┐
        │Find Bear │             │Find Bull │
        │OB or FVG │             │OB or FVG │
        └────┬─────┘             └────┬─────┘
             │                         │
        ┌────▼─────┐             ┌────▼─────┐
        │  SHORT   │             │  LONG    │
        │  SETUP   │             │  SETUP   │
        └──────────┘             └──────────┘
```

## Alert Trigger Flow

```
┌────────────────────────────────────────────────────────────┐
│                    ALERT CONDITIONS                         │
├────────────────────────────────────────────────────────────┤
│                                                             │
│  Bullish FVG Valid  ────────────►  Alert: "Bullish FVG"   │
│                                                             │
│  Bearish FVG Valid  ────────────►  Alert: "Bearish FVG"   │
│                                                             │
│  Price Cross Above IPDA EQ  ────►  Alert: "Enter Premium"  │
│                                                             │
│  Price Cross Below IPDA EQ  ────►  Alert: "Enter Discount" │
│                                                             │
│  is_manipulation == true  ───────►  Alert: "Manipulation"  │
│                                                             │
│  is_distribution == true  ───────►  Alert: "Distribution"  │
│                                                             │
└────────────────────────────────────────────────────────────┘
```

## Configuration Matrix

```
╔═══════════════════╦═══════════════╦═══════════════╦═══════════════╗
║   Trading Style   ║   Scalping    ║  Day Trading  ║ Swing Trading ║
╠═══════════════════╬═══════════════╬═══════════════╬═══════════════╣
║ Timeframe         ║ 1m - 5m       ║ 15m - 1h      ║ 4h - 1D       ║
║ PO3 Value         ║ 9 or 27       ║ 27 or 81      ║ 81 or 243     ║
║ IPDA Lookback     ║ 10-15         ║ 20            ║ 30-50         ║
║ OB Lookback       ║ 5-7           ║ 10            ║ 20-30         ║
║ FVG Min Size      ║ 0.2-0.5 ATR   ║ 0.0 (all)     ║ 0.0 (all)     ║
║ Dealing Range     ║ 10-15         ║ 20            ║ 30-50         ║
║ Session Focus     ║ Manipulation  ║ All 3 Phases  ║ Distribution  ║
╚═══════════════════╩═══════════════╩═══════════════╩═══════════════╝
```

## Color Legend Quick Reference

```
LINES:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚪ White Cross Line        Fix Price (Central Anchor)
🟢 Green Lines             Premium Goldbach Levels
🔴 Red Lines               Discount Goldbach Levels
🔵 Blue Circles            IPDA High/Low Points
🟠 Orange Line             IPDA Equilibrium (50%)
🟣 Purple Lines            Dealing Range
🟪 Fuchsia Crosses         External Ranges

ZONES (Fills):
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🔴 Red Tint               IPDA Premium (Sell Zone)
🩶 Gray Tint              IPDA Equilibrium (Neutral)
🟢 Green Tint             IPDA Discount (Buy Zone)

BACKGROUNDS:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🔵 Blue Background        Accumulation Phase
🟡 Yellow Background      Manipulation Phase
🔴 Red Background         Distribution Phase

BOXES:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🟩 Green Box              Bullish Order Block (Demand)
🟥 Red Box                Bearish Order Block (Supply)
🟢 Lime Box               Bullish FVG (Gap Up)
🟤 Maroon Box             Bearish FVG (Gap Down)
```

## Integration with Goldbach Book Concepts

```
┌──────────────────────────────────────────────────────────────┐
│            GOLDBACH FUNDAMENTALS BOOK CONCEPTS               │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  Mathematical Approach    ──►  PO3 Sequence (3^n)           │
│  Fractal Structure        ──►  Nested Levels                │
│  Institutional Behavior   ──►  IPDA Zones                   │
│  Market Phases            ──►  AMD Cycles                   │
│  Price Imbalances         ──►  Fair Value Gaps              │
│  Supply/Demand Zones      ──►  Order Blocks                 │
│  Central Reference        ──►  Fix Price                    │
│  Extended Targets         ──►  External Ranges              │
│  Self-Application         ──►  Works All Timeframes/Assets  │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

---

This visual structure document helps understand how all components work together in the Goldbach Fundamentals Indicator.
