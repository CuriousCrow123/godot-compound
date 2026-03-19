# Changelog

All notable changes to godot-compound will be documented in this file.

## [0.2.0] - 2026-03-19

### Added
- **gc-gdscript-reviewer** — Reviews .gd files for static typing, member ordering, naming, signal naming, Resource mutation patterns (8 principles)
- **gc-resource-safety-reviewer** — Reviews resource integrity: .tres/.tscn references, .uid sidecars, shared Resource mutation, res:// path safety (8 principles)
- **gc-gdscript-lint** — Runs gdformat + gdlint checks (model: haiku)
- **gc-godot-architecture-reviewer** — Reviews scene composition, signal flow, autoloads, inheritance depth (7 principles)
- **gc-godot-performance-reviewer** — Reviews _process abuse, typed hotpaths, scene traversal costs, Server APIs (7 principles)
- **gc-godot-timing-reviewer** — Reviews signal timing, await races, queue_free safety, call_deferred ordering (7 principles)
- **gc-godot-export-verifier** — Verifies export presets, asset integrity, platform gotchas, .uid consistency (7 principles)
- **gdscript-lint skill** — Skill wrapper for gdformat/gdlint with disable-model-invocation
- **timing-async.md** — Reference file for timing/async patterns (godot-patterns skill)
- **export-builds.md** — Reference file for export/build patterns (godot-patterns skill)

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
