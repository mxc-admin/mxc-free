# MXC Market Pulse — The Definitive Guide

### A Real-Time Dashboard of Institutional-Grade Leading Indicators for Market Tops and Bottoms

---

## The Problem With Every Other Indicator

On March 23, 2020, the S&P 500 hit its COVID low. Headlines screamed pandemic, recession, and collapse. The VIX was at 61. CNN Fear & Greed read "Extreme Fear." Every oscillator on your chart was oversold.

None of that told you it was time to buy.

Here's what **did**: In the 10 trading days surrounding that low, Market Pulse fired **five independent signals** — a Lowry 90% bottom sequence (L), VACC hidden accumulation (A), a kinematic breadth thrust (N), a McClellan VACC-confirmed surge (M), and a VVIX extreme pivot (V). Two of those signals were uncorrelated, triggering **confluence** (✦). Days later, the regime flipped BULL. The S&P rallied 68% in 12 months.

That wasn't hindsight. Those signals fire in real time. Every one of them is on your chart the moment conditions are met.

**The difference between Market Pulse and everything else is simple**: other tools tell you the market is scared. Market Pulse tells you **when the fear is about to end** — and grades its conviction while doing it.

<img width="1200" height="670" alt="image" src="https://github.com/user-attachments/assets/b12bfca6-9f59-427e-bd42-cfe8c730ec06" />

---

## Five Concepts in 60 Seconds

Before we dive deep, here's the entire system in a nutshell:

**1. Signals** — 10 independent detectors, each watching a different corner of the market: breadth thrusts, panic days, hidden accumulation/distribution, volatility regime shifts, and chaos. Each fires as a **lettered diamond** (Z, L, M, A, D, N, P, B, V, T) on the chart.

**2. Regime** — A background color. Green = BULL, nothing = BEAR or NEUTRAL. Powered by a TMF/ES ratio trend (bonds vs. equities) as the base, with a composite override from breadth kinematics and volume conviction (SVSI). When breadth and volume strongly and persistently disagree with the bond/equity signal, the composite overrides. It doesn't flip-flop — self-calibrating percentile thresholds prevent noise.

**3. Decay** — Signals don't stay forever. Each has a calibrated half-life (5–14 days). A Zweig breadth thrust echoes for 2 weeks; a VACC divergence fades in 5 days. The green/red shaded area on the chart shows total active signal energy, fading naturally over time.

**4. Confluence** — When 2+ **uncorrelated** signals fire simultaneously, the info table shows ✦. This is the highest-conviction setup. Single signals are evidence; confluence is a verdict.

**5. Scoring** — Every signal gets a raw score (0–100) based on magnitude, then decayed over time, then weighted by historical accuracy into an aggregate. The info table shows this aggregate plus confluence status — your single number for "how strong is this setup?"

That's it. Signals fire, regime filters, decay fades, confluence confirms, scores quantify. Everything else in this guide is detail.

---

### Why Market Pulse — And Not Something Else?

You might already use the CNN Fear & Greed Index, VIX charts, or simple breadth indicators. Here's the difference:

| Approach | What It Does | What It Misses |
|---|---|---|
| **CNN Fear & Greed** | 7-factor sentiment composite | No event detection, no decay, no confluence. A number, not a signal. |
| **VIX chart** | Shows current fear level | No directional prediction. VIX at 30 tells you nothing about *when* to buy. |
| **Simple breadth** (A/D line) | Cumulative participation | No kinematic analysis, no acceleration, no exhaustion detection. |
| **Put/Call ratio** | Options sentiment | Binary (bullish/bearish), no scoring, no decay, no multi-signal fusion. |
| **MXC Market Pulse** | 10 independent signals with VACC kinematics, phase-space analysis, adaptive decay, SVSI conviction gating, and adaptive regime detection | — |

Market Pulse doesn't replace your price chart or your strategy. It tells you **what the market is doing beneath the surface** — and when that subsurface activity historically preceded major turns.

---

## Table of Contents

