---
name: research_depth
description: Determines the required research depth based on the user's request and forms the analysis framework. It sets the research scope, mandatory aspects for review, and constraints that the agent must follow.
allowed-tools: Read, Write
user-invocable: false
---

## Motivation
Formalizing research depth allows controlling the scope of analysis and avoiding both superficial and excessively
deep investigations.
This makes the agent's behavior predictable and simplifies its integration into orchestration. Depth becomes an explicit quality contract between
the user and the system.

## Depth Levels

### L0 — Quick glance

- only the requested piece
- brief explanation of "what it does"

### L1 — Local context (default for method/class)

- nearest context: calls up/down (2-3 levels)
- dependencies, contracts, edge cases

### L2 — Feature/Flow (for feature/user path)

- architectural boundaries
- main scenarios

### L3 — System/Whole app (for entire app/problem search/whole module analysis)

- system risks: security/performance/concurrency
- cross-cutting dependencies, cycles, data protocols

## Selection Rules

- If request = function/method → L0 is sufficient
- If request = class/component → minimum L1, often L2 if many connections
- If request = flow/feature → minimum L2
- If request = problem/bug/regression → minimum L2 + include code style/antipatterns
- If request = entire app/architecture → L3
- If insufficient data → skill returns questions (up to 3-5) instead of depth