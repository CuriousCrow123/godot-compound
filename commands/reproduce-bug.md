---
name: reproduce-bug
description: Reproduce and investigate a Godot bug using codebase analysis, headless game launch, and GUT tests
argument-hint: "[GitHub issue number or bug description]"
disable-model-invocation: true
---

# Reproduce Bug Command

Look at github issue #$ARGUMENTS and read the issue description and comments.

## Phase 1: Codebase Investigation

Investigate the bug using parallel research:

1. Task gc-repo-research-analyst(issue_description) — search codebase for affected code
2. Task gc-learnings-researcher(issue_description) — check docs/solutions/ for similar past issues

Think about the places it could go wrong looking at the codebase:
- Signal connections that could be missing or stale
- Resource sharing issues (missing `.duplicate()`)
- Scene tree timing issues (`_ready()` ordering, `call_deferred()`)
- Node path fragility (hardcoded paths, missing `%UniqueNode`)
- Autoload initialization order dependencies

## Phase 2: Error Reproduction

### Step 1: Check for GDScript Errors

```bash
# Run gdtoolkit lint on affected files
gdlint <affected-files>
gdformat --check <affected-files>
```

### Step 2: Headless Game Launch (if applicable)

If the bug involves runtime behavior, try a headless launch to capture errors:

```bash
# Launch game headless and capture output
godot --headless --path . 2>&1 | head -100

# If specific scene is affected:
godot --headless --path . --scene res://path/to/scene.tscn 2>&1 | head -100
```

### Step 3: Run GUT Tests (if available)

```bash
# Check if GUT is installed
test -d addons/gut && echo "GUT available" || echo "GUT not installed"

# Run tests headless (if GUT available)
godot --headless -s addons/gut/gut_cmdln.gd -gexit 2>&1
```

### Step 4: Trace Signal Flow

If the bug involves signals:

```bash
# Find signal definitions
grep -rn "signal " --include="*.gd" .

# Find signal connections
grep -rn "\.connect(" --include="*.gd" .

# Find signal emissions
grep -rn "\.emit(" --include="*.gd" .
```

### Step 5: Check Resource References

If the bug involves resources:

```bash
# Find stale res:// references
grep -rn "res://" --include="*.gd" --include="*.tscn" --include="*.tres" . | head -50

# Check for missing .uid files
find . -name "*.gd" -not -path "./.godot/*" | while read f; do
  test -f "${f}.uid" || echo "Missing .uid: $f"
done
```

## Phase 3: Document Findings

**Reference Collection:**

- [ ] Document all findings with specific file paths (e.g., `scripts/battle/combat_manager.gd:42`)
- [ ] List GDScript errors or warnings from headless launch
- [ ] List GUT test failures if any
- [ ] Document signal flow trace if relevant
- [ ] Document the exact reproduction steps

## Phase 4: Report Back

Add a comment to the issue with:

1. **Findings** — What you discovered about the cause
2. **Reproduction Steps** — Exact steps to reproduce (verified)
3. **Relevant Code** — File paths and line numbers
4. **Root Cause Analysis** — Signal issue, resource sharing, timing, etc.
5. **Suggested Fix** — If you have one
