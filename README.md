# AMATA — Autonomous Multi‑Asset & Multi‑Strategy Trading Agent
## A fully autonomous, regime‑aware and volatility‑adaptive trading agent built for real market conditions.

[▶ Watch AMATA Initialization Video](https://youtu.be/xdFQfwbHBqU)

[![AMATA Initialization Video](https://img.shields.io/badge/▶_Watch_Initialization_Video-000000?style=for-the-badge&logo=video)](https://youtu.be/xdFQfwbHBqU)

AMATA is the evolution of my session‑based architecture MATA.  
Where MATA focused on structural patterns, volatility behaviour and deterministic execution,  
AMATA adds the missing dimension: **context**.

---

## 🚀 Core principles
- Continuous market structure analysis during each symbol’s active market hours
- Regime‑based market structure analysis & volatility state modelling
- Macro‑aware safety layer with automatic execution halts  
- Multi‑Asset & Multi‑Strategy architecture
- Fully autonomous, policy‑driven and extensible design

AMATA is not a strategy — it is a **platform** for running strategies.

---

## 🧠 Why AMATA Exists
Running [MATA](https://github.com/arvidjohansson83/MATA) live revealed a key limitation:  
**structure without context is not enough.**

MATA executed every day at fixed times, regardless of regime, volatility or macro events.  
AMATA is built to understand when the environment supports the edge — and when it doesn’t.

---

## 🛡️ Safety‑First Execution

AMATA includes a fully autonomous, macro‑aware safety layer that:

- identifies meaningful macro events  
- applies pre‑ and post‑event lock windows  
- filters out irrelevant noise  
- blocks execution during structural instability  
- ensures strategies only run when the environment is safe  

This removes the need for manual decision‑making around news and volatility shocks.

---

## 📈 Adaptive strategy refinement

AMATA logs every trade with:

- regime  
- volatility state  
- structure conditions  
- execution context  

This creates a continuous feedback loop for data‑driven optimisation.

AMATA doesn’t just execute strategies — **it learns from them**.

---

## 🧩 Why AMATA is the Last EA I will Ever build

AMATA is not an EA — it is the platform that replaces the need to never again build another one. 

AMATA is fully autonomous — strategies run themselves, and the platform handles timing, safety and execution without manual intervention.

Instead of creating a new EA for every idea, every strategy or every symbol,  
AMATA allows me to run **unlimited strategies**, across **unlimited symbols**,  
all inside a single autonomous agent.

New strategies are added as Symbol Profiles.  
New behaviours are added as Policies.  
No recompilation. No new EA. No new codebase.

AMATA is the last EA I will ever build —  
because from here on, I only evolve strategies, not software.

---

## 📚 Documentation Structure (A–J)

All documentation is organised into modular sections that reflect AMATA’s architecture.

## **A — Platform Architecture**
- [A1_Platform_Overview.md](docs/A1_Platform_Overview.md)  
- [A2_System_Architecture.md](docs/A2_System_Architecture.md)  
- [A3_Platform_Configurations.md](docs/A3_Platform_Configurations.md)  
- [A4_Platform_Structure.md](docs/A4_Platform_Structure.md)  

## **B — Market Understanding Layer**
- [B1_Regime_Engine.md](docs/B1_Regime_Engine.md)  
- [B2_Volatility_Engine.md](docs/B2_Volatility_Engine.md)  

## **C — Symbol Intelligence Layer**
- [C1_Symbol_Profiles.md](docs/C1_Symbol_Profiles.md)  
- [C2_Boost_Architecture.md](docs/C2_Boost_Architecture.md)  

## **D — Strategy & Multi‑Strategy Layer**
- [D1_Strategy_Modules.md](docs/D1_Strategy_Modules.md)  
- [D2_Multi_Strategy_Architecture.md](docs/D2_Multi_Strategy_Architecture.md)  
- [D3_Multi_Symbol_Architecture.md](docs/D3_Multi_Symbol_Architecture.md)  

## **E — Safety & Macro Layer**
- [E1_Safety_Engine.md](docs/E1_Safety_Engine.md)   

## **F — Entry & Execution Layer**
- [F1_Entry_Engine.md](docs/F1_Entry_Engine.md)  
- [F2_Execution_Engine.md](docs/F2_Execution_Engine.md)  

## **G — Risk & Limits Layer**
- [G1_Risk_Model.md](docs/G1_Risk_Model.md)  
- [G2_Trend_Following_Engine.md](docs/G2_Trend_Following_Engine.md)  
- [G3_Agent_Workflow.md](docs/G3_Agent_Workflow.md)

## **H — System Infrastructure**
- [H1_State_Machine.md](docs/H1_State_Machine.md)  
- [H2_Logging_Engine.md](docs/H2_Logging_Engine.md)  
- [H3_Dashboard.md](docs/H3_Dashboard.md)  
- [H4_Dataflow.md](docs/H4_Dataflow.md)  

## **I — Development & Analysis**
- [I1_Backtesting_Pipeline.md](docs/I1_Backtesting_Pipeline.md)  
- [I2_Strategy_Extraction.md](docs/I2_Strategy_Extraction.md)  
- [I3_Gridsearch_Optimization.md](docs/I3_Gridsearch_Optimization.md)  

## **J — Meta**
- [J1_Glossary.md](docs/J1_Glossary.md)  
- [J2_Roadmap.md](docs/J2_Roadmap.md)  
- [J3_Documentation_Structure.md](docs/J3_Documentation_Structure.md)  

---

# 🧪 Examples

Examples related to specific modules can be found in:

- `examples/B1_example_regime_detection.md`  
- `examples/B1_example_live_regime_logging.md`  
- `examples/A3_example_initializing.md`  

---

# 📌 Status

AMATA is under active development and will be expanded continuously.  
New modules and updated documentation are added as the platform evolves.
