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

## 7. Stop Loss Configuration

AMATA uses a **unified, symbol‑agnostic ATR‑based Stop Loss model** across all symbols and strategies.  
This creates a flexible, edge‑aware execution system suitable for multi‑strategy orchestration.

Profiles may define:

- ATR multipliers  
- Regime‑specific ATR adjustments  
- Entry‑type‑specific ATR adjustments  

The AMATA Core Engine applies the SL configuration at entry.

---

## 8. Trailing Stop Configuration

Trailing Stop logic is also ATR‑based and fully externalized:

- ATR‑based trailing  
- Step trailing  
- Hybrid ATR models  
- Minimum distance rules  

The engine updates the SL dynamically based on the profile’s rules.

---

## 9. SL/TSL System  
### Layered, Strategy‑Specific Stop Logic

AMATA supports a **layered SL/TSL override system**, where Stop Loss and Trailing Stop rules can be defined at multiple levels:

- **default SL/TSL**  
- **regime‑specific SL/TSL**  
- **entry‑type‑specific SL/TSL**  
- **strategy‑specific overrides**  

AMATA loads these layers in order:

1. default  
2. regime override  
3. entry‑type override  
4. strategy override  

This creates a flexible, edge‑aware execution system suitable for **multi‑strategy orchestration**.

---

## 10. Boost System  
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
- any SL/TSL profile  

without modifying the AMATA Core Engine.

This design transforms the AMATA Platform into a **unified, scalable, and fully customizable trading engine** capable of hosting an unlimited number of strategies through external configuration.

---