# Claude Code Researcher Plugin

An intelligent code analysis plugin for [Claude Code](https://claude.com/code) that performs deep research of codebases, generates visual diagrams, identifies issues, and produces actionable improvement plans.

## Overview

The Researcher Plugin transforms code analysis from simple explanation into comprehensive engineering research. It uses a specialized agent architecture with multiple skills to provide:

- Deep code understanding with visual diagrams
- Systematic risk and bug identification
- Prioritized improvement recommendations
- Persistent research artifacts

### Components

- **`/research`** - User-facing skill that delegates to the researcher agent
- **researcher agent** - Orchestrates the analysis process
- **research_depth** - Determines analysis depth (L0-L3)
- **mermaid** - Generates Mermaid diagrams
- **research_artefact** - Formats structured RESEARCH.md reports

## Features

### Advanced Code Analysis

- **Multi-level analysis depth**: From quick glance (L0) to full system review (L3)
- **Automatic context expansion**: Identifies related files, dependencies, and callers
- **Architecture mapping**: Understands boundaries between UI, domain, and data layers

### Visual Documentation

- **Sequence diagrams**: Shows component interactions and data flow
- **Dependency graphs**: Maps module and class relationships
- **Flowcharts**: Explains complex decision logic
- **ER diagrams**: Documents database schemas (when applicable)

### Quality Assurance

- **Bug detection**: Logic errors, NPE risks, race conditions
- **Security analysis**: Token handling, sensitive data exposure, cleartext issues
- **Performance review**: Main thread blocking, memory leaks, algorithm complexity
- **Code style assessment**: Naming, coupling, SRP violations, missing tests

### Actionable Output

- **Risk matrix**: Categorized by severity (Critical/High/Medium/Low)
- **Prioritized backlog**: P0 (must fix), P1, P2 tasks with acceptance criteria
- **Test plan**: Unit, integration, and e2e testing recommendations

## Installation
In Claude Code, register the marketplace first: 
`/plugin marketplace add memksim/workflow-marketplace`

Then install the plugin from this marketplace: 
`/plugin install researcher@workflow-plugins`

## Usage

### Basic Analysis

Analyze a specific file:
```
/research src/auth/AuthViewModel.kt
```

### Feature Analysis

Study an entire feature flow:
```
/research "User authentication flow"
```

### Targeted Investigation

Look for specific issues:
```
/research @feature/newsfeed/ "Find memory leaks in image loading"
```

### Custom Scope

Specify analysis boundaries:
```
/research @src/network/ "you must check whole module and identify security risks"
```

### With Context

Provide entry points and goals:
```
/research UserRepository.kt UserUseCase.kt
Goal: Analyze login and registration flows
Scope: Include all dependencies
```

## How It Works

### Phase 1: Request Analysis

1. Parses user query to determine target code
2. Identifies missing context and asks clarifying questions
3. Determines appropriate analysis depth (L0-L3) via `research_depth`

### Phase 2: Code Exploration

1. Locates entry files/symbols
2. Expands context:
   - Same package/module files
   - Direct dependencies (imports, constructor params)
   - Callers and callees
   - Interfaces and implementations
   - Configuration files (Gradle, DI modules, routing)

### Phase 3: Analysis

1. **Behavior explanation**: Documents what code does, control flow, state, threading
2. **Diagram generation**: Creates sequence and dependency diagrams via `mermaid`
3. **Issue identification**: Finds bugs, security risks, performance issues
4. **Improvement planning**: Generates prioritized task backlog

### Phase 4: Artifact Creation

1. Formats findings into structured `RESEARCH.md` via `research_artefact`
2. Embeds Mermaid diagrams
3. Creates chat-friendly summary
4. Handles file conflicts (asks before overwriting existing `RESEARCH.md`)

## License

MIT