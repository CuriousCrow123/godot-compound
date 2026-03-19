# Changelog

All notable changes to godot-compound will be documented in this file.

## [0.3.0] - 2026-03-19

### Added — Phase 5: Integration & Polish
- **reproduce-bug** command rewritten for Godot (headless launch, GUT tests, signal tracing)
- **godot-setup** skill with GUT/gdtoolkit detection and all Godot agents
- **godot-patterns** skill with 5 reference files (scene-architecture, gdscript-quality, resource-system, timing-async, export-builds)
- `schema_version: 1` and `node_types` field in compound-godot schema
- README with full agent inventory and installation guide

### Changed
- All remaining `compound-engineering` references → `godot-compound`
- MCP tool references updated to `mcp__plugin_godot-compound_context7__*`
- Resolution template frontmatter aligned with schema.yaml enums
- `report-bug` fully updated for godot-compound repo
- `deepen-plan` plugin discovery paths updated

### Fixed
- gc-gdscript-lint model changed from haiku to sonnet (user preference)

## [0.2.0] - 2026-03-19

### Added — Phase 3: Godot Review Agents
- **gc-gdscript-reviewer** — Static typing, naming, member ordering, Resource mutation (8 principles)
- **gc-resource-safety-reviewer** — .tres/.tscn integrity, .uid sidecars, shared mutation (8 principles)
- **gc-gdscript-lint** — gdformat + gdlint checks (model: sonnet)
- **gc-godot-architecture-reviewer** — Scene composition, signals, autoloads, inheritance (7 principles)
- **gc-godot-performance-reviewer** — _process abuse, typed hotpaths, Server APIs (7 principles)
- **gc-godot-timing-reviewer** — Signal timing, await races, queue_free safety (7 principles)
- **gc-godot-export-verifier** — Export presets, asset integrity, platform gotchas (7 principles)
- **gdscript-lint** skill wrapper with disable-model-invocation
- **timing-async.md** and **export-builds.md** reference files

## [0.1.0] - 2026-03-19

### Added
- Initial fork from Compound Engineering v2.38.1
- Plugin metadata (`plugin.json`) for godot-compound
- Plugin CLAUDE.md with Godot conventions (inherited by all agents)
- `/gc:` command namespace for all core workflow commands

### Changed
- All 10 kept agents renamed with `gc-` prefix to avoid CE name collisions
- All `/ce:` references updated to `/gc:`
- `report-bug` command points to godot-compound repo

### Removed
- 19 web-specific agents (Rails, TypeScript, Python, Figma, database, security reviewers)
- 11 web-specific skills (agent-browser, DHH-rails, frontend-design, gemini-imagegen, etc.)
- 6 web-specific commands (test-browser, test-xcode, feature-video, agent-native-audit, deploy-docs, create-agent-skill)
- Deprecated `commands/workflows/` aliases
- `agents/design/` and `agents/docs/` directories (all contents removed)

### Origin
- Forked from [Compound Engineering](https://github.com/EveryInc/compound-engineering-plugin) v2.38.1 by Kieran Klaassen / Every
