# Symbol Profile Specification  
### Modular Strategy Definition for the AMATA Trading Agent


A **Symbol Profile** is the core configuration unit that defines how AMATA trades a specific symbol or executes a specific strategy.  
Profiles act as **modular strategy plugins**, allowing the user to design, combine, and deploy any number of strategies without modifying the AMATA Core Engine.

AMATA supports both predefined strategies and fully custom strategies.  
Advanced users may define any combination of conditions, indicators, timeframes, filters, or market regimes.  
The engine does not impose any limitations — it simply executes the logic defined in the profile.

By adding a new Symbol Profile, the user effectively adds a new strategy to the system.  
AMATA can therefore operate as a single‑strategy EA or as a multi‑strategy platform capable of running dozens or even hundreds of strategies in parallel.

AMATA supports:

- predefined strategy families (trend, microtrend, breakout, range, mean reversion)  
- fully custom strategies  
- multi‑strategy execution  
- regime‑aware logic  
- entry‑type separation (STOP/LIMIT)  
- layered SL/TSL override logic per strategy  
- session‑aware entry policies  
- unlimited strategy expansion  

Because all strategy logic is external, AMATA becomes a **universal trading engine** capable of running:

- 1 strategy  
- 10 strategies  
- 100 strategies  

simultaneously, each defined by its own profile.

---

## 1. Purpose of Symbol Profiles

Symbol Profiles allow the user to define:

- Entry conditions  
- Market regime filters  
- Stop Loss and Trailing Stop logic 
- Take Profit level (regime‑aware, entry‑type‑aware) 
- Indicator‑based conditions  
- Time‑based filters  
- Trend, range, breakout or pullback logic  
- Multi‑condition combinations  
- Custom strategy behavior  

The engine does not impose any limitations — it simply evaluates the conditions defined in the profile.

---

## 2. Profile Structure Overview

A Symbol Profile typically contains:

- **General Settings**  
- **Entry Conditions**  
- **Market Regime Definitions**  
- **Stop Loss Configuration**  
- **Trailing Stop Configuration**  
- **Take Profit Configuration**
- **Indicator Parameters**  
- **Time‑Based Filters**  
- **Strategy‑Specific Rules**  

The structure is flexible and can be extended as needed.

---

## 3. General Settings

Defines basic operational parameters:

- Symbol name  
- Timeframes used  
- Activation flags  
- Execution mode  
- Dependencies on other modules  

These settings tell the platform how and when the strategy should operate.

---

## 4. Entry Conditions

Entry conditions are fully customizable and may include:

- Trend‑following logic  
- Range‑trading logic  
- Breakout conditions  
- Indicator‑based signals (EMA, RSI, MACD, etc.)  
- Price action patterns  
- Multi‑condition combinations  
- Custom filters  

Supported condition types:

- Crossovers  
- Threshold checks  
- Boolean combinations (AND/OR)  
- Structure‑based triggers  
- Volatility filters  

The engine does not interpret indicators — it only evaluates the conditions defined in the profile.

---

## 5. Market Regime Filters

Profiles may define multiple **market regimes**, such as:

- Trending  
- Ranging  
- Volatility expansion  
- Low‑volatility consolidation  

Each regime includes:

- Activation rules  
- Indicator thresholds  
- Volatility conditions  
- Structure‑based filters  

AMATA evaluates the current regime and applies the appropriate rules.

---

## 6. Entry Policy System  
### Session‑Aware and Regime‑Aware Entry Types

AMATA supports:

- STOP entries  
- LIMIT entries  
- Session‑aware entry selection  
- Regime‑based entry selection  
- Fallback logic  

If a symbol does not define session‑specific behavior, AMATA automatically falls back to the global regime‑based entry type.

This allows:

- LIMIT‑only symbols  
- STOP‑only symbols  
- STOP/LIMIT hybrid symbols  
- Session‑dependent entry types  
- Strategy‑specific entry types  

---

## 7. AMATA Unified SL/TSL/TP System  
### ATR‑Driven, Regime‑Aware, Entry‑Type‑Aware Risk Model

AMATA uses a unified ATR‑based risk model where Stop Loss, Trailing Stop Loss (including TSL‑Step), and Take Profit levels are all derived from the same volatility‑aligned multiplier system.  
This ensures that all risk parameters scale consistently with the symbol’s natural behaviour and remain coherent across regimes, entry types, and strategy overrides.

All components are:

- ATR‑driven  
- symbol‑specific  
- regime‑aware  
- entry‑type‑aware  
- empirically calibrated  
- externally defined in the Symbol Profile

### Why a Unified Model  
The unified SL/TSL/TP system ensures:

- consistent risk scaling  
- coherent payoff structure  
- stable expectancy across regimes  
- balanced STOP/LIMIT behaviour  
- predictable trade distribution  
- clean multi‑strategy orchestration  

### STOP vs LIMIT  
AMATA separates SL/TSL/TP logic based on the selected entry type:

