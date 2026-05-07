# AMATA Execution Engine
### Core Execution Layer of the Autonomous Multi‑Asset & Multi Strategy Trading Agent

The **AMATA Execution Engine** is the central component that transforms market context, symbol‑specific configuration, and strategy‑level edge into safe, deterministic, and conflict‑free trade execution.

It is designed as a **modular**, **data‑driven**, and **fully externalized** execution layer.  
All symbol behavior, thresholds, SL/TSL logic, and regime conditions are defined in external configuration files — not in code — enabling a **scalable, maintainable, and licensing‑friendly architecture.**

The engine itself contains **no embedded strategy rules**.  
All entry logic is **fully data‑driven**.

---

## 1. Architectural Overview

The Execution Engine is responsible for:

- assembling the full execution context  
- validating all permission layers  
- executing trades only when all independent conditions agree  
- calculating position size based on the user-defined *risk per trade* (not symbol-specific)
- enforcing user‑defined risk limits:  
  - **MaxOpenTrades**  
  - **MaxOpenTradesPerSymbol**  
  - **MaxTradesPerSession**  
  - **MaxDailyLoss**  
  - **MaxDailyDrawdown**  
  - **MaxLossPerSymbol**  
- placing Stop Loss (SL)
- placing Take Profit (TP)
- moving SL to breakeven when instructed (BE)
- managing Trailing Stop Loss (TSL) from breakeven  
- following market structure  
- integrating with Safety and News Engines  
- routing strategy signals through a deterministic pipeline  

The engine contains **no symbol‑specific logic**.  
All behavior is driven by external profiles.

---

## 2. Data‑Driven Configuration (Plugin Architecture)

Each symbol has its own external profile defining:

- SL/TSL/TP multipliers  
- ATR‑based thresholds  
- structural filters  
- regime filters  
- volatility constraints  
- default LIMIT parameters  
- boost STOP parameters
- strategy permissions 
- preferred classes (regimes allowed for trading) 

This plugin‑based design ensures:

- **scalability**  
- **maintainability**  
- **broker‑agnostic mapping**  
- **safe licensing**  
- **rapid optimization**  
- **future‑proof expansion**  

Creating or modifying a symbol requires **no code changes** — only profile edits.

---

## 3. Execution Context Assembly

Before any strategy is allowed to activate, AMATA assembles a complete execution context:

- **current regime**  
- **volatility state**  
- **market structure (HH/LL)**  
- **symbol‑specific thresholds**  
- **Safety Engine status**  
- **News Engine status**  
- **spread & slippage constraints**  
- **session filters**  
- **user-defined risk limits**

This ensures that strategies operate on a **fully prepared, validated environment**.

---

## 4. Multi‑Layer Execution Permissions
### Safety → Regime → Symbol Profile → Strategy Module → Execution Layer

AMATA executes a trade **only when all layers independently agree**.

```
Safety Engine
   ↓
Regime Engine
   ↓
Symbol Profile
   ↓
Strategy Module
   ↓
Execution Layer
```

### Layer 1 — Safety Engine 
[Safety Engine Specification](./AMATA_Safety_Engine.md)

The environment must be safe:

- no high‑impact news  
- no session blocks  
- no ATR exhaustion  
- no volatility spikes 
- no spread violations 

### Layer 2 — Regime Engine 
[Regime Engine Specification](./AMATA_Regime_Engine.md)

The current regime must be included in the symbolprofile’s preferred_classes.

### Layer 3 — Symbol Profile  
[Symbol Profile Specification](./AMATA_Symbol_Profiles.md)

Symbol‑specific thresholds must be satisfied:

- ATR bands  
- volatility filters  
- structural constraints  
- regime‑specific parameters  
- default LIMIT min/max thresholds  
- boost STOP min/max thresholds

Boost STOP parameters are only included when the symbol’s data points show a clear statistical separation between LIMIT and STOP entry signatures. If no separation exists, no boost block is created and the engine uses default thresholds only.

### Layer 4 — Strategy Module  
The strategy must validate its own edge:

- internal filters  
- timing rules  
- strategy‑specific edge validation  

### Layer 5 — Execution Layer  
Only when all previous layers say **YES** does the Execution Engine:

- calculate lot size  
- place SL/TP 
- activate STOP/LIMIT state machine  
- execute the order  

This design ensures execution that is:

- **safe**  
- **consistent**  
- **symbol‑aware**  
- **strategy‑aware**  
- **deterministic**  
- **conflict‑free**

---

## 5. Strategy Module Integration
### Strategies consume context — they do not create it.

Strategy Modules do **not** determine market structure, classify regimes, or evaluate safety.  
They simply consume the validated execution context produced by the AMATA Core.

Each strategy receives:

- current regime  
- volatility state  
- structural context  
- symbol thresholds  
- safety status  

A strategy activates only if:

1. the Safety Engine confirms the environment  
2. the current regime is open for trade execution  
3. the symbol profile permits execution  
4. the strategy’s own filters validate edge  

This ensures clean, conflict‑free multi‑strategy execution across all symbols.

