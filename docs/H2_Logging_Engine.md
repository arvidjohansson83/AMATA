# AMATA Live Trade Logging
### How AMATA Captures Every Trade for Analysis, ML, and Continuous Improvement

Most trading systems execute trades — but they don’t *learn* from them.  
AMATA does.

To evolve, validate, and improve its strategies, AMATA records every trade, every signal, every regime, and every state transition in a structured, machine‑readable format.

This is the foundation of AMATA’s data‑driven architecture.

---

## **Purpose**
The **Live Trade Logging** module provides a complete, deterministic record of every trade AMATA executes.  
It enables reproducibility, analysis, ML‑training, and continuous system improvement by mirroring the same structure used in the **[Backtesting Pipeline](./I1_Backtesting_Pipeline.md)**.

---

## 🧩 **Why Live Trade Logging Matters**

Backtesting gives you historical performance.  
Live logging gives you *real‑world behaviour*:

- real spreads  
- real slippage  
- real volatility  
- real execution timing  
- real market microstructure  

AMATA captures all of this — automatically.  
This is how AMATA becomes a continuously improving system.

---

## 📦 **What AMATA Logs**  
AMATA uses a **three‑file logging architecture** to capture the *entire lifecycle* of every trade:

---

### **Summary of Log Files**

| File                     | Purpose                           | Frequency          |
|--------------------------|-----------------------------------|--------------------|
| **trade_entry.csv**      | Entry snapshot                    | Once per trade     |
| **trade_progress.csv**   | Live telemetry (bar‑by‑bar)       | Every bar          |
| **trade_exit.csv**       | Exit summary + realized result    | Once per trade     |

---

## **1. trade_entry.csv — Entry Snapshot**  
Captures all market conditions at the moment the trade is opened:

- **symbol, direction, entry price**  
- **regime and session**  
- **volatility metrics**  
- **swing distance**  
- **news proximity**  
- **indicator min/max windows**  
- **strategy‑relevant features**

This file represents the *decision moment* — why the trade was taken.

---

## **2. trade_progress.csv — Live Telemetry**  
Records every bar during the trade:

- **high / low / close**  
- **volatility changes**  
- **trend metrics**  
- **swing structure**  
- **real‑time indicator evolution**

This is AMATA’s “black box” — the full behavioural timeline of the trade.

---

## **3. trade_exit.csv — Exit Summary**  
Captures the final state:

- **exit price**  
- **exit time**  
- **realized R**  

This is where edge is measured.

---

All parameters and state transitions used during live trading are written to structured CSV‑files.  
It makes it optimal to further analyze, visualize and work with the data in Python for improvements.

- Every trade becomes a data point.  
- Every data point becomes part of a dataset.  
- Every dataset becomes part of AMATA’s evolution.

---

## 🔄 **Unified Data Model: Backtest = Live**

AMATA uses the same data structure for:

- **historical backtesting**  
- **live trade logging**

This means:

- the same columns  
- the same logic  
- the same regime tagging  
- the same strategy tagging  
- the same opportunity detection  

AMATA can be trained on historical data —  
and later refined with live data.

---

## 🧠 **ML‑Ready by Design**

AMATA’s logging format is built for:

- **feature extraction**  
- **regime classification**  
- **volatility modelling**  
- **edge validation**  
- **strategy comparison**  
- **reinforcement‑style improvement**

Nothing is unstructured.  
Nothing is ambiguous.  
Everything is deterministic.

---

## 🚀 **The Role of Live Logging in AMATA’s Future**

Live Trade Logging is not just a utility.  
It is **AMATA’s memory**.

It enables:

- **continuous optimisation**  
- **strategy evolution**  
- **symbol‑specific tuning**  
- **volatility adaptation**  
- **regime refinement**  
- **portfolio‑level intelligence**

AMATA doesn’t just trade.  
AMATA learns and adapts to real market behaviour.

---
