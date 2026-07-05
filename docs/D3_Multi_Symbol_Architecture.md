# AMATA Multi‑Symbol Architecture  
**How AMATA Operates as a True Multi‑Asset Trading Agent**

AMATA is not designed to trade a single symbol.  
True to its name - It is built to operate as an **Autonomous Multi‑Asset Trading Agent**, capable of running multiple symbols, multiple strategies, and multiple market conditions/regimes — all in parallel, all without interference.

This part builds on the [Multi‑Strategy](./D2_Multi_Strategy_Architecture.md) and [Boost](./C2_Boost_Architecture.md) Architectures, extending AMATA from vertical scaling (strategies) to horizontal scaling (symbols).

---

## Symbol‑Level Isolation

Each symbol in AMATA runs through its own fully isolated processing pipeline.  
This includes:

- **Regime Engine state**  
- **Volatility state**  
- **Safety state (local symbol‑level checks)**  
- **Strategy stack**  
- **Entry Engine permissions**  
- **Execution pipeline**  
- **Symbol‑specific thresholds and parameters**

No symbol shares internal state with another.  
This prevents:

- cross‑symbol contamination  
- shared indicator buffers  
- timing conflicts  
- race conditions  
- inconsistent behaviour  

Each symbol is treated as its own autonomous micro‑environment.

---

## Global vs Local State

AMATA separates state into two categories:

### Local State (per symbol)

- **regime classification**  
- **volatility conditions**  
- **strategy activation**  
- **entry permissions**  
- **execution sequencing**  
- **symbol‑specific risk thresholds**

### Global State (platform‑level)

- **Safety Engine global state**  
- **maxDailyLoss**  
- **maxDrawdown**  
- **news blocks**  
- **portfolio‑level risk constraints**

This separation ensures that:

- symbols remain independent  
- global risk is enforced consistently  
- no symbol can violate platform‑level safety  
- portfolio behaviour remains predictable  

---

## Symbol Scheduling & Loop Architecture

AMATA does not rely on MT5 tick events or asynchronous callbacks.  
Instead, it runs a **continuous market evaluation loop** that scans the market, detects regime changes, and evaluates each symbol in a deterministic sequence.

This loop is the foundation of AMATA’s stability and multi‑symbol capability.

---

### Regime‑Driven Execution

For every new candle, AMATA updates the [**Regime Engine**](./B1_Regime_Engine.md) for each symbol.
When a regime change is detected, AMATA immediately checks:

> **Is this regime approved for trading for this symbol?**

If the regime is not approved → the symbol remains in a neutral state.  
If the regime *is* approved → AMATA enters a **WAITING_FOR_PRICE** state.

In this state, AMATA loads:

- symbol-level thresholds  
- STOP/LIMIT activation levels  
- strategy‑specific filters  
- earliest entry rules  
- session filters  

AMATA now waits for the symbol to reach a **required structural validation state** that confirms edge for *this exact regime*.

Only when both conditions are true:

1. **Regime is valid**, and  
2. **The symbol satisfies the structural conditions associated with this regime**

…does AMATA allow execution.

If the regime changes during this waiting period, the entire process is aborted and reset.

---

### Regime‑Driven State Validation

AMATA executes only when a symbol reaches a **validated opportunity state** — a proprietary  
set of structural and behavioural conditions that have demonstrated statistical edge within  
the current regime. These states are defined externally in the symbol profile and act as  
the final confirmation layer before any strategy is permitted to execute.

---

### The Deterministic Evaluation Loop

In each cycle, AMATA performs:

1. **Collect global context**  
   Safety Engine, maxDailyLoss, news blocks, global risk.

2. **Iterate through each symbol**  
   Always in the same order for deterministic behaviour.

3. **Evaluate symbol‑level context**  
   Regime, volatility, thresholds, local safety.

4. **Run the strategy stack**  
   Each strategy independently checks if it has edge.

5. **Apply Entry Engine gating**  
   Timing, sequencing, earliest entry, session filters, regime validation.

6. **Execute orders through the Execution Engine**  
   Clean, conflict‑free order handling.

---

### Why This Architecture Matters

This design ensures:

- **regime‑aligned execution flow**  
- **structural validation before action**  
- **consistent timing across symbols**  
- **no conflicting or overlapping execution flows**  
- **equal processing priority for all symbols**  
- **fully deterministic system behaviour**  

AMATA behaves like a portfolio‑level engine, not a tick‑driven script.

---

### Deterministic vs Event‑Driven

Event‑driven systems depend on tick frequency and broker behaviour.  
AMATA avoids this by controlling its own timing through a **deterministic evaluation cycle**, ensuring stable and predictable multi‑symbol execution.

---

## Multi‑Symbol + Multi‑Strategy = Portfolio Engine

When combining:

- **Multi‑Strategy** (vertical scaling)
- **Multi‑Symbol** (horizontal scaling)  
- **Multi‑Regime** (contextual scaling)

AMATA becomes a **portfolio‑level autonomous agent**, capable of:

- running **multiple strategies**
- across **multiple symbols**  
- under **multiple market conditions/regimes**
- with **unified global risk**  
- and **isolated local execution** 

This is the foundation of AMATA’s portfolio‑level intelligence.

---

## Why This Architecture Scales

AMATA’s multi‑symbol design enables:

- **cross‑asset diversification**  
- **parallel strategy execution**  
- **regime‑aware symbol selection**  
- **portfolio‑level risk management**  
- **clean, deterministic behaviour**  
- **unlimited symbol expansion**

Because symbols are isolated and global risk is centralized, AMATA can scale from:

- **1 symbol**  
- **to 10 symbols**  
- **to 30 symbols**

…without any architectural changes.

---

## The Multi‑Asset Identity of AMATA

This architecture is what enables AMATA to operate as:

> **An Autonomous Multi‑Asset / Multi‑Strategy Trading Agent — enabled by modular, external configuration and isolated symbol pipelines.**