---

## 6. STOP/LIMIT Execution Logic

AMATA uses a **stateful, deterministic STOP/LIMIT model**:

- no pending orders  
- no race conditions  
- no hidden states  
- no implicit fallbacks  

The engine continuously monitors:

- STOP trigger levels  
- LIMIT trigger levels  
- structural transitions  
- volatility shifts  
- safety changes  

LIMIT or STOP entry conditions validate while the current regime remains in preferred_classes.
When entry conditions are met - AMATA calculates position size, places SL and TP, executes immediately, and logs the trade.

This is one of AMATA’s most advanced components.

---

### 6.1 Regime‑Driven STOP/LIMIT Behaviour
STOP and LIMIT entries are treated as independent execution paths because **market behaviour varies across regimes**.

AMATA models market phases as regimes, and each regime exhibits different statistical characteristics:

- expansion
- contraction
- drift
- chop
- exhaustion
- reversal

Historical data shows that:

- **momentum‑driven regimes favour STOP‑based activation**
- **mean‑reversion or pullback regimes favour LIMIT‑based activation**

For this reason, the Execution Engine loads separate thresholds, filters, and activation rules for STOP and LIMIT entries.

**When the symbol’s data shows a clear statistical separation between STOP and LIMIT behaviour, AMATA enables both paths independently**.
If no separation exists, the engine defaults to a unified threshold set.

This design allows AMATA to extract **multiple strategies** from the same symbol without conflicts or overlapping execution conditions.

---

## 7. Execution State Machine

AMATA operates through a deterministic, regime‑driven execution loop.  
At every new candle, the engine evaluates market conditions and transitions between states based on regime, safety, and symbol‑specific thresholds.

### **IDLE**  
The engine is active but no regime has yet qualified for execution.  
No thresholds are loaded and no strategies are evaluated.

### **READY**  
A new candle is detected.  
The engine reads the current regime and checks if it is included in the symbol’s *preferred_classes*.  
If so, AMATA loads all relevant thresholds from the symbol profile and prepares for potential entry.

### **WAITING_FOR_PRICE**  
Thresholds are active and strategies may validate edge.  
AMATA now waits for one of three outcomes:

1. **Entry conditions are validated** → proceed to EXECUTING  
2. **The regime changes** → abort and return to READY 
3. **Safety or symbol‑level constraints invalidate** → transition to a blocking state

All regime and safety‑related interruptions are logged for full transparency.

### **EXECUTING**  
All LIMIT or STOP entry conditions validate while the current regime remains in *preferred_classes*.
AMATA calculates position size, places SL and TP, executes immediately, and logs the trade.

### **COOLDOWN**  
A post‑execution stabilization phase preventing duplicate entries and allowing the engine to reset cleanly before returning to READY.

### **Blocking States**

These states override the normal flow and prevent execution until conditions normalize:

- **BLOCKED_BY_SAFETY** — safety conditions violated (news, volatility, ATR, spread, session).  
- **BLOCKED_BY_NEWS** — active news lock (pre‑release, release, post‑release).  
- **BLOCKED_BY_SYMBOL** — symbol‑specific thresholds not satisfied (ATR, volatility, structure, regime not in *preferred_classes*).

This regime‑driven state machine ensures that AMATA only executes trades when the environment, regime, symbol profile, and strategy edge all align — and aborts immediately when the regime changes.

---

## 8. Internal Execution Locks

Beyond Safety and News, the Execution Engine applies additional internal locks to ensure clean, conflict‑free execution across all strategies and symbols.

These include:

- **session‑level cooldown (user‑controlled)**  
  Defined by `SessionCooldownMinutes`.  
  Applies globally, not per symbol

- **strategy‑level edge cooldowns (internal)**  
  Strategies may enforce their own timing or structural spacing before allowing a new entry.

- **structure‑based constraints (external)**  
  Entries are blocked during structural transitions, invalidation zones, or no‑trade zones defined in the symbol profile.

- **volatility‑based constraints (internal)**  
  Entries are blocked when ATR, volatility bands, or spread conditions fall outside permitted ranges.

- **global trade limits (user‑controlled)**  
  `MaxOpenTrades`, `MaxOpenTradesPerSymbol`, and `MaxTradesPerSession` restrict how many trades AMATA may execute simultaneously.

These locks ensure that AMATA executes only when all conditions align — and never over‑executes or conflicts across strategies.

---

## 9. Logging Integration

Every step of the execution pipeline is logged:

- confirmed entries  
- STOP/LIMIT transitions  
- SL/TSL updates  
- execution states  
- safety blocks  
- news blocks  
- regime changes  

This provides full transparency and enables deep analysis.

---

## 10. Summary

The AMATA Execution Engine is a **modular, data‑driven, context‑aware, multi‑layered execution system** designed for:

- **safety**  
- **precision**  
- **scalability**  
- **transparency**  
- **multi‑strategy orchestration**  

It is the heart of the AMATA Platform — the component that transforms market context into deterministic, conflict‑free execution.

---