- **LIMIT entries**  
  Represent the symbol’s *default* behaviour.  
  LIMIT entries operate across the full volatility spectrum of the symbol and use SL/TSL/TP multipliers calibrated to the symbol’s natural volatility profile.

- **STOP entries**  
  Act as a momentum-aligned "sniper" mode.  
  STOP entries are only enabled when the symbol’s historical data shows a clear and consistent separation between STOP‑based and LIMIT‑based entry characteristics.  
  When this separation exists, STOP entries use their own SL/TSL/TP multipliers aligned with momentum‑driven volatility conditions.

### Volatility‑Aligned Multipliers  
All ATR multipliers are derived from each symbol’s **natural volatility characteristics**, ensuring that risk parameters scale organically with the symbol’s behaviour rather than relying on fixed or generic distances.

### Layer Loading Order  
AMATA loads SL/TSL/TP rules in the following order:

1. regime‑specific rules  
2. entry‑type‑specific rules (STOP or LIMIT)  
3. strategy‑specific overrides  

This layered structure creates a flexible, volatility‑aware risk system suitable for **multi‑strategy orchestration**, where each strategy can define its own behaviour while still operating within a unified execution framework.


---

## 8. Stop Loss Configuration

AMATA applies Stop Loss levels using the unified ATR‑based risk model.  
Each symbol profile may define:

- ATR multipliers  
- regime‑specific SL adjustments  
- entry‑type‑specific SL adjustments  

The SL is applied at entry and remains active until Trailing Stop logic takes over.

---

## 9. Trailing Stop Configuration

Trailing Stop logic is fully externalized and derived from the unified ATR‑based system.  
Profiles may define:

- ATR‑based trailing  
- step‑based trailing (TSL‑Step)  
- hybrid ATR/step models  
- minimum distance rules  

The engine updates the SL dynamically based on the profile’s rules and the symbol’s volatility conditions.

---

## 10. Take Profit Configuration  
### Regime‑Aware, Entry‑Type‑Aware TP Levels

AMATA uses an externalized Take Profit system where each symbol defines:

- TP multipliers per market regime  
- TP multipliers per entry type (STOP/LIMIT)  
- TP ranges derived from empirical gridsearch  
- TP behaviour aligned with the symbol’s volatility profile  

These TP levels are calibrated per symbol to reflect:

- volatility characteristics  
- regime‑specific behaviour  
- STOP/LIMIT separation  
- historical payoff tendencies  

---

## 11. Boost System  
### Extracting Multiple Strategies From a Single Symbol

Boosts are optional micro‑filters that activate only under specific structural or volatility conditions.  
Their primary purpose is to **separate STOP and LIMIT strategies within the same symbol**, enabling multiple strategies to coexist inside the same regime without overlapping entries.

This allows a single symbol to generate multiple strategies by activating different entry paths under different structural conditions. 
It is one of the key mechanisms that allows AMATA to extract multiple independent strategies from a single symbol.

Boosts enable:

- STOP/LIMIT separation  
- multiple strategies within the same symbol  
- multiple strategies within the same regime  
- clean, non‑overlapping entry logic  
- micro‑edge activation when conditions align

This enables **multiple strategies within the same symbol and regime**, as long as their entry conditions do not overlap.

The Boost System unlocks additional strategies whenever a symbol naturally exhibits STOP/LIMIT divergence, allowing AMATA to scale horizontally without modifying the core engine.

### 🔗 Full Boost Architecture Documentation

For a complete architectural explanation of how Boosts operate inside the AMATA Platform — including activation logic, entry‑policy modification, and multi‑strategy orchestration — see:
[Boost Architecture](./C2_Boost_Architecture.md)

---

## 11. Time‑Based Filters

Profiles may include:

- Session filters  
- Time‑of‑day restrictions  

These filters allow precise control over when the strategy is allowed to trade.

---

## 12. Multi‑Strategy Integration

Because each strategy is defined by its own profile, AMATA can run:

- Multiple strategies on the same symbol  
- Multiple strategies across different symbols  
- Multiple strategies with different regimes  
- Multiple strategies with different SL/TSL profiles  

All in parallel, all isolated, all independent.

This makes AMATA a **true multi‑strategy platform**.

---

## 13. Adding a New Strategy (Quick Guide)

- Create a new Symbol Profile
- Define entry conditions
- Define regime filters
- Define SL/TSL rules
- Add Boost filters (Optional)
- Enable the profile

The AMATA Core Engine automatically incorporates the new strategy.

---

## 14. Summary

Symbol Profiles are the foundation of AMATA’s modular architecture.  
They allow the user to define:

- any strategy  
- any logic  
- any indicator  
- any regime  
- any SL/TSL/TP profile  

without modifying the AMATA Core Engine.

This design transforms the AMATA Platform into a **unified, scalable, and fully customizable trading engine** capable of hosting an unlimited number of strategies through external configuration.

---