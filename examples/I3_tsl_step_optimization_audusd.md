# TSL Step Example — Premature Trailing in Shallow‑Continuation Behaviour (AUDUSD — 15 May 2026)

## 🔄 Version Context
This example is taken during the testing and evaluation phase of AMATA. Since then, the TSL Step Multiplier has been refined with **more trades, improved volatility scaling, and enhanced continuation‑profiling**, especially for shallow‑continuation symbols such as AUDUSD.

---

## 🎯 Purpose
To demonstrate how **TSL Step geometry that is too tight** can cause premature trailing exits in shallow‑continuation environments — even when the trend structure is valid and continuation potential is high.

AUDUSD is a symbol where micro‑pullbacks are **fast, shallow, and frequent**, making it highly sensitive to tight trailing geometry.

---

## 🖼️ Illustration

![Incorrect Trailing Step ATR Multiplier](/examples/I3_tsl_optimization_audusd.png)
*AUDUSD — clean thrust and valid continuation, but TSL followed price too aggressively and exited during a normal shallow pullback*.

---

## 📈 Behavioural Context
AUDUSD displayed:

- clean initial thrust
- shallow continuation
- fast micro‑pullbacks
- low ATR
- stable trend formation after the premature exit

The underlying movement followed a classic shallow‑continuation pattern:

- **Initial thrust** — strong directional impulse
- **Early continuation** — behaviourally valid but shallow
- **Micro‑pullbacks** — quick, symbol‑typical retracements
- **Premature exit** — TSL too tight relative to shallow behaviour
- **Continuation afterwards** — several R beyond the exit

AUDUSD often forms **clean continuation with shallow pullbacks**, making it a symbol where tight trailing geometry is especially risky.

---

## 🧩 TSL Insight
TSL activated at the correct moment, but the **step geometry was too tight** for AUDUSD’s shallow‑continuation profile.
The trailing stop was hit during a *normal* micro‑pullback — not during structural exhaustion.

Price continued several R afterwards, indicating:

- trailing geometry too aggressive
- insufficient breathing room
- premature exit during valid continuation
- shallow‑continuation behaviour not fully respected
- symbol‑specific mismatch in step‑geometry

This is a textbook example of **TSL Step misalignment** in shallow‑continuation symbols.

---

## ⭐ Why this matters
This example shows how behaviour‑aligned trailing directly affects AMATA’s performance in shallow‑continuation environments.
Symbols like AUDUSD require **wider step multipliers** to avoid premature exits during normal micro‑pullbacks — ensuring continuation potential is preserved.

---

## 🚀 Takeaway
AUDUSD’s shallow‑continuation profile demands **broader trailing geometry**.
This example demonstrates how tight TSL Step multipliers can cause premature exits even when the trend structure is valid and continuation is likely.

AMATA’s refined trailing logic now adapts more effectively to:

- **shallow‑continuation symbols**
- **fast micro‑pullbacks**
- **low‑ATR environments**
- **behaviour‑aligned breathing room**

This ensures more robust performance and reduces premature trailing exits in symbols like AUDUSD.

---