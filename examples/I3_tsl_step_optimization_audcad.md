# TSL Step Optimization — Correct Exit at Exhaustion (AUDCAD — 9 June 2026)

## 🔄 Version Context
This example is taken during the testing and evaluation phase of AMATA.
Since then, the TSL Step Multiplier has been refined with **more trades, improved volatility scaling, and enhanced exhaustion‑profiling**.

---

## 🎯 Purpose
To demonstrate how AMATA’s TSL‑engine exits trades correctly when the behavioural structure breaks — even when continuation potential is limited afterwards.
This example also shows how trailing behaves on AUDCAD’s characteristic volatility profile.

---

## 🖼️ Illustration

![AUDCAD - Correct Trailing Step ATR Multiplier](/examples/I3_tsl_optimization_audcad.png)
*AUDCAD — TSL exit during exhaustion; behaviour‑aligned trailing*.

---

## 📈 Behavioural Context
AUDCAD displayed:

- clean thrust
- shallow continuation
- early exhaustion signals
- deeper structural pullback
- limited continuation afterwards

The underlying movement followed a classic exhaustion pattern:

1. **Initial thrust** — strong directional impulse
2. **Shallow continuation** — stable but limited follow‑through
3. **Exhaustion** — momentum loss and wick‑driven hesitation
4. **Deeper pullback** — break of continuation structure

AUDCAD often forms shallow continuation phases followed by abrupt exhaustion — this trade is a textbook example of that behaviour.

---

## 🧩 TSL Insight
TSL activated at the correct moment and followed price with behaviour‑aligned geometry.
The trailing stop was hit during a deeper pullback — exactly where the continuation structure broke.

Price continued slightly afterwards, but the exit was correct and aligned with:

- symbol‑specific volatility
- exhaustion behaviour
- structural break of continuation
- optimal profit protection

This indicates:

- correct trailing geometry
- correct exit timing
- correct exhaustion detection
- symbol‑specific behaviour handling

---

## ⭐ Why this matters
This example demonstrates how behaviour‑aligned trailing improves AMATA’s performance in shallow‑continuation symbols.  
AUDCAD’s volatility profile often produces abrupt exhaustion — and correct step geometry ensures exits occur **exactly** when continuation breaks, not earlier.

---

## 🚀 Takeaway
This example validates AMATA’s trailing logic across symbols.
TSL protected profit during exhaustion and structural break — exiting precisely when the behaviour shifted and continuation potential diminished.

AMATA’s trailing engine adapts to:

- **symbol‑specific volatility**
- **exhaustion patterns**
- **continuation depth**
- **structural breaks**

This ensures robust and behaviour‑aligned exits even in shallow‑continuation symbols like AUDCAD.

---