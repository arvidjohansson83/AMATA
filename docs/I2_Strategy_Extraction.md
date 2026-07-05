# **Strategy Extraction**
### How AMATA Transforms Market Behaviour Into Tradeable Strategies

---

## **Purpose**
The **Strategy Extraction** module converts AMATA’s behavioural analysis into fully defined, rule‑based trading strategies.

Where the **[Backtesting Pipeline](./I1_Backtesting_Pipeline.md)** reconstructs each symbol candle‑by‑candle, Strategy Extraction identifies:

- repeatable behaviours  
- structural patterns  
- volatility‑adaptive tendencies  
- regime‑specific opportunities  

…and transforms them into **strategy blueprints** that AMATA can execute live.

AMATA doesn’t invent strategies.  
AMATA discovers them.

---

## 🔍 **From Behaviour → Strategy**
Strategy Extraction begins with the behavioural clusters produced by the Backtesting Pipeline:

- continuation patterns  
- reversal structures  
- volatility expansions  
- trend‑strength signatures  
- symbol‑specific movement tendencies  

Each cluster represents a **repeatable market behaviour**.  
Strategy Extraction turns these behaviours into structured, deterministic strategy logic.

---

## 🧪 **Behaviour-Defined → Machine-Extracted Strategy**
AMATA autonomously analyses the market behaviours the system is designed to understand:

- repeating swing structures
- trend‑strength conditions
- volatility phases
- continuation & reversal tendencies

These behaviours are observable, measurable, repeatable.

AMATA then:

- isolates the behaviour
- validates its statistical repeatability
- identifies structural prerequisites
- converts it into a strategy blueprint

Every strategy in AMATA is born from market behaviour — not from human imagination.

---

🔎 **Selective Behaviour Extraction**
AMATA analyses every candle — but only statistically repeatable behaviours become strategies.

This selective extraction makes AMATA’s strategies:

- robust
- repeatable
- behaviour‑true
- data‑grounded

---

## 🧩 **STOP vs LIMIT = Separate Strategy Families**
STOP and LIMIT entries represent **different market states** and therefore produce different strategy families.

### **STOP‑based strategies**
- momentum continuation  
- breakout behaviour  
- volatility expansion  

### **LIMIT‑based strategies**
- pullbacks  
- mean reversion  
- liquidity‑driven reversals  

AMATA extracts **separate strategy families per:**

- order type  
- regime  
- symbol  

This ensures that each strategy is aligned with the underlying market behaviour.

---

## ⚙️ **Strategy Construction Pipeline**
Once a behaviour is identified, AMATA constructs the strategy in three stages:

### **1️⃣ Behaviour Definition**
The extracted cluster becomes the “core behaviour” the strategy is built around.

AMATA defines:

- direction  
- volatility context  
- structural prerequisites  
- regime conditions  

This determines *when* the strategy should act.

### **2️⃣ Entry Logic Formation**
AMATA formalises the entry logic by analysing:

- behaviour frequency  
- behaviour consistency  
- behaviour directionality  
- behaviour volatility profile  

This produces a deterministic entry rule.

### **3️⃣ Risk & Reward Modelling**
AMATA then models the performance profile:

- **Stop Loss placement**  
- **Trailing Stop Loss behaviour**  
- **Trailing Step aggressiveness**  
- **Take Profit levels** based on natural movement length  

This defines *how* the strategy behaves once active.

---

## 📏 **ATR‑Normalised Strategy Profiles**
All extracted strategies are **ATR‑normalised**, meaning:

- strategies are symbol‑agnostic  
- volatility differences are absorbed  
- behaviour is measured in multiples, not pips  
- strategies scale across all instruments  

A strategy extracted on EURUSD can be applied to GOLD or NASDAQ  
because the behaviour is **normalised**, not hard‑coded.

---

## 🔄 **Integration With Backtesting Pipeline**
Strategy Extraction is directly connected to:

- **[Backtesting Pipeline](./I1_Backtesting_Pipeline.md)**
- **[Logging Engine](./H2_Logging_Engine.md)**
- **[Execution Engine](./F2_Execution_Engine.md)** 
- **[Regime Engine](./B1_Regime_Engine.md)**  

This ensures:

- deterministic behaviour  
- reproducible results  
- identical logic between backtest and live  
- seamless deployment of extracted strategies  

---

## 🚀 **Why Strategy Extraction Matters**
Strategy Extraction enables AMATA to:

- build strategies from real market behaviour  
- avoid curve‑fitting  
- adapt to symbol‑specific tendencies  
- create regime‑aware logic  
- scale across multiple assets  
- generate robust, data‑driven edge  

AMATA doesn’t guess.  
AMATA measures.  
AMATA extracts.  
AMATA evolves.