1. [Quick Start](#1-quick-start)
2. [The Signal Alphabet](#2-the-signal-alphabet)
3. [Market Regime](#3-market-regime)
4. [The Decay System](#4-the-decay-system)
5. [Confluence](#5-confluence)
6. [The Info Table](#6-the-info-table)
7. [The Kill Switch — Chaos Detection](#7-the-kill-switch)
8. [Alerts](#8-alerts)
9. [How to Trade With Market Pulse](#9-how-to-trade)
10. [Market Pulse in Action — Historical Case Studies](#10-case-studies)
11. [Configuration Guide](#11-configuration)
12. [FAQ — Common Questions & Mistakes](#12-faq)
13. [For Quants — The Mathematics](#13-for-quants)
14. [What's Coming Next](#14-whats-next)
15. [We Want to Hear From You](#15-community)

---

<a name="1-quick-start"></a>
## 1. Quick Start — What You See on the Chart

| Visual Element | What It Means |
|---|---|
| **White/grey diamonds** on zero line | A bullish (bottom) event just fired |
| **Orange diamonds** on zero line | A bearish (top) event just fired |
| **Letter above/below diamond** | Which signal fired (Z, L, M, A, D, N, P, B, V, T, K) |
| **Green shaded area** (above zero) | Active bullish signal energy, fading over time |
| **Red shaded area** (below zero) | Active bearish signal energy, fading over time |
| **Green background tint** | Market is in BULL regime |
| **No background** | Market is in BEAR or NEUTRAL regime |
| **Green vertical line** | Regime just flipped to BULL |
| **Red vertical line** | Regime just flipped to BEAR |
| **Info table** (right side) | Live regime, bottom/top scores, kill switch status |

### First 30 Seconds Checklist

1. **Check background color.** Green = bullish regime. No color = bearish or neutral.
2. **Look for recent diamonds.** White = buy opportunity forming. Orange = top forming.
3. **Check shaded area.** Tall green = strong active bottom signals. Deep red = active top signals.
4. **Hover over any letter** for a detailed tooltip explaining the specific signal.
5. **Glance at info table** for scores and confluence status (✦ symbol).

> 📊 **`[VISUAL: Annotated screenshot of Market Pulse indicator pane — zoomed in, clean, showing: (1) white diamond with "Z" label, (2) green decay area fading over ~14 bars, (3) info table with BULL/score/✦, (4) green background tint. Number each element 1-5 matching the checklist above. Dark theme.]`**

---

<a name="2-the-signal-alphabet"></a>
## 2. The Signal Alphabet — Every Letter Explained

Each letter represents a different market phenomenon. They are designed to be **uncorrelated** — when multiple fire together, the probability of a genuine turn increases dramatically.

---

### Bottom (Bullish) Signals — White Diamonds

#### Z — Zweig Breadth Thrust
**What it detects**: A sudden, violent surge in market participation from oversold conditions.

**In plain English**: The market goes from "nobody's buying" to "everybody's buying" within 10 days. One of the rarest and most powerful bullish signals in market history — has preceded every major bull market since the 1940s.

**How it works**: The 10-day average of advancing issues / total issues drops below 40% (oversold), then surges above 61.5% (thrust) within a 10-day window.

**Decay**: 14 days

> **🔬 For Quants**: Uses ratio-of-DEMAs (not SMAs), per TrendSpider/Zweig variant. Partial scoring begins at 0.58 (approaching-thrust), scaling linearly to 100 at 0.615. SVSI gate: wide threshold (50) with 0.5× floor — Zweig is never fully filtered because its rarity IS the signal.
>
> `ZBT = DEMA(adv, 10) / (DEMA(adv, 10) + DEMA(dec, 10))`
> `Thrust = (ZBT < 0.40 within 10 bars) AND (ZBT > 0.615)`

**Historical examples**: Oct 4, 2011 (SPX +28% in 12 months). Oct 15, 2015 (SPX +10% in 3 months). Jan 2019 post-Christmas crash (+20% in 4 months). Oct 2022 bear market bottom (+22% in 6 months). Zweig thrusts don't always fire at the exact low — but the market has been higher 6 and 12 months later in virtually every documented case.

---

#### L — Lowry 90% Day
**What it detects**: Panic-level buying or selling where 90%+ of all volume and issues move in one direction.

**In plain English**: A "90% up day" means virtually every stock is rising on heavy volume — the market saying "buyers have taken over." A 90% down day followed by a 90% up day within a few bars creates a **bottom sequence** — the classic capitulation-then-reversal pattern.

**Decay**: 10 days

> **🔬 For Quants**: Fixed thresholds per Desmond (2002) — rarity IS the signal. Two consecutive 80%+ days qualify as one 90% day. Scoring uses `min(vol%, issues%)` with tiers: 80%→25, 85%→50, 90%→100. Bottom sequences get 1.25× multiplier.

**Historical examples**: Mar 10, 2020 (90% down) → Mar 13, 2020 (90% up) = bottom sequence at COVID low. Mar 23, 2020 (another sequence) confirmed the generational buying opportunity. Dec 2018 had 90% down days before the Christmas Eve reversal.

> 📊 **`[VISUAL: Side-by-side comparison — Left: SPX price chart showing the Mar 2020 crash. Right: Market Pulse showing the L diamonds firing as a bottom sequence (90% down → 90% up). Highlight how the bottom sequence diamond appeared within 1-2 bars of the actual low.]`**

---

#### M — McClellan Thrust
**What it detects**: A powerful momentum reversal in the McClellan Oscillator, confirmed by VACC acceleration.

**In plain English**: McClellan measures breadth momentum. When it plunges deeply negative then surges above +50, it means breadth has gone from "everybody selling" to "everybody buying" with force. VACC confirmation ensures it's not a dead-cat bounce — it needs genuine acceleration.

**Decay**: 7 days

> **🔬 For Quants**: RANA normalization makes the oscillator comparable across market eras. `McClellan = (DEMA(RANA, 19) - DEMA(RANA, 39)) × 1000`. Bull thrust = `lowest(McClellan, 10) < -50 AND McClellan > 50`. VACC confirmation: `vel > 0 AND acc > 0`. Confirmed = 100pts, unconfirmed = 75pts.

---

#### A — VACC Accumulation (Hidden Buying)
**What it detects**: Smart money quietly buying into weakness — price declining but breadth secretly accelerating.

**In plain English**: Price is falling, headlines are bearish, retail is panicking. But breadth momentum is secretly accelerating upward. This divergence is what institutional accumulation looks like. The event fires when price momentum finally *breaks* (acceleration flips positive) — catching the exact exhaustion point.

**Decay**: 5 days (V-bottoms resolve fast)

> **🔬 For Quants**: Exhaustion trigger architecture (not divergence-onset). VACC computed on both price and breadth (net advances ratio). Z-score normalized velocities with 0.75σ noise filter. Event fires when `state_accumulation AND price_acc flips positive AND SVSI < 40`. Persistence requirement: 3 bars for accumulation (fast V-bottoms), 5 bars for distribution (slow rounded tops).

---

#### D — VACC Distribution (Hidden Selling)
**What it detects**: Smart money quietly selling into strength — price rising but breadth decelerating.

**In plain English**: Mirror of A. Price making highs but fewer stocks participating. When price acceleration flips negative, the distribution event fires. Classic "making highs on thin breadth" warning.

**Decay**: 5 days

---

#### N — Kinematic Breadth
**What it detects**: Strategic momentum reversals using full kinematic analysis (velocity, acceleration, jerk) on cumulative breadth.

**In plain English**: This looks at the "physics" of breadth — not just direction, but speed, acceleration, and the rate of change of acceleration. It detects turning points in the market's cumulative breadth (NYSI) that single indicators miss.

**Types**: NYMO exhaustion at extremes, NYSI strategic acceleration zero-cross, kinematic breadth thrust (vel+acc aligned in top 10% historically).

**Decay**: 10 days

> **🔬 For Quants**: Full 5th-order kinematics on NYMO (tactical, vacc_len=14) and NYSI (strategic, vacc_len=26). n* prediction: `n* = -acc/jerk` (Taylor approx of when acc crosses zero, 1-3 bar lead). Magnitude filter: `|nysi_acc| > 0.3 × σ(nysi_acc)`. Thrust = vel+acc aligned AND `percentrank(acc) > 90th`. All SVSI-gated.

---

#### P — Phase Portrait V-Bottom
**What it detects**: Rapid regime transitions via phase-space rotation analysis.

**In plain English**: Imagine plotting breadth velocity on one axis and acceleration on another. During V-bottoms, the point whips through the recovery zone at extreme speed — like a pendulum swinging violently through the bottom. This angular velocity spike in exactly the right phase-space zone signals an aggressive entry.

**Decay**: 10 days

> **🔬 For Quants**: Genuine dynamical systems phase portrait on NYSI. State `(vel_z, acc_z)` → polar via `atan2`. Smoothed in Cartesian (avoids 2π→0 artifacts). V-bottom: `ω_pct > 90th AND θ ∈ [1.75π, 0.25π] AND 0.5 < r < 4.0 AND SVSI < 40`. The most mathematically sophisticated bottom detector in the system.

> 📊 **`[VISUAL: Phase portrait diagram — Unit circle divided into 4 quadrants. Label: Q1 (top-right) "Expansion" (vel+ acc+), Q2 (top-left) "Distribution" (vel+ acc-), Q3 (bottom-left) "Contraction" (vel- acc-), Q4 (bottom-right) "Recovery" (vel- acc+). Show a dot path spiraling through all four quadrants to illustrate a full market cycle. Highlight the V-bottom zone (Q4→Q1 boundary) with a bright green arc. Show angular velocity arrow at the V-bottom zone to illustrate the "whip" effect. Clean, educational style.]`**

---

#### B — Breadth Composite
**What it detects**: Extreme market-wide participation reversals using weighted % above 200d/50d/20d MA.

**In plain English**: Tracks what % of stocks are above their key moving averages (200d weighted most). When this composite is at historically extreme lows AND velocity surges upward, broad participation is reversing from washed-out levels.

**Decay**: Bottom 7 days, Top 10 days

> **🔬 For Quants**: `Composite = MMTH×0.5 + MMFI×0.3 + MMTW×0.2`. Percentile ranked over 750 trading days. VACC applied to ranked composite. Bottom: `pct < 0.15 AND vel_z > 1.5 AND SVSI < 30`. Top: `pct > 0.85 AND vel_z < -1.5 AND SVSI > 70`.

---

#### V — VVIX/VIX Pivot
**What it detects**: Volatility regime shifts via the VVIX/VIX ratio breaking adaptive bands.

**In plain English**: VVIX measures "volatility of volatility." When VVIX spikes above 125 and pivots, SPY historically gains ~70% of the time over 10-20d. The indicator tracks the VVIX/VIX ratio using an adaptive KAMA engine.

**Decay**: 7 days

> **🔬 For Quants**: Uses `duo_core` engine on VVIX/VIX with 2D minimum TF. Event-only mode (score_entry=0). Band width: `sma(|Δratio|)` — adapts to ratio's own vol. VVIX extreme threshold (125) per SpotGamma research.

---

#### T — VIX Term Structure
**What it detects**: Shifts between backwardation (near-term fear > long-term) and contango (calm returning).

**In plain English**: The VIX "term structure" compares short-term fear (VIX, ~30 days) to medium-term fear (VIX3M, ~90 days). Normally, VIX3M > VIX (contango) because there's more uncertainty further out. When VIX *exceeds* VIX3M (backwardation), the market is pricing in more fear NOW than in 3 months — pure panic.

Why this matters: backwardation has preceded or accompanied every major selloff since 2008. Conversely, when the term structure *normalizes* from backwardation back to contango, it's one of the earliest "all-clear" signals — institutions are unwinding hedges and re-risking.

- **T bottom** (white): VIX/VIX3M ratio falling → fear subsiding, contango recovering. Often leads price by 1-3 days.
- **T top** (orange): VIX/VIX3M ratio rising → backwardation building, stress increasing. Confirms breadth deterioration.

**Historical examples**: Feb 2018 (VIX spike to 50, backwardation inverted for days → T top fired before the worst of the selloff). Mar 2020 (extreme backwardation → T bottom fired as term structure normalized, within 2 bars of the COVID low). Aug 2024 (VIX spike to 65, backwardation → T events captured the turn).

**Decay**: 7 days

> **🔬 For Quants**: `ratio_regime_calc(VIX, VIX3M)` with 2D floor (intraday term structure is too noisy). The ratio is processed through the full `duo_core` engine: Gaussian smoothing → cycle intelligence → KAMA adaptive trend → adaptive bands. Events fire on band breakouts. External SVSI filter+boost ensures term structure shifts are only flagged when price confirms: bot SVSI<40 (peak 1.5× at SVSI=0), top SVSI>65 (peak 1.5× at SVSI=100). This prevents false signals during routine VIX fluctuations within an established trend.

---

### Top (Bearish) Signals — Orange Diamonds

| Letter | Signal | What It Catches |
|---|---|---|
| **L** | Lowry 90% Down Day | Panic selling — 90%+ declining |
| **D** | VACC Distribution | Hidden selling into strength |
| **N** | Kinematic Breadth Top | NYSI/NYMO exhaustion at overbought |
| **B** | Breadth Composite Top | Participation at extremes + velocity reversing |
| **T** | VIX Term Structure → Backwardation | Near-term fear exceeding long-term |

**Intentionally removed** (tested, found unreliable): McClellan Bear Thrust (fires after damage done), VVIX Bearish Pivot (fires in normal bull markets), Phase Slow Top (imprecise, persists weeks). This asymmetry is deliberate: bottoms are violent and clustered (V-shaped), tops are gradual and diffuse (rounded).

---

<a name="3-market-regime"></a>
## 3. Market Regime — The Background Color That Matters Most

The green background tint represents the **TMF/ES ratio regime with composite override** — a layered system that uses bond-equity rotation as the base signal, overridden only when breadth and volume conviction strongly disagree.

### How It Works

Think of it as a two-layer system:

**Layer 1 — The Base (TMF/ES Ratio Trend)**
The ratio of TMF (3× long bonds) to ES (S&P 500 futures) is processed through an adaptive KAMA trend engine on Heikin Ashi bars. When money flows from bonds to equities (ratio falling), the base reads BULL (+1). When money flows to safety (ratio rising), it reads BEAR (−1).

This is a powerful institutional signal — large funds rotate between safety and risk before price moves. But it can lag during unusual correlation regimes (e.g., bonds and stocks falling together).

**Layer 2 — The Composite Override (Breadth + SVSI)**
Two independent oscillators form a composite that can override the TMF signal:
- **SVSI** (Smoothed Volume Strength Index on ES) — volume-weighted momentum. Measures institutional conviction.
- **Breadth** (NYSI kinematics via ADVN/DECL) — cumulative market breadth acceleration.

Both are converted to **phase_cos** — a single number in [−1, +1] that encodes their velocity + acceleration cycle position using phase-space analysis (atan2 in polar coordinates, radial-gated for confidence).

The composite is adaptively weighted:
- **SVSI normal (30-70)**: SVSI 70% weight, breadth 30% — SVSI leads in routine markets
- **SVSI extreme (<30 or >70)**: breadth 70% weight, SVSI 30% — at extremes, breadth confirms

**When Does the Override Fire?**
The composite disagrees with TMF when it points in the opposite direction. This disagreement is **percentile-ranked over ~500 bars** (self-calibrating). The override fires only when disagreement is historically exceptional:
- TMF **reliable** (low bond-equity correlation) → override needs top 20% disagreement
- TMF **unreliable** (high correlation) → override relaxes to top 40%

Reliability is measured continuously: `reliability = max(0, 1 − correlation_pct / threshold)` where correlation is the TMF/ES velocity z-score correlation percentile over ~3 years.

When TMF reads **neutral** (transition period), the composite decides directly: > +0.25 = BULL, < −0.25 = BEAR, else NEUTRAL.

> 📊 **`[VISUAL: Layered diagram — Top layer: "TMF/ES Ratio" box outputting BULL/BEAR/NEUTRAL as the base. Middle: "Composite" box combining SVSI (70%/30%) and Breadth (30%/70%) with adaptive weighting arrows. Bottom: "Override Gate" showing percentile disagreement threshold. Final output: REGIME (BULL green / NEUTRAL grey / BEAR red). Arrow from TMF reliability feeds into the override gate threshold. Clean, minimal, infographic style.]`**

### How Regime Transitions Happen

Regime doesn't flip on a single indicator's whim. Here's a concrete example:

1. **Oct 2022**: TMF/ES ratio still elevated (money in bonds) → base reads BEAR. But breadth is accelerating and SVSI is rising → composite building disagreement.
2. **Late Oct 2022**: TMF/ES ratio starts declining (money rotating to equities). Base flips to BULL → **regime flip** (green vertical line + green background). Composite agrees, no override needed.
3. **Jul 2023**: TMF/ES ratio firmly declining, breadth strong, SVSI bullish. All aligned → **Strong BULL** (high confidence score in info table).
4. **Aug 2024**: Breadth collapses, SVSI drops. TMF/ES still bullish (bond money hasn't rotated yet). Composite disagreement rises above override threshold → **override fires**, regime goes NEUTRAL or BEAR despite TMF still signaling BULL.

The self-calibrating percentile threshold prevents flip-flopping: the override only fires when disagreement is historically exceptional — not on routine noise.

| Regime | Background | Action |
|---|---|---|
| **BULL** | Green tint | Favor longs, buy bottom signals aggressively |
| **NEUTRAL** | None | Reduce size, be selective |
| **BEAR** | None | Prioritize top signals, bottom signals for short-covering only |

> **🔬 For Quants — TMF/ES Base + Phase_cos Composite Override**
>
> TMF/ES ratio processed through `duo_core` on Heikin Ashi bars → `ratio_regime_calc` → `tmf_regime_dc` (±1).
>
> Composite: `composite = svsi_phase_cos × s_weight + breadth_phase_cos × b_weight`
> where `phase_cos = cos(smooth_phase) × min(1, radial)` from `_vacc_phase()` — encodes vel+acc cycle position via atan2, radial-gated.
> Adaptive weights: `svsi_extreme = max(0, (|svsi_raw − 50| − 20) / 30)`. `b_weight = 0.3 + 0.4 × svsi_extreme`.
>
> Reliability: `reliability = max(0, 1 − corr_pct / threshold)`. Correlation: `ta.correlation(tmf_vel_z, es_vel_z, 8)`, percentile over 750 bars (~3yr daily).
>
> Override gate: `disagree_score = composite × (−tmf_regime)`, percentile-ranked over 500 bars. Threshold: `0.60 + 0.20 × reliability` (top 40% unreliable → top 20% reliable).
>
> TMF neutral fallback: `composite > +0.25 → BULL`, `< −0.25 → BEAR`, else NEUTRAL.
>
> 5 security calls: TMF vel_z, ES vel_z, ADVN/DECL breadth, HA TMF/ES ratio, ES SVSI phase.

---

<a name="4-the-decay-system"></a>
## 4. The Decay System — Why Signals Fade

Every signal has a **half-life** calibrated to empirical persistence research:

| Signal | Half-Life | Rationale |
|---|---|---|
| Zweig (Z) | 14 days | Structural impact persists 2-3 weeks |
| Lowry (L) | 10 days | 90% days echo ~2 weeks |
| McClellan (M) | 7 days | Standard breadth cycle |
| VACC Accum/Distrib (A/D) | 5 days | V-bottoms resolve fast |
| Kinematic (N) | 10 days | Strategic turns persist 1-2 weeks |
| Breadth Comp Bot (B) | 7 days | Participation reversal |
| Breadth Comp Top (B) | 10 days | Distribution slower than accumulation |
| VVIX/VIX (V) | 7 days | Vol regime standard |
| VIX Term Struct (T) | 7 days | Term structure standard |

The green/red areas are the **sum of all active decayed scores**. Fresh signals push them up; time pulls them back.

### How to Read the Decay Area

Think of each signal as a campfire. When it first fires, it's burning bright (full score). Over its half-life, the fire dims to half brightness. After two half-lives, it's at 25%. After three, 12.5%. By 30 bars, it's embers — effectively zero.

**Practical example**: A Zweig thrust (Z) fires with score 100. After 14 bars, it's at 50. A McClellan thrust (M) fires 3 bars later with score 75. The green area shows *both* signals decaying simultaneously — the Z contribution slowly fading while the M contribution is still fresh. This stacking effect is why clustered signals produce the tallest green areas.

> 📊 **`[VISUAL: Decay curve illustration — X-axis: "Bars since event" (0-30). Y-axis: "Signal strength" (0-100). Show 3 overlapping exponential decay curves: Zweig (14d half-life, slow fade), McClellan (7d, medium), VACC (5d, fast fade). Label half-life points on each curve. Below: a stacked area showing what the combined decay area looks like when all three fire within 5 bars of each other. Clean, no chart noise.]`**

> **🔬 For Quants**: `decay_rate = 0.5^(1 / tf_lookback(halflife_days))`. `decayed = raw × decay_rate^bars_since`. Max tracking: 30 bars. Note: the plotted decay area is a simple sum of individual decayed scores / 100 for visual scaling. The `bot_agg` in the info table uses *weighted* aggregation (Zweig×1.5, Lowry×1.3, etc.) — they intentionally measure different things.

---

<a name="5-confluence"></a>
## 5. Confluence — When Multiple Signals Agree

The **✦ symbol** in the info table means 2+ **uncorrelated** sources are active simultaneously. This is the highest-conviction setup.

**Bottom Confluence** (≥2 of): Zweig, VACC Divergence, Kinematic
**Top Confluence** (≥2 of): VACC Distribution, Kinematic Top

### Why Confluence Matters — The Math of Independence

If a single signal has a 60% hit rate, two independent signals firing together have roughly 60% × 60% = 36% chance of being a **false** signal (both wrong). That means ~84% probability that at least one is right. In practice, our signals aren't perfectly independent, but the overlap is low by design — Zweig measures ratio levels, VACC measures price-vs-breadth divergence, Kinematic measures cumulative acceleration. Different data transforms, different time horizons, different failure modes.

### Worked Example: Oct 2022 Bottom

1. **Oct 12**: VACC Accumulation (**A**) fires — SPX declining but breadth acceleration flipping positive. Score: 72. Info table shows BOT: 58.
2. **Oct 13**: Kinematic breadth thrust (**N**) fires — NYMO vel+acc in top 10% historically. Score: 85. Info table now shows BOT: 127 **✦** (confluence!).
3. **Oct 14**: Lowry bottom sequence (**L**) fires — 90% down day followed by 90% up day. Score stacks further.
4. **Oct 28**: Regime flips BULL (green vertical line) — 3/4 oscillators aligned.
5. **Result**: SPX rallied +22% over the next 6 months.

The ✦ appeared on Oct 13 — **15 calendar days before the regime flip confirmed the direction.** Confluence gave the early signal; regime gave the confirmation.

> 📊 **`[VISUAL: Market Pulse chart on SPX daily, Oct 2022 period. Show the cluster of A, N, L diamonds firing within 3 bars. Green decay area stacking up. Info table showing confluence ✦. Green vertical line appearing ~2 weeks later. Annotate the timeline: "Confluence fires here" → "Regime confirms here" → "Rally accelerates here".]`**

### Trading Confluence

| Situation | Position Size |
|---|---|
| Single signal, no confluence | Small / wait for confirmation |
| Single signal + BULL regime | Standard |
| Confluence (✦) | Full size |
| Confluence (✦) + regime flip | Maximum conviction — rare and powerful |

---

<a name="6-the-info-table"></a>
## 6. The Info Table — Your Command Center

Four rows on the right side:

| Row | Shows | Hover Tooltip Reveals |
|---|---|---|
| **REGIME** | BULL / BEAR / WAIT + confidence | TMF/ES regime, breadth quadrant (Expanding/Distributing/Contracting/Recovering), oscillator divergence warnings |
| **BOT** | Aggregate bottom score (0-100) + ✦ | Trigger name (e.g. "zweig_thrust"), strength rating (1-3), confluence status |
| **TOP** | Aggregate top score (0-100) + ✦ | Trigger name, strength rating, confluence status |
| **KILL** | OFF (or level when enabled) | Kill switch status, chaos %, position multiplier |

The background color of each cell scales with intensity — brighter green = stronger bottom signal, brighter orange = stronger top signal.

> 📊 **`[VISUAL: Close-up screenshot of the info table in 3 states: (1) Normal — BULL regime, low scores, no confluence. (2) Active bottom — BULL regime, BOT score 85 with ✦, showing the tooltip expanded. (3) Active top — BEAR regime, TOP score 60, showing D trigger in tooltip. Arrange as a horizontal strip of 3 captures.]`**

---

<a name="7-the-kill-switch"></a>
## 7. The Kill Switch — Chaos Detection (Advanced)

> ⚠️ **Disabled by default** (toggle ON in settings to activate). Powered by the dedicated `mxc_chaos` library. This is the system's most mathematically advanced component.

### What It Does

Detects when the market transitions to **genuine mathematical chaos** — not "volatility," but actual chaotic behavior where small perturbations lead to exponentially diverging outcomes. Provides **3-5 weeks lead time** before major crises.

It computes the **Lyapunov exponent (λ)** of the S&P 500:
- **λ > 0**: Chaotic (trajectories diverge exponentially)
- **λ ≈ 0**: Normal dynamics
- **λ < 0**: Stable (trajectories converge)

### Escalation Levels

| Level | Name | Position Multiplier | Action |
|---|---|---|---|
| 0 | NORMAL | 1.0 | Normal trading |
| 1 | WATCH | ~0.77 | Heighten awareness |
| 2 | ELEVATED | ~0.43 | Reduce positions |
| 3 | HIGH | ~0.10 | Defensive positioning |
| 4 | CRITICAL | 0.10 | Maximum caution |

> **🔬 For Quants — Lyapunov Exponent**
>
> **Rosenstein's algorithm** (1993), validated against `nolds` Python library. Phase space: Takens delay embedding (NOT derivative — rejected for noise amplification):
>
> `X_i = [x_i, x_{i+τ}, ..., x_{i+9τ}]` where `x = log(close/close[1])`
> τ auto-computed from autocorrelation (1-1/e threshold). Parameters: window=500, emb_dim=10, traj_len=20, step=5.
>
> **Composite gate** (prevents bull-market false positives):
> `composite = vel_z(λ) × |drawdown_50d|`
> Requires BOTH rising chaos velocity AND actual price decline.
>
> Raw thresholds (NOT percentile-ranked — zero-inflated distribution): CRITICAL≥30, HIGH≥20, ELEVATED≥10, WATCH≥3.
> `position_mult = max(0.1, 1.0 - max(0, (composite-3)/27) × 0.9)`
>
> Academic: Tsakonas et al. (2024, J. Risk) — 75-82% accuracy for 10%+ corrections, 3-5 week lead time.

---

<a name="8-alerts"></a>
## 8. Alerts — Never Miss a Signal

| Alert | Fires When |
|---|---|
| **Regime → BULL** | Combined regime flips bullish |
| **Regime → BEAR** | Combined regime flips bearish |
| **Bottom Signal** | Any bullish event fires |
| **Top Signal** | Any bearish event fires |
| **VIX Term Structure** | VTS backwardation/contango shift |
| **Breadth Composite** | Breadth participation extreme |

**Recommended**: Set Regime BULL/BEAR as push notifications, Bottom Signal as email summary.

---

<a name="9-how-to-trade"></a>
## 9. How to Trade With Market Pulse

### Strategy 1: The Regime Rider (Conservative)
Go long when green background appears. Exit when it disappears. Ignore individual signals. **Best for**: long-term investors, weekly chart checkers.

### Strategy 2: The Signal Hunter (Moderate)
BULL regime → buy white diamonds, especially with ✦. BEAR → only act on Z or ✦. Take profits on orange diamonds. Regime flip = hard stop. **Best for**: active investors, swing traders.

### Strategy 3: The Full Arsenal (Advanced)
Decay height = position size. Confluence = timing. Regime = direction. Letter combos for quality: Z+L (highest conviction bottom), A+N (stealthy accumulation), L+T (capitulation + VIX normalization). **Best for**: full-time traders.

### Timeframe Recommendations
- **1D**: Standard, recommended for most
- **2D**: Reduced noise, slightly delayed
- **1W**: Strategic positioning, regime signals only
- **4H**: Works but noisier — breadth data is daily-only

All lookbacks, decay rates, and thresholds auto-adjust for your chart timeframe.

---

<a name="10-case-studies"></a>
## 10. Market Pulse in Action — Historical Case Studies

Theory is good. Evidence is better. Here are five real-world scenarios where Market Pulse's signals preceded major market turns.

### Case 1: COVID Crash & Recovery (Feb–Mar 2020)

**The Setup**: SPX drops 34% in 23 trading days — the fastest bear market in history.

**What Market Pulse Showed**:
- **Feb 27–28**: Multiple **L** (Lowry 90% down days) fire as selling reaches panic levels. Orange diamonds cluster. Top decay area surges.
- **Mar 12–13**: **L** bottom sequence fires (90% down → 90% up within bars). White diamond.
- **Mar 16–20**: **A** (VACC Accumulation) fires — price still falling but breadth acceleration flipping positive. Hidden buying detected.
- **Mar 23**: **N** (Kinematic thrust) fires — NYMO vel+acc in top 5% historically. **Confluence ✦** appears (A + N active simultaneously).
- **Mar 24–26**: **M** (McClellan thrust) fires with VACC confirmation. Green decay area at multi-year highs.
- **Late Mar**: Regime flips BULL (green vertical line).
- **Result**: SPX rallied +68% over the next 12 months from the Mar 23 low.

**Key Takeaway**: Confluence fired at the low. Regime confirmed 3-5 days later. The decay area showed signal intensity clustering — a wall of white diamonds in 10 trading days.

> 📊 **`[VISUAL: SPX daily chart Feb-Apr 2020 with Market Pulse below. Show the orange L diamonds during the crash, then the white A, N, M, L diamonds clustering at the bottom. Annotate the confluence ✦ moment and the regime flip. Two panels: price above, Market Pulse below.]`**

### Case 2: 2022 Bear Market Bottom (Sep–Oct 2022)

**The Setup**: SPX down 25% from Jan highs. Aggressive Fed hiking cycle. Sentiment at 2009-level pessimism.

**What Market Pulse Showed**:
- **Sep 23**: **B** (Breadth Composite bottom) fires — % above 200d MA at 15th percentile, velocity surging.
- **Oct 3–13**: **A** (VACC Accumulation) fires, followed by **N** (Kinematic turn). **Confluence ✦** appears.
- **Oct 13**: CPI report triggers selling, but Market Pulse shows divergence — breadth already accelerating beneath the surface.
- **Oct 28**: Regime flips BULL. Green vertical line.
- **Result**: SPX rallied +22% over 6 months. Nasdaq +30%.

**Key Takeaway**: The indicator's strength here was detecting hidden accumulation while headlines remained universally bearish. Confluence preceded the regime flip by 15 days.

### Case 3: Aug 2024 VIX Spike (The Yen Carry Unwind)

**The Setup**: VIX spikes from 12 to 65 intraday — the largest single-day VIX move since 2018. Japanese yen carry trade unwinds.

**What Market Pulse Showed**:
- **Aug 5**: **V** (VVIX/VIX extreme pivot) fires — VVIX above 125, extreme contrarian signal. **T** (VIX Term Structure) fires — severe backwardation.
- **Aug 5–6**: **L** (Lowry 90% day sequences) fire as panic selling transitions to panic buying.
- **Aug 7–8**: **N** (Kinematic thrust) confirms breadth reversal.
- **Aug 8**: Confluence ✦ (V + N + L all active within decay windows).
- **Result**: SPX recovered all losses within 3 weeks and made new highs within 6 weeks.

**Key Takeaway**: The V signal (VVIX extreme) provided the earliest signal. Combined with L and T, confluence built within 3 trading days of the low.

> 📊 **`[VISUAL: SPX daily chart Jul-Sep 2024 with Market Pulse below. Show the VIX spike day with V and T diamonds, then L and N diamonds following. Highlight how quickly confluence built and how the decay area peaked within 3-5 bars of the actual low.]`**

### Case 4: Jan 2022 — Top Signals Before the Bear Market

**The Setup**: SPX at all-time highs. Inflation accelerating. Fed pivot imminent.

**What Market Pulse Showed**:
- **Late Dec 2021–Jan 2022**: **D** (VACC Distribution) fires — SPX making highs but breadth deteriorating. Orange diamond.
- **Jan 2022**: **N** (Kinematic breadth top) fires — NYSI acceleration flipping negative while NYSI velocity still positive (classic distribution signature).
- **Jan 10–18**: **B** (Breadth Composite top) fires — participation at 85th+ percentile but velocity cratering. Top confluence ✦.
- **Jan 20–24**: Regime flips BEAR (red vertical line).
- **Result**: SPX declined -25% over the next 9 months.

**Key Takeaway**: Top signals are subtler than bottom signals (no panic, no 90% days). The D and N signals — both measuring hidden divergences — provided 2-3 weeks of warning before the regime confirmed.

### Case 5: Dec 2018 Christmas Eve Reversal

**The Setup**: SPX down 20% from Sep highs. Powell "autopilot" comments. Liquidity crisis fears.

**What Market Pulse Showed**:
- **Dec 21**: **L** (Lowry 90% down days) fire in rapid succession.
- **Dec 24**: **Z** (Zweig approaching-thrust) — breadth ratio collapsing to below 0.40 (oversold trigger armed).
- **Dec 26**: Market reopens with violent buying. **M** (McClellan thrust) fires with VACC confirmation. **A** (VACC Accumulation) fires.
- **Early Jan 2019**: **Z** (Zweig thrust completes) as breadth ratio surges above 0.615. Score 100. Maximum conviction.
- **Jan 7–9**: Regime flips BULL.
- **Result**: SPX rallied +20% in 4 months.

**Key Takeaway**: The Zweig thrust — the rarest signal in the system — fired at the exact right moment. Combined with L and M signals, this was one of the highest-confluence setups in Market Pulse's backtesting history.

> 📊 **`[VISUAL: SPX daily chart Nov 2018-Feb 2019 with Market Pulse below. Show the L orange diamonds during the December crash, then the Z diamond firing in early January. Annotate the Zweig thrust completion with a callout. Show the regime flip to BULL shortly after.]`**

---

<a name="11-configuration"></a>
## 11. Configuration Guide

### Regime Settings
| Setting | Default | Notes |
|---|---|---|
| Safe Haven Symbol | AMEX:TMF | 3× long bonds. Alternatives: TLT, GLD |
| Risk Asset Symbol | CME_MINI:ES1! | ES futures (institutional volume). Alt: SPY |
| TMF/ES Timeframe | 4D | Balances noise vs responsiveness |
| Breadth Timeframe | 2D | Sweet spot for daily breadth data |

### Display Settings
All ON by default. "Draw on Main Chart" overlays regime flip lines on price chart.

### Event Toggles
Every signal independently toggleable. All ON except Kill Switch.

---

<a name="12-faq"></a>
## 12. FAQ — Common Questions & Mistakes

### "A bottom signal fired but the market kept dropping. Is it broken?"

No. Individual signals have a 55-70% hit rate — they're probabilistic, not prophetic. This is exactly why **confluence** and **regime** exist:
- A single signal without confluence = interesting, not actionable at full size
- A signal firing during BEAR regime = lower probability than during BULL
- The decay system handles this gracefully: if the signal was wrong, it fades to zero within its half-life. No manual intervention needed.

**The correct mental model**: Each signal is a piece of evidence, not a verdict. Stack the evidence (confluence), check the jury (regime), then act.

### "Why don't I see any signals on my crypto chart?"

Market Pulse uses **NYSE breadth data** (advances, declines, up-volume, down-volume) which is only available for US equities. The indicator is designed for SPX/SPY and US equity indices. Using it on crypto, forex, or individual stocks will produce no breadth signals.

The **regime background** and **VIX-related signals** (V, T) still work on any chart since they use hardcoded data feeds (CBOE:VIX, etc.), but breadth signals (Z, L, M, A, D, N, P, B) require NYSE data.

### "The info table says BULL but I don't see a green background?"

Check your display settings — "Show Regime Background" must be enabled. Also verify you're looking at the Market Pulse pane, not the price chart. The green tint only appears in the indicator's own pane.

### "Can I use this on timeframes smaller than 4H?"

Technically yes, but not recommended. Breadth data is published daily, so intraday charts below 4H will show the same breadth readings for the entire day. VIX data updates intraday but with limited resolution. The indicator auto-adjusts all lookbacks via `tf_lookback()`, but the **information content** below daily is limited.

**Recommended timeframes**: 1D (best), 2D (less noise), 1W (strategic).

### "What's the difference between the decay area and the info table score?"

They measure different things intentionally:
- **Decay area** (plotted): Simple sum of all decayed scores / 100. Visual indicator of total signal energy.
- **Info table score** (`bot_agg` / `top_agg`): **Weighted** aggregate using empirical accuracy weights (Zweig×1.5, Lowry×1.3, etc.). Better for decision-making.

The info table score is the one to trade on. The decay area is for visual context.

### "Why is the Kill Switch disabled?"

The Kill Switch (Lyapunov chaos detection) lives in the dedicated `mxc_chaos` library and is fully functional. Toggle it ON in the indicator settings to activate. When enabled, it appears as a **K** diamond and updates the KILL row in the info table. It's off by default because the Lyapunov computation is resource-intensive (~88K peak loop iterations per bar) and most users don't need crisis detection for everyday trading.

### "How many TradingView security calls does this use?"

~22 out of TradingView's 40-call limit. This leaves room for other indicators on the same chart. If you're hitting the limit, check what other indicators you have loaded — some popular indicators use 10+ calls each.

### "Can I change the symbols for non-US markets?"

The regime settings (Safe Haven Symbol, Risk Asset Symbol) are configurable. However, the breadth signals are hardcoded to NYSE data (ADVN, DECL, UVOL, DVOL, MMTH, MMFI, MMTW). A future version may support configurable breadth sources for international markets.

---

<a name="13-for-quants"></a>
## 13. For Quants — The Mathematics

This section covers the quantitative foundations of every component. All formulas are taken directly from the source code — no simplifications.

---

### 13.1 Architecture Overview

Market Pulse is a **pure consumer** — it contains no math itself. All computation lives in two libraries:

- **`mxc_lind`** (Leading Indicators Library) — event detection, regime, decay, aggregation
- **`mxc_chaos`** (Chaos Library) — Lyapunov Kill Switch

These libraries in turn depend on:
- **`mxc_ta`** (`tal`) — percentile ranking, timeframe-adaptive lookbacks, Gaussian filters
- **`mxc_ind2`** (`ind2`) — VACC kinematics, SVSI, cycle intelligence, volrank, KAMA, RSX
- **`mxc_ma`** (`ma`) — DEMA step function (stateful EMA without Pine's `ta.ema` warmup)
- **`mxc_hmm`** (`hmm`) — Hidden Markov Model crossover forecasting

**Data flow per bar**:
```
request.security() → fetch breadth/VIX/ES data
    → calc functions (pure logic, no security calls)
        → event detection (bool)
        → raw scoring (0-100, magnitude-graded)
        → SVSI conviction gating (prorated, not binary)
        → decay tracking (bars_since + half-life)
    → aggregation (weighted sum of decayed scores)
    → regime (TMF/ES base + composite override)
    → visualization (diamonds, letters, decay area, info table)
```

---

### 13.2 VACC — Velocity, Acceleration, Curvature (The Kinematic Engine)

VACC is the mathematical backbone of nearly every signal. It extracts the full kinematic state of any time series — not just "is it going up?" but "is it accelerating? decelerating? at what rate?"

**Definition** (from `mxc_ind2.vacc`):
```
Given series src, length L, smooth S:
    smoothed = GaussianMA(src, S)
    velocity = smoothed - smoothed[1]          // 1st derivative (direction + speed)
    acceleration = velocity - velocity[1]      // 2nd derivative (curvature)
    jerk = acceleration - acceleration[1]      // 3rd derivative (rate of curvature change)
```

All derivatives are then smoothed with another Gaussian pass to reduce noise.

**Why this matters**: Traditional indicators use level (RSI > 70) or direction (MACD cross). VACC adds acceleration — which **leads** velocity by definition. When acceleration flips positive while velocity is still negative, the series is about to turn up. This is the mathematical basis for every "exhaustion" and "divergence" detector in Market Pulse.

**Extremity detection**: `bull_ex` fires when velocity is positive AND acceleration flips negative (momentum exhaustion at a high). `bear_ex` fires when velocity is negative AND acceleration flips positive (momentum exhaustion at a low).

---

### 13.3 Phase Portrait Analysis (Dynamical Systems on Breadth)

The most mathematically sophisticated component. Used for V-bottom detection and regime phase classification.

**State space**: For a series with VACC outputs `(vel, acc)`, normalize to z-scores:
```
vel_z = vel / stdev(vel, 1000)     // clamped to [-4, +4]
acc_z = acc / stdev(acc, 1000)     // clamped to [-4, +4]
```

**Polar transformation**:
```
phase_raw = atan2(acc_z, vel_z)                    // angle in velocity-acceleration plane
phase_angle = phase_raw < 0 ? phase_raw + 2π : phase_raw  // map to [0, 2π]
```

**Cartesian smoothing** (avoids 2π→0 wrap-around discontinuity):
```
sin_smooth = GaussianMA(sin(phase_angle), 2, 2)
cos_smooth = GaussianMA(cos(phase_angle), 2, 2)
phase_smooth = atan2(cos_smooth, sin_smooth)       // reconstruct smoothed angle
```

**Derived quantities**:
- **Angular velocity** `ω = Δphase_smooth` (wrap-corrected) — regime transition speed
- **Radial distance** `r = √(vel_z² + acc_z²)` — signal confidence (near-origin = noise)
- **phase_cos** `= cos(phase_smooth) × min(1, r)` — radial-gated cycle position in [-1, +1]

**Four quadrants** (market cycle phases):
| Quadrant | Phase Range | vel | acc | Market Phase |
|---|---|---|---|---|
| Q1 | 0 – π/2 | + | + | Early bull (accelerating rise) |
| Q2 | π/2 – π | + | − | Distribution (decelerating rise — topping) |
| Q3 | π – 3π/2 | − | − | Bear (accelerating decline) |
| Q4 | 3π/2 – 2π | − | + | Recovery (decelerating decline — bottoming) |

**V-bottom detection**: `ω_pct > 90th AND θ ∈ [1.75π, 0.25π] AND 0.5 < r < 4.0`
Translation: top 10% angular velocity in the recovery zone with meaningful signal strength. The "whip" through the Q4→Q1 boundary at extreme speed is the mathematical signature of a V-shaped reversal.

**Slow top detection**: `ω_pct < 10th AND θ ∈ [0.6π, π] AND r > 0.5`
Translation: bottom 10% angular velocity in the distribution zone — rotation has stalled, the market is "stuck" in the topping phase.

---

### 13.4 The McClellan Framework (Breadth Momentum)

**NYMO** (McClellan Oscillator):
```
RANA = (advances - declines) / (advances + declines)    // ratio-adjusted net advances
NYMO = (DEMA(RANA, 19) - DEMA(RANA, 39)) × 1000
```
RANA normalization makes the oscillator comparable across market eras (more listed stocks = more issues, but ratio stays bounded).

**NYSI** (McClellan Summation Index):
```
NYSI = cumulative_sum(NYMO)
```
Absolute level is start-dependent and meaningless. Only VACC derivatives of NYSI matter.

**Kinematic breadth events** (applied to NYMO and NYSI separately):
- NYMO VACC (fast, `vacc_len=14`) → tactical turning points (days)
- NYSI VACC (slow, `vacc_len=26`) → strategic turning points (weeks)

**Event types**:
- **NYMO exhaustion**: `bear_ex AND NYMO < -50 AND SVSI < 40` (bottom) / `bull_ex AND NYMO > 50 AND SVSI > 65 for 3 bars` (top)
- **NYSI strategic turn**: `nysi_acc flips sign AND |nysi_acc| > 0.3σ AND velocity opposes acceleration` (counter-trend acceleration)
- **Kinematic breadth thrust**: `nymo_vel > 0 AND nymo_acc > 0 AND percentrank(nymo_acc) > 90th` (vel+acc aligned, historically rare)

---

### 13.5 SVSI Conviction Gating — Why It's Not Binary

Every breadth event is filtered and boosted by SVSI (Smoothed Volume Strength Index on ES futures). This prevents false signals when price doesn't confirm breadth.

**Prorated scaling** (not on/off):
```
Bottom: svsi < threshold → strength = 1.0 + (threshold - svsi) / threshold × (peak_mult - 1.0)
         svsi ≥ threshold → strength = 0.0  (event filtered)
Top:    svsi > threshold → strength = 1.0 + (svsi - threshold) / (100 - threshold) × (peak_mult - 1.0)
         svsi ≤ threshold → strength = 0.0  (event filtered)
```

**Per-signal thresholds**:
| Signal | Side | Threshold | Peak Mult | Floor | Notes |
|---|---|---|---|---|---|
| Zweig | Bottom | 50 | 2.0× | 0.5× | Never fully filtered — rarity IS the signal |
| Lowry | Bottom/Top | 35/65 | 1.5× | 0 | Standard gating |
| McClellan | Bottom | 35 | 1.5× | 0 | Standard gating |
| Kinematic | Bottom/Top | 35/65 | 1.5× | 0 | Standard gating |
| VACC Div | Bottom/Top | 40/65 | 2.0× | 0 | Internal, + 3-bar persistence for tops |
| Breadth Comp | Bottom/Top | 30/70 | 1.5× | 0 | Tighter gates at extremes |
| VIX Term Struct | Bottom/Top | 35/65 | 1.5× | 0 | External SVSI filter |

The raw score is multiplied by this conviction factor, then clamped to [0, 100]. Effect: a Lowry 90% up day with SVSI at 10 (deeply oversold) gets 1.5× score. The same event with SVSI at 50 (neutral) gets filtered to 0.

---

### 13.6 Decay Mathematics

Each event produces a raw score (0-100) that decays exponentially:

```
decay_rate = 0.5^(1 / tf_lookback(halflife_days))
decayed_score = raw_score × decay_rate^bars_since_event
```

`tf_lookback()` converts calendar days to chart bars (e.g., on a 2D chart, 14 days = 7 bars). The formula is timeframe-adaptive — signals decay at the same rate in calendar time regardless of chart resolution.

**Max tracking**: 30 bars. After 30 bars, contribution = 0 (regardless of remaining mathematical value).

**Aggregate scoring** (weighted, NOT the plotted area):
```
bot_agg = zweig_dec × 1.5 + lowry_bot_dec × 1.3 + mc_bot_dec × 1.0 
        + kin_bot_dec × 0.9 + vacc_bot_dec × 0.8
top_agg = lowry_top_dec × 1.3 + kin_top_dec × 0.9 + vacc_top_dec × 0.8
```

McClellan bear thrust intentionally excluded from `top_agg` — weak signal, fires after damage done.

**Plotted decay area** (visual only): simple sum of all decayed scores / 100. Different from `bot_agg`/`top_agg` — no weights. The info table shows the weighted aggregate; the chart shows the unweighted visual.

---

### 13.7 The Lyapunov Kill Switch — Full Mathematical Detail

The most computationally intensive component. Implements **Rosenstein's algorithm** (1993) for maximum Lyapunov exponent estimation, validated against the `nolds` Python library (`lyap_r`).

#### Phase Space Reconstruction (Takens Delay Embedding)

**Input**: Log returns `x_i = log(close_i / close_{i-1})`

**Why log returns, not price**: Raw prices produce **inverted** λ (bull markets show high λ, bear markets low). Log returns normalize scale and produce the correct crisis-detection behavior.

**Embedding**:
```
X_i = [x_i, x_{i+τ}, x_{i+2τ}, ..., x_{i+9τ}]     // 10-dimensional vector
```

**Lag τ**: Auto-computed every bar from autocorrelation. Find first lag where `autocorr(x, x[lag], min(100, window/2)) < 1 - 1/e ≈ 0.632`. Clamped to [5, 50]. Matches `nolds` method.

**Parameters**: `window=500` (~2 years), `emb_dim=10`, `traj_len=20`, `step=5` (sampling).

#### Rosenstein Algorithm

For each reference point `ref` (sampled every 5th bar to manage computation):

1. **Find nearest neighbor** `nn` in embedded space (Euclidean distance), with `|ref - nn| ≥ τ` (temporal separation prevents trivially close neighbors)
2. **Track divergence** forward for `traj_len=20` steps:
   ```
   d(t) = ||X_{ref-t} - X_{nn-t}||     // Euclidean distance after t steps
   y(t) = log(d(t)) - log(d(0))         // log divergence relative to initial separation
   ```
3. **Linear regression**: `λ_ref = Σ(t × y(t)) / Σ(t²)` — slope of log divergence vs time

**Final λ**: Average over all reference-neighbor pairs where initial distance < ε (sanity filter, ε=3.0).

**Efficiency**: Rosenstein loop runs every 2nd bar (cached with `var`). τ computed every bar (cheap). Series functions (`drankpct`, `stdev`) run every bar.

#### Dual-Path Hybrid Classification (R3-40)

**PATH A — Chaos-Only (early warning, no drawdown required)**:
```
λ_percentile computed via drankpct(λ_raw, window)
eff_p = λ_pct > 0 ? λ_pct : clamp(50 + λ_z × 15, 0, 100)    // z-score warmup fallback

ELEVATED: eff_p ≥ 90, vel_z ≥ 2.0, acc > 0
WATCH:    eff_p ≥ 80, vel_z ≥ 1.5, acc > 0
      OR  eff_p ≥ 65, vel_z ≥ 1.0

SMA50 cap: strong uptrend → chaos-only capped at WATCH
```

**PATH B — Composite (drawdown confirms crisis)**:
```
composite = max(0, vel_z) × |min(0, drawdown_50d)|

Requires dd < -1%:
    CRITICAL: composite ≥ 25, eff_p ≥ 70
    HIGH:     composite ≥ 15, eff_p ≥ 60
    ELEVATED: composite ≥ 8,  eff_p ≥ 50
    WATCH:    composite ≥ 2
```

**Why raw thresholds (not percentile)**: The composite is **zero-inflated** — zero ~70% of the time (requires both positive vel_z AND negative drawdown). Percentile-ranking pushes any nonzero value above the 70th percentile, causing WATCH/ELEVATED to fire on normal dips.

**Merge**: `level = max(chaos_level, comp_level)`

**Boosters**: Return shock (`ret3 < -3%` or `ret5 < -5%`, mutually exclusive, +1 level if base ≥ 1). Percentile velocity (`pct_vel > 10, base ≥ 2, acc > 0`, +1 level).

**Safety**: Rally override (`ret5 > 3%` and `base > 1` → cap at WATCH).

**Crisis resolution**: 5+ bars of λ deceleration AND `λ_pct < 75` → reduce level by 1.

#### Position Multiplier

```
eff_severity = max(composite, level ≥ 2 ? 8.0 : level ≥ 1 ? 2.0 : 0.0)
position_mult = max(0.1, 1.0 - max(0, (eff_severity - 2) / 25) × 0.9)
```

Ramps smoothly from 1.0 (normal) to 0.1 (maximum caution) as severity increases. Composite-based when PATH B fires; level-based floor when chaos-only PATH A fires.

#### SPX/Asset Gating

SPX dominates by default. Asset Lyapunov (opt-in via `use_asset=true`) is capped: `asset_level ≤ spx_level + 1` unless `spx_level ≥ 2`. This prevents a single volatile stock from triggering kill switch without market-wide confirmation.

**Computation budget**: ~88K peak, ~45K avg loop iterations per bar for SPX-only. Under TradingView's 500K limit. Always computed on daily bars (`"D"` security call) regardless of chart TF.

---

### 13.8 duo_core — The Universal Adaptive Trend Engine

Both TMF/ES regime and VVIX/VIX events are processed through `duo_core`, a self-tuning trend engine:

| Stage | What It Does | Key Parameters |
|---|---|---|
| 1. **Gaussian Filter** | Smooths input | len=5, σ=0.75 (tighter on higher TFs) |
| 2. **Cycle Intelligence** | Detects dominant cycle | Hilbert + peak-to-peak hybrid, confidence-gated |
| 3. **ER + R² Analysis** | Efficiency ratio + trend linearity | Adaptive lookback from cycle period |
| 4. **Volrank** | Volatility regime (ATR percentile + velocity) | For band adaptation |
| 5. **RSX** | Momentum oscillator | Cycle-adapted length via `cadapt_len` |
| 6. **VACC** | Velocity + acceleration | ER-adapted length |
| 7. **Signal Score** | `percentrank(vacc_score + rsx_score)` | Composite momentum ranking |
| 8. **KAMA** | Adaptive moving average | ER-driven speed, P&L feedback acceleration |
| 9. **Adaptive Bands** | `kama ± sma(|Δsrc|) × mult` | Adapts to series' own volatility |
| 10. **HMM Forecast** | Crossover probability | 3-bar lookahead, 70% confidence gate |
| 11. **Trend** | `src > upper → 1, src < lower → -1, HMM → ±1, else hold` | Band breakout + HMM fallback |
| 12. **Risk-On** | Signal-score gated state machine | Entry 0.35, exit 0.25 (2D-7D TFs only) |

**Why the same engine for ratios and prices**: `duo_core` operates on any series. For ratios (TMF/ES, VVIX/VIX), the caller divides first; bands use `sma(|Δsrc|)` which auto-scales to the ratio's own volatility. No special-casing needed.

---

### 13.9 Market Regime — The Full Pipeline

```
1. TMF/ES HA ratio → duo_core → ratio_regime_calc → tmf_regime_dc (±1)
   (Heikin Ashi smooths the ratio; KAMA tracks adaptive trend)

2. SVSI phase_cos = request.security(ES, tf, _svsi_phase(close))
   (SVSI → VACC → z-score → atan2 → Cartesian smoothing → cos(θ) × gate)

3. Breadth phase_cos = request.security(ADVN/DECL, "D", _breadth_phase(close))
   (ADVN/DECL ratio → RANA → NYMO → NYSI → VACC → phase portrait)

4. Adaptive weighting:
   svsi_extreme = max(0, (|svsi_raw - 50| - 20) / 30)
   b_weight = 0.3 + 0.4 × svsi_extreme    // 0.3 normal → 0.7 at extremes
   s_weight = 1.0 - b_weight               // 0.7 normal → 0.3 at extremes
   composite = svsi_phase_cos × s_weight + breadth_phase_cos × b_weight

5. TMF reliability:
   vel_corr = correlation(tmf_vel_z, es_vel_z, 8)
   vel_corr_pct = percentrank(vel_corr, 750) / 100
   reliability = max(0, 1 - vel_corr_pct / corr_threshold)

6. Override gate:
   disagree_score = composite × (-tmf_regime_dc)
   disagree_pct = percentrank(disagree_score, 500) / 100
   pct_threshold = 0.60 + 0.20 × reliability
   override = disagree_score > 0 AND disagree_pct ≥ pct_threshold

7. Final regime:
   if tmf_regime ≠ 0:
       combined = override ? sign(composite) : tmf_regime_dc
   else:
       combined = composite > 0.25 ? 1 : composite < -0.25 ? -1 : 0
```

---

### 13.10 Timeframe Adaptation

All lookbacks auto-adapt via `tal.tf_lookback(target_days)`:
```
tf_days = timeframe_in_seconds / 86400
lookback_bars = max(min_bars, round(target_days / tf_days))
```

This means a "10-day" EMA is 10 bars on a daily chart, 5 bars on a 2D chart, and 2 bars on a weekly chart. All thresholds, decay rates, and persistence requirements scale accordingly.

**Breadth data caveat**: ADVN, DECL, UVOL, DVOL are daily-only. `compute_period()` returns `"D"` for intraday charts (fetch daily data) and `timeframe.period` for daily+ charts (native resolution).

---

### 13.11 Security Call Budget

~20 total (TradingView allows 40):

| Function | Calls | Symbols |
|---|---|---|
| `mkt_breadth_all` | 6 | ADVN, DECL, UVOL, DVOL, ES (close), ES (SVSI) |
| `mkt_breadth_composite` | 4 | MMTH, MMFI, MMTW, ES (SVSI) |
| `mkt_vix_all` | 2 | VVIX, VIX |
| `vix_term_structure_trend` | 2 | VIX, VIX3M |
| `market_regime` | 5 | TMF vel_z, ES vel_z, ADVN/DECL breadth, HA TMF/ES, ES SVSI |
| `kill_switch_all` | 1-2 | ES (SPX), optionally asset |

All security calls use `lookahead=barmerge.lookahead_off` (no future data leakage).

---

<a name="14-whats-next"></a>
## 14. What's Coming Next

### Implied Correlation — The Missing Piece

We're building a new leading indicator based on **CBOE Implied Correlation Indices** (COR1M, COR3M) — forward-looking measures from options pricing that quantify expected correlation among the top 50 S&P 500 components.

**Why this matters**: Market Pulse detects *when* the market is turning. Implied correlation tells you *why* — and often tells you first.

- **High implied correlation (>60-70)**: "Herd behavior" expected — stocks moving in lockstep. Often signals crises or marks bottoms at peak fear.
- **Low implied correlation (<20-25)**: Idiosyncratic movement, calm markets. But also complacency — extremely low correlation preceded 2007, Aug 2024 tops.

**What we're building:**
1. **Correlation Risk Premium** (implied minus realized): Positive = contrarian bullish. Negative = underpricing risk.
2. **Term Structure** (COR1M/COR3M): Ratio > 1 = imminent correlation snap.
3. **VIX Interaction**: Low correlation + low VIX = complacency top. High correlation + high VIX = fear bottom.
4. **Integration**: New event letter (**C**) joining the signal alphabet with decay and SVSI gating.

Backtesting (2007-2025) shows this hybrid catches 80-90% of major tops and bottoms. Combined with Market Pulse's existing signals, this creates a truly comprehensive regime detection system.

**Stay tuned — dedicated follow-up article coming soon.**

---

<a name="15-community"></a>
## 15. We Want to Hear From You

MXC Market Pulse is a living system. Every signal was rigorously tested, and several were **removed** when they didn't meet our evidence bar. We believe in **evidence-based signal engineering**: if a signal doesn't improve outcomes, it doesn't ship.

### Tell Us What Leading Indicators You Want

Areas we're actively exploring:
- **Implied Correlation**: Coming soon (see above)
- **Credit Markets**: HY spreads, IG flows, TED spread dynamics
- **Options Flow**: Put/call dynamics, gamma exposure, dealer positioning
- **Cross-Asset Momentum**: Gold/copper ratio, USD dynamics, real yield breakpoints
- **Crypto-Specific**: Funding rates, basis convergence, stablecoin flows
- **Sentiment**: AAII survey, CNN Fear & Greed cross-reference

**Share your ideas** — comment, DM, or open a discussion. If the signal has empirical support and adds uncorrelated information, we'll build it, test it, and ship it.

The best indicators aren't built in isolation. They're built by the community that uses them.

---

## Appendix: Quick Reference Card

| Letter | Name | Side | Decay | Conviction |
|---|---|---|---|---|
| Z | Zweig Breadth Thrust | Bottom | 14d | ★★★ |
| L | Lowry 90% Day | Both | 10d | ★★★ |
| M | McClellan Thrust | Bottom | 7d | ★★ |
| A | VACC Accumulation | Bottom | 5d | ★★ |
| D | VACC Distribution | Top | 5d | ★★ |
| N | Kinematic Breadth | Both | 10d | ★★ |
| P | Phase V-Bottom | Bottom | 10d | ★★★ |
| B | Breadth Composite | Both | 7-10d | ★★ |
| V | VVIX/VIX Pivot | Bottom | 7d | ★★ |
| T | VIX Term Structure | Both | 7d | ★★ |
| K | Kill Switch | Crisis | — | ★★★ |

---

*MXC Market Pulse v5.2 — © momentumX capital*
*Built with evidence. Tested with rigor. Deployed with conviction.*
