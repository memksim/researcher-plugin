---
name: research
description: Proxy skill that delegates code analysis to the researcher agent. Explains code with visual diagrams and advice improvements. Use when explaining how code works, teaching about a codebase, or when the user asks "How does this work?"
allowed-tools: Read, Grep, Glob
model: inherit
context: fork
agent: researcher
---

## Purpose
This is a **proxy skill** that forwards code analysis requests to the `researcher` agent.

The skill acts as a simple entry point that:
1. Captures user requests for code analysis
2. Delegates all work to the specialized `researcher` agent
3. Returns the agent's findings back to the user

## When to use
Use this skill when user asks to:
- "analyze code", "explain how it works", "find bugs", "assess quality", "draw diagrams"
- or provides a snippet / file / symbol / module path and wants analysis

## How it works
1. User request → this skill receives the query
2. Skill forwards request → to `researcher` agent
3. Agent performs analysis using its full toolset (Read, Grep, Glob, Bash)
4. Agent uses sub-skills: `mermaid`, `research_artefact`, `research_depth`
5. Results returned → back to user

## Inputs (what to ask for if missing)
- Entry point: file path(s), class/function name(s), or a snippet
- Goal: what scenario to analyze (happy path, error path, edge cases)
- Scope: "only this file" vs "whole module/feature"

> The agent will ask for clarification if context is insufficient.

## Outputs
The `researcher` agent returns:
- **Chat response**: Executive summary in user's language with key findings
- **RESEARCH.md file**: Structured report with:
  - Context and boundaries
  - Code behavior explanation
  - Key scenarios
  - Sequence diagram (Mermaid)
  - Dependency diagram (Mermaid)
  - Risks, bugs, and problem areas
  - Recommended work plan (P0/P1/P2)
  - Questions and assumptions

## Constraints
- **Language**: Agent responds in the same language as the user's query
- **File creation**: Always creates/updates RESEARCH.md in repository roots `.claude` folder
  - If RESEARCH.md exists with content → asks user before overwriting
  - If file doesn't exist or is empty → creates new file
- **Diagrams**: All diagrams generated in Mermaid format
- **Quality**: Concrete findings with code references (file paths, line numbers)

## Agent capabilities
The researcher agent can analyze:
- Single methods or functions
- Classes and components
- Modules and packages
- Complete user flows (e.g., auth, checkout, media loading)
- Entire applications

The agent can also search for:
- Vulnerabilities
- Bugs
- Security issues
- Memory leaks
- Performance problems
- Network issues
- Concurrency problems

## Example flow
```
User: "Analyze the login flow in auth module"
    ↓
research skill (fork context)
    ↓
researcher agent (full analysis)
    ↓
User receives:
  - Summary in chat
  - RESEARCH.md with diagrams and findings
```