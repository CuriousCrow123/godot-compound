# Godot Compound Plugin

Godot 4 + GDScript development tools for Claude Code. Fork of Compound Engineering, stripped of all web/Rails/TypeScript content and namespaced under `/gc:`.

## Godot Conventions (inherited by all agents)

- **Language:** GDScript only (no C#)
- **Static typing is mandatory.** Every variable, parameter, and return type must be explicitly typed.
- **Composition over inheritance.** Limit scene inheritance to one layer. Compose entities from single-purpose child nodes. Derive only from engine node types.
- **"Call down, signal up."** Parents call methods on children. Children emit signals. Siblings communicate through a shared parent. Event Bus autoload for genuinely cross-system events only.
- **`.tscn` files are read-only for agents.** Scene files have strict structure. Agents must never edit `.tscn` files directly.
- **Resource safety:** Call `.duplicate()` on any `.tres` Resource that will be mutated at runtime. Prefer `preload()` over dynamic `load()`.

## GDScript Style

- **Naming:** snake_case for files/vars/functions, PascalCase for classes/nodes, UPPER_SNAKE_CASE for constants/enums, `_prefix` for pseudo-private, `is_`/`can_`/`has_` for booleans, past-tense for signals (`damage_taken`).
- **Member ordering:** class_name/extends/docstring → signals → enums → constants → @export → public vars → _private vars → @onready → virtual methods → signal callbacks → public methods → private methods → inner classes.

## Linting

```bash
gdformat --check .   # formatting
gdlint .             # style rules
```

## Command Namespace

All commands use `/gc:` prefix:
- `/gc:plan` — Implementation planning with GUT/gdtoolkit references
- `/gc:work` — Execution with Godot acceptance patterns
- `/gc:review` — Multi-agent review with Godot agents
- `/gc:compound` — Knowledge capture with Godot schema
- `/gc:brainstorm` — Collaborative exploration (game design focus)

## Versioning

- **MAJOR**: Breaking changes
- **MINOR**: New agents, commands, or skills
- **PATCH**: Bug fixes, doc updates

Update `.claude-plugin/plugin.json` and `CHANGELOG.md` with every change.

## Directory Structure

```
agents/
├── review/     # Code review agents
├── research/   # Research and analysis agents
└── workflow/   # Workflow automation agents

commands/
├── gc/         # Core workflow commands (gc:plan, gc:review, etc.)
└── *.md        # Utility commands

skills/
└── */          # Skills with SKILL.md + references/
```
