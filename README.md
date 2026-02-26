# Claude code plugin for code analysus and research project functionality

## Features

- **Code Explanation**: Analyzes code with visual diagrams and analogies
- **Sequence Diagrams**: Generates Mermaid sequence diagrams for key scenarios
- **Dependency Graphs**: Creates dependency diagrams showing module relationships
- **Risk Assessment**: Identifies bugs, security issues, and code smells
- **Task Backlog**: Generates prioritized improvement recommendations

## Installation
In Claude Code, register the marketplace first: 
`/plugin marketplace add memksim/workflow-marketplace`

Then install the plugin from this marketplace: 
`/plugin install researcher@workflow-plugins`

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
