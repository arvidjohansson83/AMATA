# G3 — AMATA Agent Workflow
**How AMATA Reads, Understands, Decides and Executes in Real Time**

AMATA is not an EA.  
It its name states - it is an **Autonomous Multi-Asset Trading Agent** — a structured, deterministic system that transforms raw market data into synchronized, reproducible trading decisions.

This document describes the **full lifecycle** of the AMATA Agent:  
how it thinks, how it acts, and how it improves.

---

## 1. Overview

The AMATA Agent Workflow is the complete operational pipeline that:

- ingests raw market data  
- extracts behavioural patterns  
- builds strategies  
- optimizes parameters  
- executes trades deterministically  
- logs every action  
- improves itself through feedback  

It is the **central nervous system** of the AMATA platform.

---

## 2. Architecture Layers

AMATA operates through four strictly separated layers.  
Each layer is independent, yet connected through a unified data architecture.

### **Input Layer**

- OHLC data  
- ATR volatility   
- sessions & execution time filters  
- volatility regimes  
- feature normalization  

### **Processing Layer**

- behaviour extraction  
- continuation strength  
- structural integrity  
- ATR geometry  
- symbol profile consumption (profiles are pre‑defined behavioural models)

### **Execution Layer**

- Entry Engine  
- Trend Following Engine  
- Safety Engine (execution‑layer safety rules) 
- SL / TSL / TP logic  
- session rules  
- deterministic state machine  

### **Output Layer**

- logging (bar‑by‑bar agent behaviour)
- state snapshots (agent state at each candle)
- event logs (BOS, trailing, SL/TSL movements)
- backtesting artifacts (identical to live execution)
- reproducibility data (ensures Backtest = Live = Simulation)

---

## 3. Real‑Time Pipeline (M5 Bar‑Close)

On every completed candle, the AMATA Agent performs the following deterministic sequence:

1. **Read Market State**  

   - Regime detection runs continuously  
   - Market structure is classified according to stable behavioural thresholds  
   - Volatility, trend strength, drift, choppiness and expansion states are evaluated  
   - This classification guides all downstream engines

2. **Evaluate News Blocks (Pre / During / Post)** 

   - Symbol‑specific news mapping determines which symbols are affected  
   - **Pre‑news block:** prevents entries before releases that have historically caused volatility  
   - **During‑news block:** halts all entry evaluation during the release  
   - **Post‑news block:** protects against aftershock volatility following the release  
   - Only events listed in the **external symbol‑specific news‑filter JSON files** are considered  
   - These filters are based on historical volatility for each symbol  
   - Unaffected symbols continue trading normally  
   - All news logic is defined externally (weekly news file + symbol-specific filters)

3. **Update Symbol Profile**  

   - Symbol Profiles are derived from repeated analysis of real market data, using both historical backtests and live market observations  
   - Because AMATA’s behavioural metrics are identical in backtest and live environments, these profiles remain stable and reproducible  
   - Profiles contain ATR geometry, volatility behaviour, swing‑distance distributions and threshold definitions  
   - The agent does not generate profiles in real time; it only consumes them as pre‑defined behavioural models
   
4. **Run Engines**  

   - **Entry Engine** — evaluates entry logic  
   - **Trend Following Engine** — evaluates continuation and structure  
   - **Safety Engine (Execution Layer)** — session blocking, spread/slippage blocking, volatility blocking  
   - All engines operate only if the News‑Aware Execution Guard allows execution

5. **Synchronize Strategies**  
6. **Log Behaviour**  
7. **Persist State for Reproducibility**

This pipeline is identical in:

- live trading  
- backtesting  
- simulation  

---

## 4. The 7‑Step Agent Loop

This is the core lifecycle of the AMATA Agent — the full transformation from raw data to continuous improvement.

### **1. Market Data → Features**
Raw OHLC, ATR, spread and session data are normalized into structured features.

### **2. Features → Behaviour**
The Backtesting Pipeline analyzes the market candle‑by‑candle:

- movement  
- trend strength  
- volatility  
- behavioural clusters  

This reveals **what the market is actually doing**.

### **3. Behaviour → Strategy**
Strategy Extraction converts behaviours into:

- entry logic  
- STOP/LIMIT families  
- regime‑specific strategies  

AMATA builds strategies directly from market behaviour.

### **4. Strategy → Precision**
Gridsearch Optimization refines:

- SL  
- TSL  
- trailing step  
- TP levels  

All ATR‑normalized.  
All symbol‑agnostic.

### **5. Precision → Execution**
The Execution Engine applies strategies live:

- entry  
- SL / TSL / TP  
- trailing  
- session rules  

**Backtest = Live.**

### **6. Execution → Logging**
Every trade is logged:

- entry snapshot  
- bar‑by‑bar progression  
- exit summary  

This is the agent’s memory.

### **7. Logging → Improvement**
Logs feed back into the system:

- new clusters  
- new strategies  
- new optimizations  

AMATA is **self‑improving**.

---

## 5. Data Structures

AMATA uses three core data structures to maintain deterministic behaviour and full reproducibility across live trading, backtesting and simulation.

---

### **Symbol Profiles**

Symbol Profiles are AMATA’s pre‑defined behavioural models, derived from repeated analysis of real market data.  
They contain all structural, volatility‑based and regime‑specific parameters required for deterministic execution.

A Symbol Profile includes:

- **Session rules**  

  - earliest entry  
  - latest entry  

