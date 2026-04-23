# AMATA Safety Engine  
**News‑Aware Execution Guard for Volatile Market Events**

The **AMATA Safety Engine** is a protective module that prevents trading during news events known to cause abnormal volatility or unpredictable price behavior.  
It acts as a **dynamic execution lock**, pausing trading for affected symbols before and after major economic releases.

The Safety Engine ensures that AMATA operates only when market conditions are stable and aligned with institutional behavior.

---

## 1. Purpose

Financial markets can experience extreme volatility during certain news events.  
The AMATA Safety Engine is designed to:

- Apply symbol‑specific news mapping  
- Support externally configurable lock durations  
- Pause trading during historically volatile news events  
- Prevent entries when conditions are unstable  
- Resume operation immediately after the event window  

This module enhances AMATA’s robustness by ensuring that trading occurs only in suitable environments.

---

## 2. How AMATA Handles News Releases

AMATA includes a dedicated **Safety Engine** designed to protect the platform during periods of abnormal volatility caused by scheduled economic events.

For every upcoming news release, AMATA follows a strict policy:

- If a symbol is likely to be affected by the event, AMATA activates a Safety Filter
- This filter temporarily blocks new trades before and after the event
- Only symbols that may experience volatility are locked
- All unaffected symbols continue trading normally

This ensures that AMATA behaves in a controlled, institutional manner during sensitive market conditions caused by scheduled economic events, without interrupting trading on unrelated assets.

---

## 3. Symbol‑Specific News Mapping

Each symbol in AMATA is linked to one or more currencies through a **symbol‑specific mapping system**.
This mapping determines which news events are relevant for each symbol.

Key principles:

- Symbols inherit news relevance from their associated currencies
- Cross‑pairs inherit relevance from both currencies
- Indices inherit relevance from the currencies that historically drive their volatility
- Symbols with no relation to the event’s currency remain fully active

Examples:

- USD events lock only USD‑mapped symbols  
- GBP events lock only GBP‑mapped symbols  
- XAUUSD inherits USD mapping  
- DAX40 → inherits EUR and USD

This mapping ensures that AMATA reacts only to news events that are historically relevant for each symbol.

---

## 4. Execution Lock Logic

When a relevant event is detected, the Safety Engine:

1. Identifies affected symbols  
2. Activates a **pre‑news lock**  
3. Pauses entry evaluation and execution  
4. Maintains the lock through the release  
5. Extends the lock for a **post‑news window**  
6. Automatically resumes normal operation  

Open positions are not affected unless explicitly configured; AMATA does not force‑close trades during news events.

---

## 5. User‑Controlled Parameters

The Safety Engine uses only a very small set of **direct EA inputs** related to session‑based blocking:

- SessionPreOpenBlockMinutes  
- SessionPostOpenBlockMinutes  

All news‑related behavior — including pre‑news and post‑news lock durations, symbol‑specific overrides, currency mappings, and event definitions — is configured through **external JSON files**.  
These files are fully user‑editable but are **not EA inputs**.

For a complete overview of all platform‑level configuration options, see:  
[**User‑Configurable Platform Inputs**](AMATA_Platform_Configurations.md)

---

## 6. High‑Impact Focus

The Safety Engine reacts **only to events that have historically shown the ability to move the market**, such as:

- Central Bank decisions and communications
- Inflation releases
- Employment reports
- GDP and growth indicators
- Major geopolitical statements
- High‑impact speeches

Low‑impact or routine events are ignored.

---

## 7. Integration With the AMATA Engine

The Safety Engine operates as a **parallel protective layer**:

- It does not modify strategy logic  
- It does not alter symbol profiles  
- It only controls whether AMATA may evaluate entries  

When active:

- The AMATA Engine continues running  
- Entry evaluation is temporarily suspended for affected symbols
- Normal operation resumes instantly when the lock expires  

This ensures seamless integration without architectural interference.

---

## 8. Weekly News Update System

AMATA uses a two‑stage news configuration system to ensure accurate and symbol‑specific handling of market events.

### 8.1 Stage 1 — Global Weekly News File

AMATA first loads a **global weekly news file** containing all scheduled Financial News for the upcoming week.  

This file includes:

- All upcoming economic releases  
- Timestamps for each event  
- Associated currencies  
- General metadata  

This file acts as the raw data source for the Safety Engine.

### 8.2 Stage 2 — Currency‑Specific News Filters

AMATA then loads external **currency‑specific news configuration files**. 
These files determine, **based on event titles**, which events should trigger execution locks.

Only events listed in these filters are treated as impactful.
This ensures that AMATA does not block trading unnecessarily.

### 8.3 Combined Logic

The Safety Engine combines:

- The full weekly news list  
**with**  
- The currency‑specific filters  

…to determine exactly which events should trigger pre‑ and post‑news lock windows for each symbol.

This design ensures:

- Maximum accuracy  
- Minimal downtime  
- Full user control through editable JSON files  
- No need to modify EA code when news behavior changes  

---

## Summary

The AMATA Safety Engine provides a critical protection layer that prevents trading during news events with historically proven market impact.

Key strengths:

- **Symbol‑specific news mapping** ensures that only relevant symbols are locked during each scheduled  economic news release
- **Externally configurable lock windows** allow full control over pre‑ and post‑news behavior  
- **Seamless integration** with the AMATA Engine without modifying strategy logic or symbol profiles  
- **Weekly external news files** keep the system aligned with real‑world market schedules  
- **Minimal downtime** by blocking only symbols that may experience volatility  
- **Institution‑grade execution safety** during sensitive market conditions  

Together, these components form a transparent, reliable, and institution‑grade risk management layer that prevents unnecessary exposure during periods of elevated volatility.

---