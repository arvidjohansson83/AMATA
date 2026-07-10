# SL Optimization — GBPUSD (29 May 2026)
Support Example — SL Misalignment During Trend Continuation

## 🔄 Version Context
This support example is taken from the same evaluation period as the EURCAD main SL‑optimization case.
Since then, AMATA’s SL‑multipliers have been refined with **more trades, improved volatility scaling, and enhanced trend‑behaviour profiling**.

---

## 🖼️ Illustration

![GBPUSD SL Example](/examples/I3_sl_optimization_gbpusd.png)
*GBPUSD — AMATA placed an optimal trend-entry, but the SL was positioned slightly too tight during early trend formation, resulting in a premature exit before the continuation unfolded.*

---

GBPUSD traded with higher intraday volatility compared to EURCAD. AMATA detected a valid continuation setup, but the SL was placed 1.2 pips too tight, equivalent to 0.52 ATR at the time of entry.
This half‑ATR misalignment was enough to trigger a premature exit during early trend formation — even though the trend continued immediately after the SL‑hit and extended several R beyond the exit.

---

## 🎯 Purpose of the Example
This example highlights how a slightly misaligned SL‑multiplier can cause a premature exit during a valid trend continuation phase — even when the trend structure is clean and stable.

---

## 📈 Behavioural Context
GBPUSD displayed:

- strong initial thrust
- stable trend formation
- clean continuation behaviour
- no exhaustion signals
- multi‑R potential beyond the SL‑hit

The behaviour was structurally similar to EURCAD, but GBPUSD’s volatility profile requires wider breathing room.

## 🧩 SL‑Multiplier Insight
In this trade:

- the SL was placed too tight relative to GBPUSD’s volatility profile
- the trend continued immediately after the SL‑hit
- the movement extended several R beyond the exit

This demonstrates why AMATA’s SL‑geometry must be symbol‑aware and volatility‑scaled.
The improved SL‑multipliers in the current version of AMATA reduce the likelihood of premature exits in similar GBPUSD trend phases.

---

## ⭐ Why this matters
This example reinforces why symbol‑specific ATR geometry is essential — and how refined SL‑multipliers improves AMATA’s performance in higher‑volatility symbols like GBPUSD.

---

## 🚀 Takeaway
This support example reinforces the importance of behaviour‑aligned SL‑multipliers:

- **tight SL → premature exit** 
- **behaviour‑aligned SL → full continuation potential**

Since this trade, AMATA has identified that GBPUSD’s volatility requires slightly wider breathing room than symbols such as EURCAD — and the platform's refined SL‑geometry now accounts for this difference.

---