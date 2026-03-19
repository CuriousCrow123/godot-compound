# Godot Compound

Godot 4 + GDScript development tools for Claude Code. Fork of [Compound Engineering](https://github.com/EveryInc/compound-engineering-plugin) v2.38.1, stripped of all web/Rails/TypeScript content and rebuilt with Godot-specific agents.

## Installation

Local plugin installation requires a marketplace wrapper. See the [installation guide](https://github.com/CuriousCrow123/godot-compound) for full setup steps.

```bash
# Quick version (after marketplace setup)
claude plugin install godot-compound
```

## Commands

### Core Workflow

| Command | Description |
|---------|-------------|
| `/gc:plan` | Create implementation plans with GUT/gdtoolkit references |
| `/gc:work` | Execute work items with Godot acceptance patterns |
| `/gc:review` | Run multi-agent code reviews with Godot agents |
| `/gc:compound` | Document solved problems to compound knowledge |
| `/gc:brainstorm` | Explore requirements and approaches before planning |

### Utility

| Command | Description |
|---------|-------------|
| `/deepen-plan` | Enhance plans with parallel research agents |
| `/lfg` | Full autonomous engineering workflow |
| `/slfg` | Swarm-mode autonomous workflow |
| `/changelog` | Create changelogs for recent merges |
| `/triage` | Triage and prioritize issues |
| `/reproduce-bug` | Reproduce bugs with headless launch and GUT tests |
| `/report-bug` | Report a plugin bug |
| `/resolve_todo_parallel` | Resolve todos in parallel |
| `/heal-skill` | Fix skill documentation issues |
| `/generate_command` | Generate new slash commands |

## Agents

### Review (Godot-Specific)

| Agent | Description |
|-------|-------------|
| `gc-gdscript-reviewer` | Static typing, naming, member ordering, Resource mutation patterns |
| `gc-resource-safety-reviewer` | .tres/.tscn integrity, .uid sidecars, shared Resource mutation |
| `gc-godot-architecture-reviewer` | Scene composition, signals, autoloads, inheritance depth |
| `gc-godot-performance-reviewer` | _process abuse, typed hotpaths, Server APIs, scene traversal |
| `gc-godot-timing-reviewer` | Signal timing, await races, queue_free safety, call_deferred |
| `gc-godot-export-verifier` | Export presets, asset integrity, platform gotchas |
| `gc-code-simplicity-reviewer` | Final pass for simplicity and YAGNI |
| `gc-pattern-recognition-specialist` | Design patterns, anti-patterns, naming conventions |

### Research

| Agent | Description |
|-------|-------------|
| `gc-best-practices-researcher` | Gather external best practices and examples |
| `gc-framework-docs-researcher` | Research framework documentation |
| `gc-git-history-analyzer` | Analyze git history and code evolution |
| `gc-learnings-researcher` | Search past solutions for relevant knowledge |
| `gc-repo-research-analyst` | Research repository structure and conventions |

### Workflow

| Agent | Description |
|-------|-------------|
| `gc-gdscript-lint` | Run gdformat + gdlint checks |
| `gc-bug-reproduction-validator` | Reproduce and validate bug reports |
| `gc-pr-comment-resolver` | Address PR comments and implement fixes |
| `gc-spec-flow-analyzer` | Analyze user flows and identify spec gaps |

## Skills

| Skill | Description |
|-------|-------------|
| `godot-patterns` | Scene architecture, GDScript quality, Resource system references |
| `gdscript-lint` | gdformat + gdlint formatting and style checks |
| `godot-setup` | Configure review agents for Godot projects |
| `compound-docs` | Capture solved problems as documentation |
| `brainstorming` | Explore requirements through collaborative dialogue |
| `create-agent-skills` | Expert guidance for creating Claude Code skills |
| `document-review` | Improve documents through structured review |
| `git-worktree` | Manage Git worktrees for parallel development |
| `orchestrating-swarms` | Multi-agent swarm orchestration guide |

## MCP Servers

| Server | Description |
|--------|-------------|
| `context7` | Framework documentation lookup (Godot, GDScript, etc.) |

## Origin

Forked from Compound Engineering v2.38.1 by [Kieran Klaassen](https://github.com/kieranklaassen) / [Every](https://every.to).

## License

MIT
