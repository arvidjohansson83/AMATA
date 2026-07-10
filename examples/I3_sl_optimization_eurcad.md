# SL Precision Example - EURCAD (8 May 2026)
How AMATA’s SL‑Multipliers Prevent Behavioural Misalignment

## 🔄 Version Context

This example is taken during the testing and evaluation phase of AMATA, using M5 bar‑close trailing logic. Since then, the SL Optimization Pipeline has been updated with **more trades, more behavioural data, and improved SL‑multiplier stability**.

---

## 🎯 Purpose of the Example

This trade demonstrates how SL‑multipliers determine whether a trend‑strategy can survive the natural adverse movement before continuation.

## 🖼️ Illustration

![EURCAD SL Example](/examples/I3_sl_optimization_EURCAD.png)
*EURCAD — textbook continuation behaviour with SL placed slightly too tight*.

EURCAD traded in a narrow Asian-session range. AMATA detected a valid setup and placed an optimal entry. Later in the morning, Euro‑driven news created a strong volatility expansion — producing a **clean, multi‑R continuation pattern**.

The movement extended to more than 10R, but in this trade, the SL was **0.5 pips too narrow**, equivalent to **0.22 ATR at entry**.
This small misalignment was enough to trigger a premature exit before the continuation unfolded.

---

## A Textbook Example
This is a textbook example of:

- why SL‑multipliers must be correctly calibrated
- how tiny differences determine the entire R‑profile
- how AMATA Gridsearch Pipeline optimizes SL

Even though the behaviour was perfect, the SL‑geometry was just slightly misaligned — and that is exactly what multiplier optimization solves. The more data AMATA gets - the better the platform can find each symbol's natural movements and patterns.

---

## 📈 Behavioural Context
EURCAD displayed:

- strong thrust
- clean continuation
- stable volatility
- no early exhaustion
- clear multi‑R extension potential

This is precisely the type of movement trend-strategies in AMATA Platform are designed to capture.

---

## 🧩 SL‑Multiplier Insight

In this example, the SL‑multiplier was almost perfect, but:

- 1 pip too tight → SL hit risk
- 1 pip wider → full 10R continuation

This is why SL‑multipliers are critical:
they define how much “breathing room” a behaviour needs before proving itself.

In the current version of AMATA, the SL‑multiplier has been refined using:

- more trades
- more continuation clusters
- improved volatility scaling
- enhanced trend‑behaviour profiling

The result is a more stable and behaviour‑aligned SL‑geometry.

---

## ⭐ Why this matters
This example shows how SL‑geometry directly influences AMATA’s performance — and why volatility‑normalized multipliers are essential for behaviour‑aligned execution.

---

## 🚀 Takeaway
This example shows how AMATA’s SL‑optimization converts:

**fragile trend-entries** 
→ into
**robust continuation‑strategies**

A well-calibrated SL‑multiplier is what allows AMATA to remain in high‑quality movements long enough for the behaviour to unfold.

With the refined SL‑geometry in current version of AMATA, the platform aligns even more precisely with real market structure — respecting natural volatility while preserving continuation potential.

---