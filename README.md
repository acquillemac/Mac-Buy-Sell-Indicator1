# Mac Buy/Sell Indicator

A Pine Script v6 indicator combining a **SuperTrend-ATR core** with a full **Smart Money Concepts (SMC)** overlay. Originally forked from the Zimpact Buy/Sell Signal.

<!-- TODO: insert chart screenshot -->

## Features

### v4 — current
- **Order Blocks** — last opposing candle before a BOS, drawn as demand/supply box, extended right until mitigated (close-through) or count cap.
- **Liquidity Sweeps** — wick beyond a recent pivot with close back inside; labeled `Sweep ▲` (bearish) / `Sweep ▼` (bullish).
- **On-chart legend table** — toggleable, top-right; documents every label/box color.

### v3 — SMC base
- Auto **Support / Resistance zones** (clustered, ATR-width).
- **BOS** (Break of Structure) and **CHoCH** (Change of Character) labels.
- **Market structure** labels: `HH`, `HL`, `LH`, `LL`.
- **Fair Value Gaps** (FVG / imbalance zones).
- **Premium / Discount EQ midline** (50% of last swing range).

### v2 — Recreation
- **EMA crossover filter** (9/21) to cut false signals.
- **Auto-close** on opposite signal, **win-rate stats** table.
- **TP1 hit marker**, **TP / SL horizontal lines** & **right-side price labels**.
- **Commission %** & **slippage ticks** inputs.
- Multi-channel **alerts** (Webhook JSON + email/push).

### v1 — Zimpact baseline
- ATR / RMA / SuperTrend core with Buy/Sell signals on direction flip.

---

## Installation

1. Open **TradingView** → **Pine Editor** (bottom panel).
2. Click **Open** → **New blank script**.
3. Delete the default contents and paste the full source of `Mac_BuySell_Indicator.pine`.
4. Click **Save**, name it *Mac Buy/Sell Indicator*, then **Add to chart**.

Requires **Pine Script v6** (TradingView default as of 2024).

---

## Settings reference

### Core
| Input | Default | Description |
|---|---|---|
| ATR Length | 14 | ATR period |
| ATR Multiplier | 1.5 | SuperTrend band width × ATR |
| MA Length (Teal) | 24 | Secondary RMA length |

### Trade Levels
| Input | Default | Description |
|---|---|---|
| TP1 x ATR | 1.5 | First take-profit distance |
| TP2 x ATR | 3.0 | Second take-profit distance |
| Show TP Levels | true | Draw TP horizontal lines |

### Filters
| Input | Default | Description |
|---|---|---|
| Use EMA Cross Filter | true | Gate signals on 9/21 EMA cross |
| EMA Fast Length | 9 | — |
| EMA Slow Length | 21 | — |

### Backtest
| Input | Default | Description |
|---|---|---|
| Commission % | 0.0 | Reference only — for future use |
| Slippage (ticks) | 0 | — |

### Visuals
| Input | Default | Description |
|---|---|---|
| Show Background Color | true | Green/red trend shading |
| Show Win-Rate Stats | true | Bottom-left stats table |
| **Show On-Chart Legend** | true | **v4** Top-right color/symbol key |

### Structure (SMC)
| Input | Default | Description |
|---|---|---|
| Show S/R Zones | true | Auto support/resistance boxes |
| Show BOS / CHoCH | true | Structure-break labels |
| Show Market Structure | true | HH/HL/LH/LL pivot labels |
| Show Fair Value Gaps | true | 3-candle imbalance zones |
| Show Premium / Discount | true | 50% EQ midline |
| Pivot Lookback | 5 | Bars each side for pivot confirmation |
| Max S/R Zones | 5 | Per side cap |
| Zone Width (ATR mult) | 0.5 | S/R box thickness |
| Min FVG Size (ATR mult) | 0.5 | Filter tiny noise gaps |
| Max FVG Zones | 3 | Total FVG boxes drawn |
| BOS Lookback Bars | 10 | How recent a pivot must be |
| **Show Order Blocks** | true | **v4** Demand/supply boxes |
| **Max Order Blocks (per side)** | 3 | **v4** OB cap per side |
| **OB Extend Bars (right)** | 50 | **v4** How far OBs extend |
| **Delete OB on Mitigation** | true | **v4** Auto-remove mitigated OBs |
| **Show Liquidity Sweeps** | true | **v4** Wick-beyond-pivot detection |
| **Sweep Lookback Bars** | 10 | **v4** Pivot recency for sweeps |

---

## Trading logic — the decision tree

1. **Trend bias** — background color (green = up, red = down). Don't fight it.
2. **Context** — EQ midline: above = premium (look for shorts), below = discount (look for longs).
3. **Confirmation** — BOS = trend continuation; CHoCH = potential reversal.
4. **Entry trigger** — Buy/Sell label from SuperTrend + EMA filter.
5. **Risk** — SL at the SuperTrend band (ratchets with the trend). TPs at ATR multiples.
6. **Confluence bonus** — Order Blocks, Sweeps, FVGs near the entry zone raise conviction.

### Highest-probability setups
| Setup | Bias |
|---|---|
| Buy signal in discount + bullish structure (HH/HL) + bullish BOS | Highest conviction long |
| Sell signal in premium + bearish structure (LH/LL) + bearish BOS | Highest conviction short |
| Liquidity sweep + BOS in same direction | Liquidity grab + continuation |
| CHoCH against prevailing trend | Possible reversal — wait for confirmation |

---

## Version history

See [CHANGELOG.md](./CHANGELOG.md) for full per-version detail.

---

## License

MIT — free to use, modify, and distribute with attribution.
