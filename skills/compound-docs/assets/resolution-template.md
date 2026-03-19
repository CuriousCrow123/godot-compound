---
module: [Module name or "System" for system-wide]
date: [YYYY-MM-DD]
problem_type: [parse_error|runtime_error|performance_issue|scene_corruption|resource_error|import_error|ui_bug|signal_issue|logic_error|integration_issue]
component: [scene_tree|resource_system|signal_wiring|physics_collision|animation_system|navigation|tilemap|audio|input_system|ui_controls|autoload|save_load|gdscript_tooling|project_config]
symptoms:
  - [Observable symptom 1 - specific error message or behavior]
  - [Observable symptom 2 - what user actually saw/experienced]
root_cause: [resource_sharing|uid_mismatch|scene_structure_invalid|node_path_fragile|signal_disconnected|autoload_order|untyped_code|logic_error|api_misuse|process_callback_abuse|config_error|import_cache_stale|missing_dependency]
godot_version: [4.6.1 - optional]
resolution_type: [code_fix|scene_fix|config_change|resource_fix|dependency_update|environment_setup|workflow_improvement|architecture_change]
severity: [critical|high|medium|low]
tags: [keyword1, keyword2, keyword3]
---

# Troubleshooting: [Clear Problem Title]

## Problem
[1-2 sentence clear description of the issue and what the user experienced]

## Environment
- Module: [Name or "System-wide"]
- Godot Version: [e.g., 4.6.1]
- Affected Component: [e.g., "BattleScene scene tree", "SaveManager autoload", "PlayerStats resource"]
- Date: [YYYY-MM-DD when this was solved]

## Symptoms
- [Observable symptom 1 - what the user saw/experienced]
- [Observable symptom 2 - error messages, visual issues, unexpected behavior]
- [Continue as needed - be specific]

## What Didn't Work

**Attempted Solution 1:** [Description of what was tried]
- **Why it failed:** [Technical reason this didn't solve the problem]

**Attempted Solution 2:** [Description of second attempt]
- **Why it failed:** [Technical reason]

[Continue for all significant attempts that DIDN'T work]

[If nothing else was attempted first, write:]
**Direct solution:** The problem was identified and fixed on the first attempt.

## Solution

[The actual fix that worked - provide specific details]

**Code changes** (if applicable):
```gdscript
# Before (broken):
[Show the problematic code]

# After (fixed):
[Show the corrected code with explanation]
```

**Scene changes** (if applicable, describe manually):
```
# Scene modification:
[Describe what was changed in the scene tree — do not edit .tscn directly]
```

**Commands run** (if applicable):
```bash
# Steps taken to fix:
[Commands or actions]
```

## Why This Works

[Technical explanation of:]
1. What was the ROOT CAUSE of the problem?
2. Why does the solution address this root cause?
3. What was the underlying issue (API misuse, configuration error, Godot version issue, etc.)?

[Be detailed enough that future developers understand the "why", not just the "what"]

## Prevention

[How to avoid this problem in future development:]
- [Specific coding practice, check, or pattern to follow]
- [What to watch out for]
- [How to catch this early]

## Related Issues

[If any similar problems exist in docs/solutions/, link to them:]
- See also: [another-related-issue.md](../category/another-related-issue.md)
- Similar to: [related-problem.md](../category/related-problem.md)

[If no related issues, write:]
No related issues documented yet.
