---
name: research_artefact
description: Responsible for forming and recording the final artifact based on conducted research results.
allowed-tools: Read, Write
user-invocable: false
---

## Motivation
Formatting research into a separate structured file transforms a one-time analysis into a permanent engineering artifact
that can be revisited, discussed, and used in work. This reduces the risk of knowledge loss and makes findings verifiable
and reproducible. The structure disciplines thinking and improves the quality of technical solutions.

## RESEARCH.md Formation Rules

### General Requirements
1. Language: write **strictly in the user's language**
2. Format: Markdown with embedded Mermaid diagrams
3. Location: repository root or current directory where the `.claude` directory is located. Filename: `RESEARCH.md`. Full path: `<project>/.claude/RESEARCH.md`
4. Long files (>500 lines): split into multiple diagrams/sections

### File Structure

The file must contain the following sections in the specified order:

#### 1. `# Code Research` - header

#### 2. `## Context and Boundaries`
Content:
- Object of research (what exactly was studied)
- Entry points - list of files/classes/functions
- System boundaries - layers and external systems
- Architectural style (example: MVVM, Clean Architecture)

Format:
```markdown
## Context and Boundaries

Object of research: [description].

Entry points:
- [File1.kt]
- [ClassName]
- [functionName]

Boundaries:
- UI layer: [description]
- Domain layer: [description]
- Data layer: [description]
- External systems: [list]

Architecture style: [style].
```

#### 3. `## What the code does`
Content:
- Step-by-step work scenario (1., 2., 3. ...)
- Implementation features (coroutines, threading, error handling)
- Used patterns

Format:
```markdown
## What the code does

Scenario:
1. [Step 1]
2. [Step 2]
3. [Step 3]

Features:
- [feature 1]
- [feature 2]
```

#### 4. `## Key scenarios`
Content:
- Main execution paths (happy path, error path, edge cases)
- For each scenario: brief description of features

Format:
```markdown
## Key scenarios

### 1. [Scenario name]
- [feature 1]
- [feature 2]

### 2. [Scenario name]
- [feature 1]
```

#### 5. `Enrichment with diagrams`

Review the `mermaid` skill if it hasn't been studied yet.

#### 6. `## Risks, bugs and problem areas`
Content:
- Strictly a table of all found problems
- Using lists (numbered or bulleted) is prohibited
For each problem, specify:
- Severity: Critical / High / Medium / Low
- Evidence: reference to file/symbol/lines
- Why it matters: why it's important
- Suggested fix: brief suggestion for fixing

Format:

| Problem | Severity | Evidence | Why it matters | Suggested fix |
|---------|----------|----------|----------------|---------------|
| [Problem name] | [level] | [file.kt:10-20] | [description] | [solution] |
| [Problem name] | [level] | [file.kt:line] | [description] | [solution] |

An additional column is allowed:
- Risk category (Security / Stability / Performance / Maintainability)

**Important:** problem search must include:
- Bugs (logic errors, NPE risks, race conditions)
- Security/privacy risks (tokens, sensitive data, cleartext)
- Stability risks (timeouts, retries, cancellation leaks)
- Performance risks (main thread, allocations, O(n²))
- Maintainability/style (naming, coupling, SRP violations)

#### 7. `## Recommended work plan`
Content:
- Strictly a table with prioritized task backlog
- Using lists and P0/P1/P2 subheadings is prohibited
- Grouping by priority through Priority column

For each task, specify:
- Priority: P0 / P1 / P2
- Task name
- Description
Format:

| Priority | Task | Description |
|----------|------|-------------|
| P0 | [Task name] | [details] |
| P1 | [Task name] | [details] |
| P2 | [Task name] | [details] |


#### 8. `## Questions and assumptions`
Content:
- Questions for which answers couldn't be found in the code
- Assumptions made during analysis
- Files that could not be accessed

Format:
```markdown
## Questions and assumptions

- [Question 1]
- [Question 2]
- Could not access: [list of files]
```

## File Writing Algorithm

### File Existence Check
1. Check if `RESEARCH.md` exists:
   - If file doesn't exist → create new
   - If file exists:
     - Read first 100 lines
     - If file is empty or contains only whitespace → overwrite without questions
     - If file contains content → **stop and ask user**: "RESEARCH.md already filled. Overwrite?"

### Content Writing
1. **Overwrite** (not append): completely clear and write new content
2. **Section order**: strictly as specified above (1-9)
3. **Diagrams**: embed in corresponding sections in mermaid blocks
4. **Code references**: use format `file.kt:line` or `file.kt:10-20` for ranges
5. **Formatting**: use markdown components (lists, tables, code blocks) for structuring

### Quality Check
Before saving, check:
- [ ] All sections are present and in correct order
- [ ] File language matches user language
- [ ] Diagrams are correctly embedded in ```mermaid blocks
- [ ] All code references are checked and current
- [ ] Specific problems are found with severity and evidence indicated
- [ ] Work plan contains priorities P0/P1/P2
- [ ] Questions and assumptions are documented

## Error Handling

- **Could not read file**: document in "Questions and assumptions" section
- **Could not find code reference**: remove or replace with approximate location
- **Diagram generation error**: use textual description instead of diagram

## Consistency with Other Skills

- For building diagrams → use `mermaid` skill
- For determining analysis depth → use `research_depth` skill
- For searching files → use `Glob` and `Grep`
- For reading code → use `Read`