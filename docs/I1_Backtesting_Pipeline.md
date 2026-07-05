# AMATA Backtesting Pipeline
### How AMATA Reconstructs Market Behaviour Candle‑by‑Candle

---

## **Purpose**
The **Backtesting Pipeline** is AMATA’s engine for analysing raw market behaviour.  
Instead of testing predefined strategies, AMATA measures the market itself — candle by candle — and extracts the natural volatility, structure and movement patterns of each symbol.

This pipeline is the foundation for:

- **strategy discovery**  
- **regime‑specific behaviour modelling**  
- **symbol‑specific optimization** 
- **volatility‑normalised analysis**  
- **data‑driven strategy creation**  

AMATA doesn’t guess.  
AMATA measures.

---

## 🔍 **Behaviour‑First Backtesting**
Traditional backtesting answers:

> “Does this strategy work?”

AMATA’s pipeline answers:

> “What does the market *actually do*?”

To achieve this, AMATA processes every candle in the dataset and extracts:

- trend‑following parameters  
- volatility behaviour  
- swing structure  
- normalized trend strength  
- symbol‑specific movement patterns  

**AMATA learns each symbol’s behavioural fingerprint — fully data‑driven.**

---

## 🧪 **Behaviour-Driven Exploration**
AMATA’s backtesting pipeline is designed to analyse market behaviour at scale — fully autonomously.

Instead of relying on predefined assumptions, the system explores the data space itself:

- which **swings** tend to repeat
- which **trend behaviours** persist across regimes
- which **volatility expansions** lead to continuation
- which **structural patterns** form reliable edges

AMATA then performs a systematic, ML‑style exploration:

- scans raw historical data
- clusters similar behaviours
- identifies recurring structures
- evaluates thousands of parameter combinations
- extracts statistically meaningful strategy candidates

The process is **data‑driven, deterministic**, and **fully internal**.
If the market exhibits a pattern, AMATA will detect it.

---

## 🧩 **Different Market States Detector**
AMATA treats STOP and LIMIT entries as **different behavioural patterns**.

### **STOP‑entries represent:**
- momentum  
- continuation  
- breakout behaviour  

### **LIMIT‑entries represent:**
- mean reversion  
- pullbacks  
- liquidity grabs  

These behaviours form **distinct clusters** in the data.  
AMATA uses these clusters to create **separate strategies per order type and per regime**.

This reflects the behavioural segmentation commonly applied in institutional market models.

---

⚙️ **How the Pipeline Processes Every Candle**
AMATA’s Backtesting Pipeline is engineered for **maximum analytical efficiency**.

Instead of analysing trades, it **reconstructs market behaviour itself** — deterministically and candle‑by‑candle.

For every candle, the pipeline:

- reads the raw OHLC data
- extracts volatility and structural information
- reconstructs **[swings and micro‑movements](./B1_Regime_Engine.md)**
- measures volatility expansions
- records structural shifts
- stores all extracted features in a unified data model

This creates a **perfect replay** of the market’s behaviour, without any strategy assumptions.

**The pipeline is designed to**:

- process millions of candles with minimal overhead
- rebuild every movement exactly as it happened
- extract behaviour patterns with zero bias
- normalise all measurements through ATR
- maintain deterministic output for reproducibility

This is why AMATA can analyse any symbol, any timeframe, and any market condition — using the same universal pipeline.

---

## 🚀 **Why This Matters**
The Backtesting Pipeline is not about validating strategies.  
It’s about **discovering them**.

It enables:

- **strategy extraction** 
- **regime‑specific modelling**  
- **symbol‑specific tuning**  
- **volatility‑normalised optimization**  
- **data‑driven strategy creation**  

AMATA doesn’t just simulate the market.  
AMATA learns the natural structure of every market:

- natural volatility
- movement patterns of each symbol

...and then learns to detect these behaviours in **live market conditions**.

AMATA doesn’t search for strategies.
**AMATA models each symbol as an independent behavioural system — a unique market with its own statistical properties, volatility dynamics and structural patterns.**.

---



