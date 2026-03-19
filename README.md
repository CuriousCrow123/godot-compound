# Godot Compound

Godot 4 + GDScript development tools for Claude Code. Fork of [Compound Engineering](https://github.com/EveryInc/compound-engineering-plugin) v2.38.1, stripped of all web/Rails/TypeScript content.

## Installation

```bash
claude /plugin add /path/to/godot-compound
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
| `/report-bug` | Report a plugin bug |
| `/resolve_todo_parallel` | Resolve todos in parallel |
| `/resolve_parallel` | Resolve TODO comments in parallel |
| `/heal-skill` | Fix skill documentation issues |
| `/generate_command` | Generate new slash commands |

## Agents

### Review

| Agent | Description |
|-------|-------------|
| `gc-code-simplicity-reviewer` | Final pass for simplicity and minimalism |
| `gc-pattern-recognition-specialist` | Analyze code for patterns and anti-patterns |

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
| `gc-bug-reproduction-validator` | Reproduce and validate bug reports |
| `gc-pr-comment-resolver` | Address PR comments and implement fixes |
| `gc-spec-flow-analyzer` | Analyze user flows and identify spec gaps |

## Skills

| Skill | Description |
|-------|-------------|
| `brainstorming` | Explore requirements through collaborative dialogue |
| `compound-docs` | Capture solved problems as documentation |
| `create-agent-skills` | Expert guidance for creating Claude Code skills |
| `document-review` | Improve documents through structured review |
| `file-todos` | File-based todo tracking |
| `git-worktree` | Manage Git worktrees for parallel development |
| `orchestrating-swarms` | Multi-agent swarm orchestration guide |
| `resolve-pr-parallel` | Resolve PR comments in parallel |
| `setup` | Configure review agents for your project |

## MCP Servers

| Server | Description |
|--------|-------------|
| `context7` | Framework documentation lookup (Godot, GDScript, etc.) |

## Origin

Forked from Compound Engineering v2.38.1 by [Kieran Klaassen](https://github.com/kieranklaassen) / [Every](https://every.to).

## License

MIT
