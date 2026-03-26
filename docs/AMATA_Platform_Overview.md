# AMATA Platform Overview  
Autonomous Multi‑Asset & Multi‑Strategy Trading Agent

AMATA is a fully autonomous trading platform designed to operate across multiple symbols, multiple strategies and multiple market regimes.  
It provides a modular, extensible and context‑aware execution environment where strategies run inside a unified agent rather than as separate EAs.

AMATA is not a strategy.  
It is a **platform** for running strategies.

---

## 1. Purpose and Philosophy

AMATA is built around a simple principle:

**A strategy should only execute when the environment supports its edge.**

To achieve this, AMATA continuously evaluates:

- market structure  
- volatility state  
- macro‑event risk  
- symbol‑specific behaviour  
- strategy‑specific conditions  

By separating timing, safety and context from the strategy layer, AMATA allows strategies to focus solely on their logic while the platform manages the environment around them.

---

## 2. Evolution from MATA

MATA introduced:

- deterministic session‑based execution  
- structural pattern recognition  
- volatility‑aware behaviour  
- stable, rule‑driven timing  

But MATA lacked:

- regime awareness  
- macro‑event filtering  
- multi‑strategy support  
- multi‑symbol architecture  
- adaptive execution  
- modular configuration  

AMATA is the next step — a platform that understands **context**, not just structure.

---

## 3. What AMATA Is

AMATA is a modular, extensible and autonomous trading platform that provides:

- regime‑aware market structure analysis  
- volatility‑adaptive execution  
- macro‑aware safety and news filtering  
- multi‑strategy execution inside a single agent  
- multi‑symbol support with independent policies  
- JSON‑driven configuration for all behaviours  
- full lifecycle logging for analysis and optimisation  
- a real‑time dashboard for monitoring and debugging  

The platform is designed to scale horizontally — new strategies, symbols and behaviours can be added without modifying the core engine.

---

## 4. How the Modules Fit Together (High‑Level Architecture)

AMATA is built as a coordinated system of autonomous subsystems.  
Each module has a single responsibility and communicates through well‑defined interfaces.

### Execution Flow Overview

- **Agent Core**  
  Runs a continuous autonomous loop, scanning and evaluating each symbol only during its own active market hours.

- **Symbol Profiles**  
  Provide symbol‑specific behaviour, thresholds and policies.

- **Regime Engine**  
  Determines structural context (trendstart, drift, choppy, etc.).

- **Volatility Engine**  
  Classifies volatility state and influences SL/TSL and entry logic.

- **Safety Engine**  
  Validates macro‑event risk, volatility shocks and structural instability.

- **Strategy Modules**  
  Evaluate their logic using the current context provided by AMATA.

- **Policy Engine**  
  Authorises or rejects execution based on platform‑level rules.

- **Execution Engine**  
  Places, modifies and manages orders.

- **Logging & Lifecycle Engine**  
  Records every state transition, decision and trade event.

- **Dashboard Layer**  
  Visualises the current state of the agent in real time.

This separation of concerns is what makes AMATA a platform rather than a monolithic EA.

---

## 5. What the Platform Makes Possible

AMATA enables capabilities that are not feasible in traditional EA‑based workflows:

- unlimited strategies inside one agent  
- unlimited symbols with independent logic  
- regime‑aware and volatility‑adaptive execution 
- optional session‑aware entry behaviour 
- macro‑aware safety without manual intervention  
- strategy isolation (strategies cannot interfere with each other)  
- modular configuration without recompilation  
- continuous data‑driven optimisation  
- full lifecycle logging for analysis and ML pipelines  

AMATA is designed to evolve over time without architectural changes.

---

## 6. What the Platform Actually Contains

To illustrate the scale and maturity of the architecture, AMATA currently consists of:

- **15 autonomous subsystems**  
- **40+ internal functions**  
- **5 analytical layers**  
- **3 risk engines**  
- **3 policy systems**  
- **1 ML‑ready optimisation pipeline**  
- **1 multi‑symbol execution architecture**  
- **1 multi‑strategy execution architecture**  
- **1 state machine governing strategy lifecycle**  
- **1 macro‑aware news engine**  
- **1 real‑time dashboard**  
- **1 full lifecycle logging engine**  
- **1 dataflow and backtesting pipeline**

These components form the foundation for all future modules in the AMATA documentation.

---

## 7. What Is Implemented Today

The current version of AMATA includes:

- Agent Core  
- Regime Engine  
- Volatility Engine  
- Entry Engine  
- SL/TSL Engine  
- Safety Engine  
- Multi‑Strategy System  
- Multi‑Symbol System  
- JSON‑driven configuration system  
- Dashboard layer  
- Full lifecycle logging  
- Backtesting & analysis pipeline  

All modules are operational and integrated.

---

## 8. What Is Extensible

AMATA is built for long‑term evolution.  
The following components are fully extensible:

- new strategies  
- new symbols  
- new regime definitions  
- new SL/TSL behaviours  
- new safety rules  
- new policy modules  
- new analytical layers  
- new dashboard components  
- new dataflow integrations  

The platform grows through its configuration — not through changes to the engine itself.

---

## 9. Architectural Philosophy

AMATA follows three core architectural principles:

### 1. Separation of Concerns  
Strategies focus on logic.  
AMATA handles timing, safety, context and execution.

### 2. Policy‑Driven Behaviour  
All behaviour is defined through JSON policies, not code changes.

### 3. Context‑First Execution  
Execution only occurs when the environment supports the edge.