- **Volatility constraints**  

  - minimum ATR  
  - ATR geometry  
  - swing‑distance distributions  

- **SL / TSL / TP models (per regime & entry family)**  

  - sl_mult_ATR  
  - tsl_trigger_ATR  
  - tsl_step_ATR  
  - tp_level_ATR  

- **Entry families**  

  - STOP  
  - LIMIT  
  - BLOCK  

- **Boost modules (order‑type separation)**  

  Boosts allow AMATA to activate STOP or LIMIT behaviour under specific conditions.  
  They are not “edge modules” — they are **order‑separation modules** that enable AMATA to run:
  - 1 strategy  
  - 10 strategies  
  - or 100 strategies  
  per symbol, without modifying the core engine.

  A boost module contains:

  - regime association  
  - entryPolicy override (STOP or LIMIT)  
  - regime thresholds

- **Regime thresholds**  

  - LowVol Drift  
  - Premature Entry  
  - Valid  
  - Choppy  
  - Overextended  
  - Neutral  
  - Unknown  

- **Preferred classes**  

  - regime‑specific entry preferences  

Symbol Profiles are stable across environments because AMATA’s behavioural metrics are identical in backtest and live data.

---

### **State Snapshots**

AMATA maintains two types of state snapshots:

#### **1. Internal Agent State (always active, every M5 bar)**  

This state is updated continuously, even when no trade is active.  
It represents AMATA’s real‑time understanding of the market.

It includes:

- ATR  
- volatility state  
- continuation state  
- structure state  
- active regime  
- active entry policy  
- active boost module  
- parameter values

This state is **not shown to the user** and **not logged in the trade journal** unless a trade is active.

#### **2. Trade Snapshots (only when a trade is open)**  

When a trade is opened, AMATA begins logging full trade‑state snapshots.  
These snapshots form the trade’s journal and ensure complete reproducibility.

A trade snapshot contains:

- ATR  
- SL / TSL / TP levels  
- continuation state  
- structure state  
- active regime  
- active entry policy  
- active boost module  
- volatility state  
- parameter values

Trade Snapshots are written to:

- **entry log** (initial state at execution)  
- **progress log** (bar‑by‑bar updates)  
- **exit log** (final state at closure)  

They allow AMATA to reconstruct every trade bar‑by‑bar.

---

### **Event Logs**

Event Logs contain only the data generated during the lifetime of an active trade.  
Each log entry is tied to a unique **TradeID**, ensuring full reproducibility and deterministic reconstruction of the trade.

AMATA produces three event log types:

---

#### **1. Entry Log**

Recorded at the moment a position is opened.

Fields include:

- TradeID  
- Symbol  
- Direction  
- EntryTime  
- EntryPrice  
- SLPrice  
- PipSize  
- Session  
- parameter values at entry
- threshold ranges used for validation  
- regime at entry  
- news_time (if applicable)

---

#### **2. Progress Log**

Recorded on every completed M5 bar while the trade is active.

Fields include:

- TradeID  
- Symbol  
- BarTime  
- High  
- Low  
- Close  
- parameter values

These logs allow AMATA to reconstruct the full bar‑by‑bar evolution of the trade.

---

#### **3. Exit Log**

Recorded when the position is closed.

Fields include:

- TradeID  
- Symbol  
- ExitTime  
- ExitPrice  
- Profit

---

Event Logs contain **only trade‑lifecycle data**.  
All other internal agent behaviour (regime changes, safety blocks, structure events, trailing signals, etc.) is part of AMATA’s internal state and is not included in the trade logs.

---

## 6. Reproducibility

AMATA guarantees **determinism** — the agent behaves identically in live trading, backtesting and simulation because all behavioural data is extracted directly from the markets and can be replicated bar‑by‑bar.

Reproducibility is achieved through:

- **Identical market data** 

  AMATA processes live data using the same metrics and thresholds as in backtesting.  
  Every bar produces identical parameter values.

- **Deterministic state updates**  

  Regime classification, continuation state, structure state and volatility state follow the same logic in all environments.

- **External parameter definitions**  

  All thresholds, parameter values and order‑type rules are stored in Symbol Profiles, ensuring identical behaviour across environments.

- **Deterministic Safety Engine**  

  News blocks, daily ATR blocks, session blocks and spread/slippage blocks operate identically in live and backtest.

- **Identical trade logs**  

  Entry, Progress and Exit logs follow the same schema and are generated using the same deterministic logic.

AMATA’s determinism ensures that **behavioural patterns detected in backtesting are recognized in live trading**, because the underlying data and decision‑logic are identical bar‑by‑bar.

---

## 7. Integration

The AMATA Agent Workflow is the central coordination layer of the platform.  
It connects and synchronizes all major components:

- **Entry Engine**  
  Evaluates entry conditions based on regime, thresholds and order‑type rules.

- **Trend Following Engine**  
  Evaluates continuation strength, structural integrity and trend progression.

- **Safety Engine**  
  Applies symbol‑specific news blocks, daily ATR blocks, session rules and spread protection.

- **Backtesting Pipeline**  
  Extracts behavioural patterns from historical market data using identical metrics as in live trading.

- **Strategy Extraction**  
  Converts repeated behaviours into deterministic strategies and order‑type families.

- **Optimization**  
  Refines SL, TSL, TP and trailing behaviour using ATR‑normalized multipliers.

The Agent Workflow ensures that all components operate deterministically and in parallel across all symbols, enabling true multi‑asset and multi‑strategy execution.

---