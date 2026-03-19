# Changelog

All notable changes to godot-compound will be documented in this file.

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
