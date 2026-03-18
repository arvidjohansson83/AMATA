# AMATA — Autonomous Multi‑Asset & Multi‑Strategy Trading Agent  
A fully autonomous, regime‑aware and volatility‑adaptive trading agent built for real market conditions.

AMATA is the evolution of my session‑based architecture MATA.  
Where MATA focused on structural patterns, volatility behaviour and deterministic execution,  
AMATA adds the missing dimension: **context**.

## Core principles
- 24/5 market structure analysis and context‑aware execution  
- Regime‑based market structure analysis & volatility state modelling
- Macro‑aware safety layer with automatic execution halts  
- Multi‑Asset & Multi‑Strategy architecture
- Fully autonomous, policy‑driven and extensible design

## Why AMATA exists
Running MATA live revealed a key limitation:  
**structure without context is not enough.**

MATA executed every day at fixed times, regardless of regime, volatility or macro events.  
AMATA is built to understand when the environment supports the edge — and when it doesn’t.

## Safety‑first execution
AMATA includes a fully autonomous, macro‑aware safety layer that removes the need for manual decision‑making around news and high‑impact events. It automatically identifies which currencies, symbols and macro events are truly price‑moving, filters out irrelevant noise, applies pre‑ and post‑event lock windows, and ensures that strategies only execute when the environment is structurally safe.

This means AMATA users never have to worry about when to trade and when to stay out — AMATA handles that entirely on its own, avoiding noise‑driven whipsaws and aligning execution with meaningful institutional activity.

## Adaptive strategy refinement
AMATA automatically logs every trade it takes, capturing regime, volatility state, structure conditions and execution context. This creates a continuous feedback loop where each strategy receives data‑driven insights from its own performance, enabling ongoing optimisation without manual intervention.

AMATA doesn’t just execute strategies — it learns from them.

## Why AMATA is the last EA I will ever build
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

## Documentation
The full platform documentation is being released module by module:

- `docs/AMATA_platform_structure.md` (coming soon)  
- `docs/AMATA_roadmap.md` (coming soon)

## Status
AMATA is under active development and will be expanded continuously.
