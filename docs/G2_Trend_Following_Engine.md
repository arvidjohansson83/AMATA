# AMATA Trend Following Engine 
**Behaviour‑Aligned Volatility‑Adaptive Profit‑Locking System**

AMATA’s Trend Following Engine is a core risk‑management module responsible for transforming raw price movement into structured trailing behaviour.
It continuously evaluates **volatility, continuation strength, structural integrity, and trend behaviour for every active symbol** — and adjusts Stop Loss levels mechanically based on **symbol‑specific ATR geometry**.

The engine is fully mechanical, symbol‑adaptive, and follows open positions every bar.

---

## Purpose of the Trend Following Engine
The Trend Following Engine determines:

- when risk should be removed
- when trailing should activate
- how trailing should advance
- when a trend is considered broken
- when a position should be closed

It is the foundation of AMATA’s ability to lock profit progressively while respecting natural market behaviour.

All Strategy Modules rely on the Trend Following Engine to:

- secure trades
- maintain breathing room
- avoid premature exits
- align trailing with volatility
- exit positions at structural breaks

This engine is the bridge between raw price movement and behaviour‑aligned risk management.

---

## Core Capabilities
The Trend Following Engine provides:

- ATR‑normalized SL placement
- ATR‑based activation thresholds
- ATR‑based trailing steps
- symbol‑specific volatility adaptation
- continuation‑aligned trailing
- Break Of Structure (BOS)‑driven exit logic
- multi‑step profit locking
- behaviour‑aligned trend termination

These capabilities allow AMATA to trail positions in a way that is:

- mechanical
- deterministic
- volatility‑aware
- symbol‑specific
- grid‑search optimized

---

## Symbol‑Specific ATR Geometry
Every symbol in AMATA has its own optimized ATR multipliers:

- **ATR SL Multiplier**
- **ATR Activation Multiplier**
- **ATR Step Multiplier**

These multipliers define:

- how far price must travel before risk is removed
- how far price must travel before trailing begins
- how far price must travel before trailing advances
- how much breathing room the trend requires
- when structural breaks invalidate continuation

This geometry is **unique per symbol** and derived from AMATA’s Gridsearch Optimization Pipeline.

---

## Real‑Time Trailing Pipeline
For every minute, AMATA executes:

- Read symbol profile
- Evaluate ATR volatility
- Check continuation strength
- Check activation threshold
- Check trailing step threshold
- Advance TSL if conditions are met
- Check BOS structural break
- Close trade if trend is invalidated
- Log trailing behaviour

This pipeline runs independently for each symbol, enabling true multi‑asset trailing behaviour.

---

## Behaviour‑Aligned Exit Logic
The Trend Following Engine closes trades only when:

- continuation fails
- volatility shifts
- structure breaks
- trend integrity is lost

This ensures that AMATA exits positions at the **correct behavioural moment** — not based on arbitrary pip distances or fixed trailing rules.

--- 

## Why Trend Following Matters
The Trend Following Engine enables AMATA to:

- lock profit progressively
- maintain breathing room
- avoid premature exits
- adapt trailing to volatility
- exit at structural breaks
- support multi‑strategy execution
- scale across symbols and timeframes

Without this engine, AMATA would behave like a traditional EA.
With it, AMATA becomes a behaviour‑aligned, volatility‑adaptive trailing system.

---

## 📎 Example
A complete behaviour‑aligned Trend Following Engine example is available here:
[Trend Following Engine — Example](/examples/G2_Trend_Following_Engine_NZDCAD.md)