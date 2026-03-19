---
name: godot-setup
description: "Detect Godot project configuration (project.godot, GUT, gdtoolkit) and write compound-engineering.local.md with Godot review agents. Use when setting up a Godot project for /gc:review."
disable-model-invocation: true
allowed-tools:
  - Bash
  - Read
  - Write
  - Glob
---

# Godot Compound Setup

Interactive setup for `compound-engineering.local.md` — configures which agents run during `/gc:review` and `/gc:work`.

## Interaction Method

If `AskUserQuestion` is available, use it for all prompts below.

If not, present each question as a numbered list and wait for a reply before proceeding. For multiSelect questions, accept comma-separated numbers (e.g. `1, 3`). Never skip or auto-configure.

## Step 1: Check Existing Config

Read `compound-engineering.local.md` in the project root. If it exists, display current settings and ask:

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

## Step 2: Detect Project Environment

Run detection checks:

```bash
# Godot project
test -f project.godot && echo "GODOT_PROJECT=true" || echo "GODOT_PROJECT=false"

# Godot version from project.godot
grep -oP 'config/features=PackedStringArray\("([^"]+)"' project.godot 2>/dev/null | head -1

# GUT test framework
test -d addons/gut && echo "GUT=true" || echo "GUT=false"

# gdtoolkit
which gdformat 2>/dev/null && echo "GDFORMAT=true" || echo "GDFORMAT=false"
which gdlint 2>/dev/null && echo "GDLINT=true" || echo "GDLINT=false"
```

**If no `project.godot` found:** Warn that this doesn't appear to be a Godot project. Ask whether to proceed anyway or cancel.

**Report detection results:**

```
Detected Godot project:
  project.godot: ✓
  Godot version: {version or "unknown"}
  GUT (testing): {✓ or ✗ — install: https://github.com/bitwes/Gut}
  gdformat:      {✓ or ✗ — install: pipx install "gdtoolkit==4.*"}
  gdlint:        {✓ or ✗ — installed with gdtoolkit}
```

Ask how to configure:

```
question: "How would you like to configure review agents?"
header: "Setup"
options:
  - label: "Auto-configure (Recommended)"
    description: "Use smart defaults for Godot 4 projects. Done in one click."
  - label: "Customize"
    description: "Choose which review agents and focus areas to enable."
```

### If Auto-configure → Skip to Step 4 with defaults:

Default agents: `[gc-gdscript-reviewer, gc-godot-architecture-reviewer, gc-code-simplicity-reviewer, gc-pattern-recognition-specialist]`

### If Customize → Step 3

## Step 3: Customize

**a. Focus areas** — multiSelect:

```
question: "Which review areas matter most?"
header: "Focus"
multiSelect: true
options:
  - label: "GDScript quality"
    description: "Static typing, naming, member ordering (gc-gdscript-reviewer)"
  - label: "Architecture"
    description: "Scene composition, signals, autoloads (gc-godot-architecture-reviewer)"
  - label: "Resource safety"
    description: ".tres/.tscn integrity, .uid sidecars, shared mutation (gc-resource-safety-reviewer)"
  - label: "Performance"
    description: "_process abuse, typed hotpaths, Server APIs (gc-godot-performance-reviewer)"
  - label: "Timing"
    description: "Signal timing, await races, queue_free safety (gc-godot-timing-reviewer)"
  - label: "Code simplicity"
    description: "Over-engineering, YAGNI violations (gc-code-simplicity-reviewer)"
  - label: "Patterns"
    description: "Design patterns, anti-patterns, naming (gc-pattern-recognition-specialist)"
```

**b. Depth:**

```
question: "How thorough should reviews be?"
header: "Depth"
options:
  - label: "Thorough (Recommended)"
    description: "All selected focus agents."
  - label: "Fast"
    description: "GDScript reviewer + code simplicity only."
  - label: "Comprehensive"
    description: "All focus agents + git history analysis."
```

## Step 4: Build Agent List and Write File

**Available review agents (always-on):**
- GDScript quality → `gc-gdscript-reviewer`
- Architecture → `gc-godot-architecture-reviewer`
- Code simplicity → `gc-code-simplicity-reviewer`
- Patterns → `gc-pattern-recognition-specialist`

**Available review agents (opt-in):**
- Resource safety → `gc-resource-safety-reviewer`
- Performance → `gc-godot-performance-reviewer`
- Timing → `gc-godot-timing-reviewer`

**Conditional agents (auto-dispatched by /gc:review based on changed files):**
- `gc-resource-safety-reviewer` — when .tres/.tscn/.uid files change
- `gc-godot-export-verifier` — when export_presets.cfg or project.godot changes
- `gc-godot-architecture-reviewer` — when .tscn files change

**Depth presets:**
- Fast: `[gc-gdscript-reviewer, gc-code-simplicity-reviewer]`
- Thorough: all selected focus agents
- Comprehensive: all above + `gc-git-history-analyzer`

**Plan review agents:** `gc-code-simplicity-reviewer`

Write `compound-engineering.local.md`:

```markdown
---
review_agents: [{computed agent list}]
plan_review_agents: [gc-code-simplicity-reviewer]
---

# Review Context

Add project-specific review instructions here.
These notes are passed to all review agents during /gc:review and /gc:work.

Examples:
- "Static typing is mandatory — flag any untyped declarations"
- "Composition over inheritance — limit scene inheritance to one layer"
- "Event bus for cross-system events only — not for parent-child communication"
```

## Step 5: Confirm

```
Saved to compound-engineering.local.md

Project:      Godot {version}
GUT:          {✓/✗}
gdtoolkit:    {✓/✗}
Review depth: {depth}
Agents:       {count} configured
              {agent list, one per line}

Tip: Edit the "Review Context" section to add project-specific instructions.
     Re-run this setup anytime to reconfigure.
```
