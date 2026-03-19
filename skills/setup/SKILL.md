---
name: setup
description: Configure which review agents run for your project. Auto-detects stack and writes compound-engineering.local.md.
disable-model-invocation: true
---

# Compound Engineering Setup

## Interaction Method

If `AskUserQuestion` is available, use it for all prompts below.

If not, present each question as a numbered list and wait for a reply before proceeding to the next step. For multiSelect questions, accept comma-separated numbers (e.g. `1, 3`). Never skip or auto-configure.

Interactive setup for `compound-engineering.local.md` — configures which agents run during `/gc:review` and `/gc:work`.

## Step 1: Check Existing Config

Read `compound-engineering.local.md` in the project root. If it exists, display current settings summary and use AskUserQuestion:

```
question: "Settings file already exists. What would you like to do?"
header: "Config"
options:
  - label: "Reconfigure"
    description: "Run the interactive setup again from scratch"
  - label: "View current"
    description: "Show the file contents, then stop"
  - label: "Cancel"
    description: "Keep current settings"
```

If "View current": read and display the file, then stop.
If "Cancel": stop.

## Step 2: Detect and Ask

Auto-detect the project stack:

```bash
test -f project.godot && echo "godot" || \
test -f pyproject.toml && echo "python" || \
test -f requirements.txt && echo "python" || \
test -f tsconfig.json && echo "typescript" || \
test -f package.json && echo "javascript" || \
echo "general"
```

Use AskUserQuestion:

```
question: "Detected {type} project. How would you like to configure?"
header: "Setup"
options:
  - label: "Auto-configure (Recommended)"
    description: "Use smart defaults for {type}. Done in one click."
  - label: "Customize"
    description: "Choose stack, focus areas, and review depth."
```

### If Auto-configure → Skip to Step 4 with defaults:

- **Godot:** `[gc-code-simplicity-reviewer, gc-pattern-recognition-specialist]`
- **General:** `[gc-code-simplicity-reviewer, gc-pattern-recognition-specialist]`

### If Customize → Step 3

## Step 3: Customize (3 questions)

**a. Stack** — confirm or override:

```
question: "Which stack should we optimize for?"
header: "Stack"
options:
  - label: "{detected_type} (Recommended)"
    description: "Auto-detected from project files"
  - label: "Godot 4"
    description: "Godot 4 + GDScript — adds GDScript, architecture, and resource safety reviewers"
  - label: "Python"
    description: "Python — adds Pythonic pattern reviewer"
  - label: "TypeScript"
    description: "TypeScript — adds type safety reviewer"
```

Only show options that differ from the detected type.

**b. Focus areas** — multiSelect:

```
question: "Which review areas matter most?"
header: "Focus"
multiSelect: true
options:
  - label: "Code simplicity"
    description: "Over-engineering, YAGNI violations (gc-code-simplicity-reviewer)"
  - label: "Patterns"
    description: "Design patterns, anti-patterns, naming conventions (gc-pattern-recognition-specialist)"
```

**c. Depth:**

```
question: "How thorough should reviews be?"
header: "Depth"
options:
  - label: "Thorough (Recommended)"
    description: "Stack reviewers + all selected focus agents."
  - label: "Fast"
    description: "Stack reviewers + code simplicity only. Less context, quicker."
  - label: "Comprehensive"
    description: "All above + git history, data integrity, agent-native checks."
```

## Step 4: Build Agent List and Write File

**Available review agents:**
- Code simplicity → `gc-code-simplicity-reviewer`
- Patterns → `gc-pattern-recognition-specialist`

**Depth:**
- Thorough: all available review agents
- Fast: `gc-code-simplicity-reviewer` only
- Comprehensive: all above + `gc-git-history-analyzer`

**Plan review agents:** `gc-code-simplicity-reviewer`.

Write `compound-engineering.local.md`:

```markdown
---
review_agents: [{computed agent list}]
plan_review_agents: [{computed plan agent list}]
---

# Review Context

Add project-specific review instructions here.
These notes are passed to all review agents during /gc:review and /gc:work.

Examples:
- "We use signals heavily — check for circular signal connections"
- "Static typing is mandatory — flag any untyped declarations"
- "Composition over inheritance — limit scene inheritance to one layer"
```

## Step 5: Confirm

```
Saved to compound-engineering.local.md

Stack:        {type}
Review depth: {depth}
Agents:       {count} configured
              {agent list, one per line}

Tip: Edit the "Review Context" section to add project-specific instructions.
     Re-run this setup anytime to reconfigure.
```
