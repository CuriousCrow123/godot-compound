# YAML Frontmatter Schema

**See `skills/compound-docs/schema.yaml` for the complete schema specification.**

## Required Fields

- **module** (string): Module name (e.g., "BattleSystem") or "System" for system-wide issues
- **date** (string): ISO 8601 date (YYYY-MM-DD)
- **problem_type** (enum): One of [parse_error, runtime_error, performance_issue, scene_corruption, resource_error, import_error, ui_bug, signal_issue, logic_error, integration_issue, developer_experience, workflow_issue, best_practice]
- **component** (enum): One of [scene_tree, resource_system, signal_wiring, physics_collision, animation_system, navigation, tilemap, audio, input_system, ui_controls, autoload, save_load, gdscript_tooling, project_config]
- **symptoms** (array): 1-5 specific observable symptoms
- **root_cause** (enum): One of [resource_sharing, uid_mismatch, scene_structure_invalid, node_path_fragile, signal_disconnected, autoload_order, untyped_code, logic_error, api_misuse, process_callback_abuse, config_error, import_cache_stale, missing_dependency]
- **resolution_type** (enum): One of [code_fix, scene_fix, config_change, resource_fix, dependency_update, environment_setup, workflow_improvement, architecture_change, pattern_adoption]
- **severity** (enum): One of [critical, high, medium, low]

## Optional Fields

- **godot_version** (string): Godot version in X.Y.Z format
- **tags** (array): Searchable keywords (lowercase, hyphen-separated)

## Validation Rules

1. All required fields must be present
2. Enum fields must match allowed values exactly (case-sensitive)
3. symptoms must be YAML array with 1-5 items
4. date must match YYYY-MM-DD format
5. godot_version (if provided) must match X.Y.Z format
6. tags should be lowercase, hyphen-separated

## Example

```yaml
---
module: BattleSystem
date: 2026-03-19
problem_type: resource_error
component: resource_system
symptoms:
  - "Shared Resource mutated across all instances"
  - "Enemy stats changing when player stats modified"
root_cause: resource_sharing
godot_version: 4.6.1
resolution_type: code_fix
severity: high
tags: [resource-sharing, duplicate, tres]
---
```

## Category Mapping

Based on `problem_type`, documentation is filed in:

- **parse_error** → `docs/solutions/parse-errors/`
- **runtime_error** → `docs/solutions/runtime-errors/`
- **performance_issue** → `docs/solutions/performance-issues/`
- **scene_corruption** → `docs/solutions/scene-corruption/`
- **resource_error** → `docs/solutions/resource-errors/`
- **import_error** → `docs/solutions/import-errors/`
- **ui_bug** → `docs/solutions/ui-bugs/`
- **signal_issue** → `docs/solutions/signal-issues/`
- **logic_error** → `docs/solutions/logic-errors/`
- **integration_issue** → `docs/solutions/integration-issues/`
- **developer_experience** → `docs/solutions/developer-experience/`
- **workflow_issue** → `docs/solutions/workflow-issues/`
- **best_practice** → `docs/solutions/best-practices/`
