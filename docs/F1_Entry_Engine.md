# AMATA Entry Engine  
### Entry Orchestration Layer of the Autonomous Multi‑Asset & Multi‑Strategy Trading Agent

The **AMATA Entry Engine** is the layer that transforms a strategy’s validated trading signal into a **structured entry request** ready for execution.  
It does **not** calculate edge, evaluate indicators, or place orders.  
Instead, it ensures that strategy conditions are translated into a **consistent, symbol‑aware, and context‑aware entry decision**.

Each strategy defines its own conditions in external **Symbol Profiles** (see *Symbol Profile Specification*).  
The Entry Engine simply checks whether those conditions are satisfied in the current environment.  
If they are, the strategy is allowed to request an entry.  
If not, the request is ignored.

This means the Entry Engine does **not** need to understand the strategy itself —  
it only follows the rules defined for that symbol and that strategy.

The Entry Engine decides **if**, **when**, and **how** a strategy is allowed to request execution.  
The actual order placement is handled by the Execution Engine.

---

## 1. Role in the AMATA Architecture

The Entry Engine sits between the **context‑producing layers** of AMATA and the **execution layer** that places trades.

It receives validated entry requests from the Strategy Layer and ensures that these requests are compatible with:

- **Safety Engine**  
  (news locks, session blocks, volatility constraints — see the  
  [Safety Engine Specification](./AMATA_Safety_Engine.md))

- **Regime Engine**  
  (current market regime classification — see the  
  [Regime Engine Specification](./AMATA_Regime_Engine.md))

- **Volatility Engine**  
  (ATR state, volatility bands — see  
  [Platform Configurations — Volatility & Exhaustion Controls](./AMATA_Platform_Configurations.md))

- **Symbol Profiles**  
  (strategy‑specific entry conditions defined externally — see the  
  [Symbol Profile Specification](./AMATA_Symbol_Profiles.md))

Only when all relevant conditions are satisfied does the Entry Engine prepare a structured entry request for the Execution Engine.

High‑level flow:

```
Safety / Regime / Volatility / Symbol Profile
                ↓
           Strategy Layer
                ↓
            Entry Engine
                ↓
          Execution Engine
```

The Entry Engine acts as the **translation layer** between strategy‑level conditions and executable orders.  
It does not evaluate edge or place trades — it ensures that each strategy’s externally defined conditions are applied consistently before an entry is allowed to proceed.

---

### Strategy Layer (Upstream Module)

The Strategy Layer is responsible for evaluating each strategy’s edge conditions as defined in the Symbol Profile.  
It determines whether a strategy wants to take an entry and submits a **validated entry request** to the Entry Engine.

The Strategy Layer performs all indicator evaluations, threshold checks, and edge validation.  
The Entry Engine does not compute edge — it only receives the final request and applies symbol‑specific entry behaviour.

---

## 2. Inputs and Outputs

### 2.1 Inputs

The Entry Engine receives a **validated entry request** from the Strategy Layer, together with the contextual information described in  
**Section 1 — Role in the AMATA Architecture**.

This includes:

- Safety context  
- Regime context  
- Volatility context  
- Symbol Profile rules  

All strategy logic, filters, and conditions are defined in **external files**.  
The Entry Engine does not compute edge or evaluate indicators — it only consumes the processed context provided by AMATA’s core modules.

Using this information, the Entry Engine determines:

- whether the strategy is allowed to request an entry  
- whether the symbol and environment permit execution  
- whether the entry should use **LIMIT** or **STOP** behaviour  
- whether any basic constraints (e.g., time windows) block the request 

---

### 2.2 Outputs

If all conditions are satisfied, the Entry Engine produces a structured **Entry Decision**, containing:

- symbol  
- strategy ID  
- selected entry model  
  - **LIMIT** — default behaviour across the symbol’s full volatility spectrum  
  - **STOP** — activated only as a boost/sniper when entry conditions clearly separate from LIMIT  
- all entry‑related parameters required by the Execution Engine
- reference to the SL/TSL profile associated with the entry type  
- metadata required by the Execution Engine  

This Entry Decision is forwarded to the **Execution Engine**, which then:

- applies risk limits  
- calculates position size  
- applies SL/TSL logic  
- enforces global constraints  
- executes or rejects the trade  

The Entry Engine does not place orders — it prepares the decision that the Execution Engine acts upon.

---

### 2.3 Responsibilities

