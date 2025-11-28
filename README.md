# Order Flow Imbalance Indicator

A TradingView Pine Script indicator that highlights intrabar order-flow imbalances as price zones and a companion data table. Key features:

- Detects the strongest buy/sell imbalance in each bar and draws an order block that tracks until filled or expires.
- Filters blocks by configurable imbalance ratio, volume multiplier, spacing, lifespan, and maximum active count (default ratio 4:1).
- Flags stacked imbalances (same-side blocks close in price or on consecutive bars) and retests of open blocks directly on chart boxes and in the Key Levels table.
- Surfaces standout intrabar imbalances with a persistent Key Levels memory (keeps notable ratios since the script was loaded) while preferring the freshest bars first and marking when an active block sits on top of the level.
- Displays per-bar order-flow clusters for the last six candles using ATR-sized price buckets (green for buys, purple for sells), plus a rolling “top ticks” strip that ranks the highest-volume price buckets over the last ~20 bars.
- (Optional) Draws compact trade markers (entry/stop/TP1/TP2) whenever a block is retested, and greys them out when the block is filled or expires.
- Alerts fire for new imbalance blocks, retests of active zones, and when an active block is filled.

## Inputs
- **Levels per Bar**: Number of price segments to evaluate inside each candle.
- **Min Ratio for Block** / **Min Volume Multiplier**: Thresholds to qualify a new imbalance zone (extra-high ratios can still print blocks even if volume is only average).
- **Max Active Blocks** / **Min Points Between Blocks**: Controls chart clutter while also defining the gap used to flag stacked blocks.
- **Bars to Keep Unfilled Blocks**: Lifespan for open zones before they expire and fade out if not filled.
- **Trade Markers**: Toggle plotting trade cues and configure TP reward:risk steps.
- **Colors**: Customize buy, sell, and accent colors.
- **Alerts**: Toggle alerts for new blocks, retests, and filled blocks.

## Notes
- The script estimates buy/sell split using candle structure heuristics; it does not access TradingView footprint data directly.
- Blocks fade when price trades through them, retests are highlighted, stacked blocks are emphasized, and stale unfilled blocks expire automatically after their configured lifespan.
