# TSL Activation Example — Breakeven Exit in Low‑Volatility Regime (NZDUSD — 25 June 2026)

## 🔄 Version Context
This example is taken during the testing and evaluation phase of AMATA.
Since then, the TSL Activation Multiplier has been refined with **more trades, improved volatility scaling, and enhanced behavioural profiling**, especially for low‑volatility symbols such as NZDUSD.

---

## 🎯 Purpose
To demonstrate how **early TSL activation** in a *low‑volatility regime* can move SL to breakeven before the behaviour has stabilised — causing premature exits even during clean trend formation.

---

## 🖼️ Illustration

![NZDUSD TSL BE example](/examples/I3_be_optimization_nzdusd.png)
*NZDUSD — clean thrust and early continuation, but TSL activated too early due to low ATR and tight activation geometry*.

NZDUSD formed a clean thrust during the London session and began developing a stable continuation pattern.
However, due to extremely low ATR, the TSL Activation Multiplier triggered too early.
SL was moved to breakeven before the behaviour had fully stabilised.
A normal micro‑pullback stopped the trade out at BE — and price continued in the intended direction afterwards.

This is a classic low‑volatility activation issue:
**the behaviour was valid, but the breathing room was insufficient**.

---

## 📈 Behavioural Context
NZDUSD displayed:

- very low ATR (low‑volatility regime)
- clean thrust
- early continuation
- shallow micro‑pullbacks
- stable trend formation *after* the breakeven exit

The behaviour was structurally sound — but the activation occurred too early relative to volatility.

---

## 🧩 TSL Insight
TSL activated too early due to tight activation geometry in a low‑volatility environment.
The trade was stopped out at breakeven during a normal micro‑pullback, and price continued several R afterwards.

This indicates:

- activation multiplier too tight for low‑volatility symbols
- insufficient breathing room
- premature transition from risk → reward
- behaviour not yet stabilised at activation

---

## ⭐ Why this matters
Low‑volatility symbols require wider activation geometry to avoid premature breakeven exits. 
This example demonstrates how tight activation multipliers reduce AMATA’s performance in shallow‑ATR environments, where normal micro‑pullbacks are part of healthy trend formation.

---

## 🚀 Takeaway
Low‑volatility symbols require **wider activation multipliers** to avoid premature breakeven exits.
Correct activation timing ensures the behaviour has proven itself before SL is moved to breakeven — preserving continuation potential even in shallow‑volatility regimes.

---