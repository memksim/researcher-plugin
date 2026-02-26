# Researcher Plugin

A Claude Code plugin for code analysis and research.

## Features

- **Code Explanation**: Analyzes code with visual diagrams and analogies
- **Sequence Diagrams**: Generates Mermaid sequence diagrams for key scenarios
- **Dependency Graphs**: Creates dependency diagrams showing module relationships
- **Risk Assessment**: Identifies bugs, security issues, and code smells
- **Task Backlog**: Generates prioritized improvement recommendations

## Installation

Place this plugin in your Claude Code plugins directory.

## Usage

Use the `/research` skill to analyze code:

```
/research path/to/file.kt
```

The skill will:
1. Analyze the requested code and its dependencies
2. Generate sequence and dependency diagrams
3. Identify risks and problem areas
4. Create a `RESEARCH.md` report with findings

## Example Output

See `skills/research/examples/RESEARCH.md` for a sample report.

## License

MIT
