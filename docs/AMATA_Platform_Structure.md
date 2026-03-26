# AMATA Platform Documentation Structure  
**Autonomous Multi‑Asset & Multi‑Strategy Trading Agent**


This documentation is organized into modular sections that reflect the architecture of the AMATA Platform.  
Each module can be developed, published, and expanded independently.

---

## 1. Platform Overview
High‑level introduction to AMATA:
- Purpose and philosophy  
- Evolution from MATA  
- Core principles (regime‑aware, volatility‑adaptive, multi‑strategy, multi‑asset)  
- What makes AMATA a platform, not an EA  

---

## 2. System Architecture
Detailed breakdown of the system’s internal structure:
- Core Engine  
- Regime Engine  
- Entry Engine
- SL/TSL Engine  
- Safety Engine  
- Multi-Strategy System
- Multi‑Symbol System  
- Logging & Lifecycle Engine  
- Dashboard Layer 
- Backteting & Analysis Pipeline 

Each component described in terms of:
- Responsibilities  
- Inputs  
- Outputs  
- Interactions  

---

## 3. Configuration System
All JSON‑driven configuration modules:
- Symbol Profiles  
- Entry Policies  
- SL/TSL Policies  
- Regime Thresholds  
- News Block Policies  
- Symbol Mapping  

Explain:
- Structure  
- Purpose  
- How AMATA reads and applies them  

---

## 3.1 Platform‑Level Inputs (User‑Configurable Parameters)
AMATA exposes a set of high‑level inputs that allow users to control platform‑level behaviour such as safety, volatility handling, structure detection and institutional activity windows.  
These parameters do not affect strategy logic — they define the environment in which strategies operate.

### Safety & Execution Controls
- MaxDailyLoss  
- MaxDailyDrawdown  
- MaxLossPerSymbol  
- MaxOpenTrades  
- MaxOpenTradesPerSymbol  
- MaxTradesPerSession  
- BlockAsianSession / BlockLondonSession / BlockUSSession  
- SessionPreOpenBlockMinutes  
- SessionPostOpenBlockMinutes  

### Volatility & Exhaustion Controls
- ATR_Period  
- DailyATR_Threshold  
- SpreadATRMultiplier  

### Structure‑Based SL/TSL Configuration
- ZigZagDepth  
- ZigZagDeviation  
- ZigZagBackstep  

### Institutional Activity Windows
- ForexStartHour / ForexEndHour  
- CommodityStartHour / CommodityEndHour  
- IndexOpenTimes  
- IndexCloseHour  

### Symbol Loading & Mapping
- SymbolsToLoad  
- IndexSymbols  

### Debug Tools
- DebugMode  

---

## 4. Regime Engine
Full specification of AMATA’s regime model:
- Regime definitions (Trendstart, Premature, LowVol Drift, Valid, Choppy, etc.)  
- Indicators used (tsNorm, ADX, trendScore, swingDist, ATR)  
- Volatility buckets  
- State transitions  
- How regimes influence entry, SL/TSL and execution  

---

## 5. Entry Engine
How AMATA evaluates and authorises entries:
- Regime‑dependent entry logic  
- STOP vs LIMIT switching  
- Optional session‑aware entry behaviour
- ATR filters  
- TrendScore filters  
- Multi‑condition evaluation  
- Strategy isolation (multi‑strategy support)  

---

## 6. SL/TSL Engine
Adaptive risk management:
- Gridsearch-optimised SL/TSL  
- Regime‑specific behaviour  
- Volatility‑aware trailing  
- Structure‑based trailing  
- Minimum distance rules  
- Execution flow  

---

## 7. Safety Engine
Macro‑aware execution layer:
- Pre‑ and post‑news blocking  
- Country‑specific filters  
- Symbol‑specific mapping  
- JSON‑driven news rules  
- Integration with Dashboard countdown  
- Enforcement of platform‑level inputs (session windows, ATR exhaustion, spread filters)

---

## 8. Multi‑Strategy System
How AMATA supports unlimited strategies:
- Strategy modules via Symbol Profiles  
- Independent execution pipelines  
- Indicator loading  
- Condition evaluation  
- Strategy isolation  
- Parallel execution  

---

## 9. Multi‑Symbol System
How AMATA handles multiple symbols:
- Family‑based modelling  
- Independent policies per symbol  
- Independent SL/TSL per symbol  
- Independent regime thresholds  
- Independent news filters  

---

## 10. Logging & Lifecycle Engine
Full lifecycle tracking:
- Entry logging  
- Regime state logging  
- Volatility state logging  
- SL/TSL evolution  
- Exit logging  
- TradeID mapping  
- Machine‑readable datasets  

---

## 11. News System
Macro‑event integration:
- HIN‑filter  
- JSON‑driven news files  
- Symbol mapping  
- Blocking logic  
- Dashboard countdown  

---

## 12. Dashboard
Real‑time monitoring of macro‑event timing and safety windows:

- upcoming news events per currency
- countdown to next event
- pre‑event lock window
- post‑event lock window
- symbol‑to‑currency mapping (implicit through news blocks)
- optional debug text output (if DebugMode is enabled)

---

## 13. Backtesting & Analysis Pipeline
AMATA includes a full analysis pipeline for designing and validating new strategies:

- **User‑defined movement logging via dedicated EA**
- **CSV‑based data export**
- **Gridsearch‑optimised SL/TSL for custom movement profiles**
- STOP/LIMIT edge analysis
- Regime distribution analysis
- Volatility profiling

---

## 14. Dataflow
System‑wide dataflow diagrams:
- How data moves through AMATA  
- Engine → Safety → Strategy → SL/TSL → Logging  
- JSON → Engine → Execution  
- Regime → Entry → SL/TSL → Exit  

---

## 15. Examples
Practical examples:
- Example Symbol Profiles  
- Example Regime Thresholds  
- Example SL/TSL Policies  
- Example News Policies  
- Example Strategy Modules  

---

## 16. Glossary
Definitions of all key concepts:
- tsNorm  
- trendScore  
- swingDist  
- ATR buckets  
- Regime states  
- STOP/LIMIT logic  
- Volatility terms  
- Policy terms  

---

## 17. Release Notes
Version history and updates:
- New modules  
- Improvements  
- Bug fixes  
- Architecture changes  

---

## 18. Roadmap
Future development:
- Planned modules  
- Planned features  
- Long‑term vision  