The Entry Engine is responsible for:

- receiving validated entry requests from the Strategy Layer  
- applying symbol‑specific entry behaviour  
- selecting **STOP** or **LIMIT** entry models  
- enforcing basic entry constraints (e.g., time windows, safety locks)  
- preparing a complete **Entry Decision** for the Execution Engine  

The Entry Engine does **not**:

- compute edge  
- evaluate indicators  
- read external configuration files directly  
- calculate SL/TSL distances  
- place orders or enforce risk limits  

These responsibilities belong to other modules in the AMATA Core Engine.

---

## 3. Entry Model Selection (STOP vs LIMIT)

The Entry Engine determines whether a strategy’s entry request should use **LIMIT** or **STOP** behaviour.  
This selection is fully defined in the symbol’s external configuration and does not involve any internal edge calculations.

- **LIMIT**  
  Default entry behaviour across the symbol’s full volatility spectrum.

- **STOP**  
  Activated only as a boost/sniper when the entry conditions clearly separate from LIMIT behaviour.

Each strategy may define its own STOP/LIMIT preferences in its Symbol Profile.  
The Entry Engine simply applies these rules and forwards the selected entry model to the Execution Engine, which computes the actual price levels and SL/TSL distances.

---

## 4. Strategy Modules and Isolation

The Entry Engine supports **multiple independent strategies per symbol**.  
Each strategy is defined externally through its own Symbol Profile and is treated as an isolated module inside the AMATA platform.

### Strategy Isolation  
The Entry Engine guarantees that:

- each strategy is evaluated independently  
- one strategy cannot block or interfere with another  
- cooldowns apply only to the strategy that triggered them  
- STOP/LIMIT preferences are applied per strategy  

This ensures clean separation between strategies, even when they operate on the same symbol and within the same market regime.

### Multi‑Strategy Compatibility  
AMATA can run multiple strategies in parallel on a single symbol.  
The Entry Engine evaluates each strategy request independently and prepares separate Entry Decisions when conditions are met.

This modular design is what enables AMATA’s **multi‑strategy architecture** inside a single trading agent.

---

## 5. Logging and Transparency

The Entry Engine logs all entry‑related decisions for transparency and post‑trade analysis.  
These logs are descriptive rather than revealing — they show *what happened*, not *how* internal logic is computed.

The Entry Engine records:

- which strategies requested entries  
- which requests were accepted 
- the selected entry model (STOP or LIMIT)  
- the strategy ID associated with the request  
- all non-sensitive entry‑related parameters used by AMATA to evaluate the entry at that moment  

These logs allow AMATA to analyse live behaviour and understand how different strategies perform under real market conditions.

The Entry Engine does **not** log trade lifecycle events.  
Trade entry, trade progress, and trade exit are logged separately by the Execution Engine and the Trade Logger.

---

## 6. Strategy‑Level Cooldown

The Entry Engine enforces an internal **per‑strategy cooldown** to prevent over‑execution and ensure clean multi‑strategy behaviour.  
Each strategy maintains its own cooldown state per symbol, independent of other strategies.

If a strategy is in cooldown, its entry request for that symbol is skipped until the cooldown expires.  
This mechanism is internal to the Entry Engine and is not user‑configurable.

This strategy‑level cooldown is separate from the platform’s global execution constraints — such as **SessionCooldownMinutes**, which prevents multiple trades on the same symbol within a user‑defined time window and is enforced by the Execution Engine.

---

## Summary

The AMATA Entry Engine is the orchestration layer that transforms validated strategy signals into structured, executable entry decisions.  
It does not compute edge, evaluate indicators, or place orders. Instead, it ensures that each strategy’s externally defined conditions are applied consistently within the current safety, regime, volatility, and symbol‑specific environment.

The Entry Engine:

- receives validated entry requests from the Strategy Layer  
- applies symbol‑specific entry behaviour  
- selects STOP or LIMIT entry models  
- enforces basic entry constraints  
- maintains per‑strategy cooldowns  
- prepares complete Entry Decisions for the Execution Engine  

It guarantees clean multi‑strategy operation by isolating strategies per symbol and ensuring that no strategy can interfere with another.  
All trade lifecycle events, risk enforcement, and order placement are handled by the Execution Engine and the Trade Logger.

In short, the Entry Engine defines **how** a strategy is allowed to enter —  
the Execution Engine decides **whether** the trade can be executed safely.

---