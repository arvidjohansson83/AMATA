# Trend Following Engine — Behaviour‑Aligned Progression (Example Case)
**(NZDCAD — 28 April 2026)**

## 🔄 Version Context
This example is taken during the testing and evaluation phase of AMATA. 
The Trend Following Engine (TFE) used the following ATR‑normalized multipliers for this specific trade:

- **SL Multiplier**: 1.0 ATR
- **TSL Activation**: 2.0 ATR
- **TSL Step**: 0.3 ATR

Since then, TFE has been refined with more trades, improved volatility scaling, and enhanced behaviour profiling.

---

## 🎯 Purpose
This example demonstrates how AMATA’s Trend Following Engine:

- places SL based on optimized symbol‑specific volatility
- activates trailing only after behaviour confirmation
- follows price with behaviour‑aligned geometry
- protects profit without killing continuation
- handles trend progression in real time

This example shows a complete TFE progression from **entry → activation → trailing → exit**.

---

## 📏 Execution Geometry

- **Entry price**: 0.80306
- **ATR at entry**: 0.00045 (4.5 pips)
- **Stop Loss (1.0 ATR)**: 𝑆𝐿=0.80306 − 0.00045 = **0.80261**
    → **SL was placed 4.5 pips below entry**, providing correct breathing room for NZDCAD’s volatility profile.

- **TSL Activation (2.0 ATR)**: 𝑇𝑆𝐿_𝑎𝑐𝑡𝑖𝑣𝑎𝑡𝑖𝑜𝑛=0.80306+(0.00045)⋅2= **0.80396**
    → **TSL activated only after price moved +9.0 pips**, confirming trend structure.

- **TSL Step (0.3 ATR)**: 𝑇𝑆𝐿_𝑠𝑡𝑒𝑝=0.00045⋅0.3= **0.000135**
    → **Each trailing step moved SL 1.35 pips upward** — forming a clean, behaviour‑aligned staircase.

---

## 🖼️ Illustration - Trend Following Engine progression (NZDCAD)  

![NZDCAD Entry](/examples/G2_tfe_entry_nzdcad.png)  
The entry at **0.80306** was validated by stable volatility and clean thrust behaviour. ATR at entry defined the baseline geometry: the initial stop‑loss was placed at **1.0 ATR** below entry, reflecting AMATA’s volatility‑normalized risk model.

![NZDCAD Trailing Activation](/examples/G2_tfe_trailing_activation_nzdcad.png)

As price advanced, continuation strength remained stable. When the engine’s behavioural threshold of **2.0 ATR** was reached, AMATA moved the stop‑loss to break‑even and established the anchor for behaviour‑aligned trailing.

![NZDCAD Trailing Steps](/examples/G2_tfe_trailing_steps_nzdcad.png) 
Each trailing step was calculated using a **0.3 ATR** increment, forming a staircase aligned with volatility contraction and strengthening directional flow. This behaviour is visible in the controlled SL progression throughout the trend.

The position was not closed by a pullback. Instead, AMATA executed a **forced institutional close**, just before liquidity drops and spreads expand during the transition from US session into Pacific/Asian session. This nightly forced close is part of AMATA’s institutional risk model: **no overnight exposure, no swap costs, no illiquid conditions, no spread‑expansion risk**.

The trade closed at **0.80544**, corresponding to a **3.48R reward** relative to the initial 1R risk — completing a full behaviour‑aligned progression from **entry → break‑even → trailing → institutional close**.

---

## 📈 Behavioural Context
NZDCAD displayed:

- clean thrust
- stable early continuation
- low‑to‑medium ATR
- clear trend progression
- symbol‑typical micro‑pullbacks
- stable structure after activation

This is a textbook NZDCAD trend profile:
**calm volatility, clean thrust, stable continuation**.

---

## 🧩 TFE Insight
Trend Following Engine handled the trade exactly as designed:

- SL placed correctly according to volatility
- TSL activated only after behaviour confirmation
- trailing followed price with correct geometry
- SL moved in stable, incremental steps
- exit occurred through AMATA’s nightly institutional close 

This demonstrates how AMATA's Trend Following Engine:

- avoids premature exits
- protects profit in real time
- respects symbol‑specific volatility
- preserves continuation potential
- avoids low‑liquidity conditions and spread expansion during the US → Pacific transition

---

## ⭐ Why This Matters
The Trend Following Engine is AMATA’s most robust module.
This example shows why:

- **correct SL geometry**
- **correct activation timing**
- **correct trailing steps**
- **correct exit behaviour**

TFE is built to:

- **follow the trend**
- **protect profit**
- **avoid noise‑driven exits**
- **respect volatility**
- **maximize continuation potential**

---

## 🚀 Takeaway
This NZDCAD example shows a **fully behaviour‑aligned trend progression**:

**Entry → SL → Activation → Trailing → Exit**

AMATA’s TFE handled the trade exactly according to design — a clean demonstration of how trend strategies should behave in real market structure.

---