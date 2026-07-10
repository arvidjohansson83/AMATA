# TSL Step Example — Premature Trailing in High‑Volatility Regime (GBPAUD — 20 May 2026)

## 🔄 Version Context
This example is taken during the testing and evaluation phase of AMATA. Since then, the TSL Step Multiplier has been refined with **more trades, improved volatility scaling, and enhanced behaviour‑profiling**, especially for high‑volatility symbols such as GBPAUD.

---

## 🎯 Purpose
To demonstrate how **TSL Step geometry that is too tight** can cause premature trailing exits in high‑volatility symbols — even when continuation behaviour is valid and structurally sound.

This example highlights why GBPAUD requires **wider breathing room** than low‑ or medium‑volatility symbols.

---

## 🖼️ Illustration

![Incorrect Trailing Step ATR Multiplier](/examples/I3_tsl_optimization_gbpaud.png)
*GBPAUD — strong thrust and valid continuation, but TSL followed price too aggressively and exited during normal high‑volatility pullback*.

---

## 📈 Behavioural Context
GBPAUD displayed:

- strong initial thrust
- clean early continuation
- deep micro‑pullbacks (symbol‑typical)
- high intraday volatility
- stable trend formation after the premature exit

The underlying movement followed a classic high‑volatility continuation pattern:

1. **Initial thrust** — strong directional impulse
2. **Continuation phase** — behaviourally valid but volatility‑heavy
3. **Micro‑pullbacks** — deeper than low‑volatility symbols
4. **Premature exit** — TSL too tight relative to volatility
5. **Continuation afterwards** — several R beyond the exit

GBPAUD often forms **clean continuation with deep pullbacks**, making it a symbol where tight trailing geometry is risky.

---

## 🧩 TSL Insight
TSL activated at the correct moment, but the **step geometry was too tight** for GBPAUD’s volatility profile.
The trailing stop was hit during a normal high‑volatility pullback — not during structural exhaustion.

Price continued several R afterwards, indicating:

- trailing geometry too aggressive
- insufficient breathing room
- premature exit during valid continuation
- volatility profile not fully respected
- symbol‑specific behaviour mismatch

This is a textbook example of **TSL Step misalignment** in high‑volatility symbols.

---

## ⭐ Why this matters
This example shows how behaviour‑aligned trailing directly affects AMATA’s performance in high‑volatility environments.
Symbols like GBPAUD require **wider step multipliers** to avoid premature exits during normal volatility‑driven pullbacks — ensuring continuation potential is preserved.

---

## 🚀 Takeaway
GBPAUD’s volatility profile demands **broader trailing geometry**.
This example demonstrates how tight TSL Step multipliers can cause premature exits even when the trend structure is valid and continuation is likely.

AMATA’s refined trailing logic now adapts more effectively to:

- **high‑volatility symbols**
- **deep micro‑pullbacks**
- **continuation under volatility pressure**
- **behaviour‑aligned breathing room**

This ensures more robust performance and reduces premature trailing exits in symbols like GBPAUD.

---