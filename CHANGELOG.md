# Changelog

All notable changes to **Mac Buy/Sell Indicator**.

## [v4] — 2026-08
### Added
- **Order Block detection** — last opposing candle before a BOS, drawn as demand/supply box, extended right until mitigated by close-through or count cap.
- **Liquidity Sweep detection** — wick beyond recent pivot + close back inside; labeled `Sweep ▲` (bearish) / `Sweep ▼` (bullish).
- **On-chart legend table** — toggleable, top-right; documents every label/box color.
- Renamed file to `Mac_BuySell_Indicator.pine` and updated `indicator()` title.
- New inputs: `showOB`, `maxOBs`, `obExtend`, `obMitigate`, `showSweeps`, `sweepLookback`, `showLegend`.

## [v3] — earlier
### Added (Smart Money Concepts baseline)
- Auto Support / Resistance zones (clustered, ATR-width).
- Break of Structure (BOS) labels.
- Change of Character (CHoCH) labels.
- Market Structure labels (HH / HL / LH / LL).
- Fair Value Gaps (FVG) — 3-candle imbalance zones.
- Premium / Discount midline (50% EQ of last swing).

## [v2]
### Added
- EMA crossover filter (9/21).
- Auto-close on opposite signal, win-rate stats table.
- TP1 hit marker, TP / SL horizontal lines & right-side labels.
- Commission / slippage inputs (reference).
- Multi-channel alerts (Webhook JSON + email/push).

## [v1]
### Baseline
- Zimpact Buy/Sell Signal — ATR / RMA / SuperTrend core with Buy/Sell signals on direction flip.
