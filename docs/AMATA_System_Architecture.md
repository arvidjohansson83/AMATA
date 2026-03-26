# AMATA System Architecture  
Autonomous Multi‑Asset & Multi‑Strategy Trading Agent

The AMATA System Architecture defines how the platform operates internally.  
It describes the core engine, the autonomous subsystems, the execution flow,  
and the design principles that make AMATA modular, extensible and context‑aware.

AMATA is built as a coordinated set of independent components, each with a  
single responsibility and a well‑defined interface. Together, they form a  
fully autonomous, multi‑asset and multi‑strategy trading platform.

---

# 1. Architecture Overview

**AMATA runs a continuous autonomous loop. Each symbol is scanned and evaluated only during its own active market hours — 24/5 for Forex, session‑based for indices and commodities, and 24/7 for crypto.**

All subsystems feed into this loop, providing structure, context, safety,  
strategy evaluation and execution control.

The architecture is designed around:

- **Separation of concerns**  
- **External configuration**  
- **Context‑first execution**  
- **Modular extensibility**  
- **A stable, minimal engine core**

Each subsystem is independent, testable and replaceable.

---

# 2. Core Engine

The Core Engine is responsible for:

- running the autonomous loop  
- loading configuration and platform‑level inputs
- orchestrating all subsystems  
- evaluating market context  
- coordinating strategy execution  
- enforcing safety and policy constraints  

It does **not** contain strategy logic, symbol‑specific rules or thresholds.  
All intelligence is external.

---

# 3. Subsystems

AMATA consists of multiple autonomous subsystems.  
Each subsystem has a single responsibility and communicates through  
structured inputs and outputs.

## 3.1 Regime Engine
Determines the structural state of the market using:

- tsNorm  
- trendScore  
- ADX  
- swingDist  
- ATR buckets  

Outputs:

- regime state  
- volatility state  
- structural context  

## 3.2 Entry Engine
Evaluates whether a strategy is allowed to enter:

- regime‑dependent logic
- session‑aware STOP/LIMIT switching (resolved via policy layer)
- ATR filters
- trendScore filters
- multi‑condition evaluation
- strategy isolation
- policy‑driven entry type resolution (per symbol, per regime, per session)

The Entry Engine itself is session‑agnostic.
It receives a fully resolved entry type (STOP or LIMIT) from the policy system, which determines the correct behaviour based on:

- current regime
- active trading session (Asia, London, US)
- symbol‑specific configuration

This design keeps the Entry Engine minimal and stable while allowing highly adaptive, session‑dependent behaviour through external JSON policies. If no session‑specific entry policy is defined, the policy system falls back to the symbol’s global regime‑based entry type.

---

## 3.3 SL/TSL Engine
Adaptive risk management:

- gridsearch‑optimised SL/TSL  
- regime‑specific behaviour  
- volatility‑aware trailing  
- structure‑based trailing (HH/LL)  
- minimum distance rules  

## 3.4 Safety Engine
The Safety Engine enforces platform‑level execution constraints based on:

- macro‑event timing
- pre/post‑event lock windows
- session windows
- daily ATR exhaustion
- spread‑ATR filters
- user‑configured platform inputs (see **Platform‑Level Inputs**)

## 3.5 Multi‑Strategy System
Supports unlimited strategies:

- isolated strategy modules  
- independent evaluation pipelines  
- shared context from the platform  
- parallel execution  

## 3.6 Multi‑Symbol System
Independent behaviour per symbol:

- symbol profiles  
- symbol‑specific SL/TSL  
- symbol‑specific regime thresholds  
- symbol‑specific news rules  

## 3.7 Logging & Lifecycle Engine
Full lifecycle tracking:

- entry logging  
- regime logging  
- volatility logging  
- SL/TSL evolution  
- exit logging  
- tradeID mapping  
- machine‑readable datasets  

## 3.8 Dashboard Layer
Real‑time monitoring of macro‑event timing and safety windows:

- upcoming news events per currency
- countdown to next event
- pre‑event lock window
- post‑event lock window
- symbol‑to‑currency mapping (implicit through news blocks)
- optional debug text output (if enabled)

---

# 4. Dataflow

AMATA’s dataflow is designed to be deterministic, transparent and modular.

### High‑Level Dataflow

Market Data
↓
Regime Engine → Volatility Engine
↓
Safety Engine
↓
Strategy Modules
↓
Policy Engine
↓
Execution Engine
↓
Logging & Lifecycle Engine
↓
Dashboard

### Configuration Dataflow

JSON Configuration
↓
Core Engine
↓
Subsystems (Regime, Entry, SL/TSL, Safety, Strategy)
↓
Execution

All behaviour is defined externally and consumed by the engine at runtime.

---

# 5. Rationale Behind the Engine Design

The AMATA Engine is built on the principle that **all strategy‑specific and symbol‑specific intelligence must remain external**.  
This ensures that the engine remains stable, predictable and independent of the parameters that define how each symbol behaves.

The design is intentional, and several key motivations drive it.

---

## 5.1 Separation of Concerns

The engine focuses exclusively on:

- reading configuration values  
- evaluating conditions  
- executing trades  
- managing SL and TSL  

It does **not** contain:

- hardcoded thresholds  
- symbol‑specific logic  
- regime definitions  
- ATR multipliers  
- optimisation results  
- strategy rules  
- market‑specific behaviour  

This separation keeps the engine clean, maintainable and future‑proof.

---

## 5.2 Symbol Profiles as External Modules

All symbol‑specific behaviour is defined in dedicated **Symbol Profile** files.  
These profiles act as modular plugins that can be:

- updated  
- replaced  
- optimised  
- extended  

…without modifying the engine code.

This design is ideal for:

- licensing  
- multi‑asset expansion  
- broker‑specific symbol mapping  
- long‑term maintainability  
- safe distribution of symbol‑specific logic  

---

## 5.3 Market Structure‑Based Trailing Logic

The engine uses a structure‑driven approach to trailing stops, following:

- local highs and lows  
- Higher Highs (HH)  
- Lower Lows (LL)  

This allows the system to lock in profit dynamically as the market evolves, without relying on fixed distances or static rules.

The structure detection method is abstracted and controlled through external parameters, enabling symbol‑specific tuning.

---

## 5.4 Regime‑Dependent Behaviour

Different market environments require different rules.  
AMATA supports multiple **market regimes**, and each Symbol Profile defines:

- which regimes are valid  
- which conditions must be met  
- which parameters apply  

The engine simply reads and applies these rules, enabling highly adaptive behaviour without internal complexity.

---

## 5.5 External Optimisation

Stop Loss and Trailing Stop values are optimised through **gridsearch**, where combinations of:

- ATR multipliers  
- SL distances  
- TSL logic  
- regime filters  

…are tested to identify the configuration that yields the highest reward for a constant level of risk.

The engine does not perform optimisation.  
It only consumes the optimised values stored in the Symbol Profiles.

---

## 5.6 No Hardcoded Logic

Because all values are external:

- the engine never needs to be recompiled  
- new symbols can be added instantly  
- existing symbols can be improved safely  
- licensing becomes controlled and secure  
- strategy evolution does not require code changes  

This creates a robust foundation for long‑term scalability.

---

# 6. Summary of the Design Philosophy

The AMATA Engine is intentionally built as a **minimal, stable and data‑driven core**.  
All intelligence, strategy rules and symbol‑specific behaviour live outside the engine in modular configuration files.

This architecture provides:

- maximum flexibility  
- safe licensing  
- easy optimisation  
- clear separation of responsibilities  
- future‑proof scalability  

**AMATA grows through its configuration — not through changes to the engine itself.**

# 7. Summary

The AMATA System Architecture provides a modular, extensible and context‑aware  
foundation for multi‑asset and multi‑strategy trading.  
It separates logic from execution, configuration from code, and strategy from  
environment — enabling long‑term scalability and safe evolution.

---