# Export & Build Patterns in Godot 4

Reference file for gc-godot-export-verifier agent. Compiled from GitHub issues, forum threads, and official documentation.

## Resources Loaded via DirAccess Are Not Tracked

Resources loaded by scanning directories with `DirAccess` + string concatenation are NOT tracked by the export system. They won't be included in the exported build unless explicitly added to export filters or referenced via `preload()`.

Source: Godot forums, #84401

**Mitigation:** Add directory patterns to export filters: `*.tres`, `*.json`, etc. Or reference resources via `preload()` which is tracked.

## Custom Resources Fail After Export (Circular Dependencies)

Custom Resource classes with circular dependencies (Resource A references Resource B which references Resource A) can fail to load after export. Works in the editor because the editor resolves classes differently than the exported runtime.

Source: #77007, #80877 (meta-tracker)

**Mitigation:** Avoid circular Resource references. If needed, use string paths instead of direct Resource references to break the cycle.

## Missing Assets — Works in Editor, Crashes in Export

Resources that exist in the project but aren't referenced by any scene or script may be excluded from export. This is especially common with:
- Resources loaded dynamically via `load()` with computed paths
- Assets in directories not covered by export filters
- Import files without corresponding source files

Source: #86317

**Mitigation:** Use export resource filters to explicitly include directories. Test exports early and often.

## Platform-Specific Gotchas

### Case Sensitivity
Windows is case-insensitive, but Android and Linux are case-sensitive. `load("res://Sprites/Player.png")` works on Windows but fails on Linux if the file is `sprites/player.png`.

Source: #86317 forum discussion

### .remap Suffix for Dynamic Loading
After export, imported resources get a `.remap` suffix. Code using `DirAccess` to list files must account for this: `file.get_basename()` to strip the `.remap` extension.

### SharedArrayBuffer for Web + Threads
Web exports using threads require `SharedArrayBuffer`, which needs specific HTTP headers (`Cross-Origin-Opener-Policy: same-origin`, `Cross-Origin-Embedder-Policy: require-corp`). Without these headers, threading silently fails.

### Android Export Breakage on Version Upgrades
Upgrading Godot versions can break Android export presets. Keystore paths, SDK references, and gradle configurations may need manual updates.

Source: #108805

## .uid Sidecar Dropped on External Rename

Renaming files outside the Godot editor (e.g., via terminal or git) can delete the old `.uid` sidecar without creating a new one. This breaks UID-based references.

Source: #104188, fixed in PR #104248 (Godot 4.5)

**Mitigation:** Always rename files through the Godot editor, or manually move `.uid` files after external renames.

## Export Preset Configuration Checklist

Common export preset issues:
1. **Export path not set** — preset exists but no output path configured
2. **Resource filters missing** — dynamic resources not included
3. **Feature flags mismatch** — debug features enabled in release export
4. **Icon/splash not set** — platform requires specific icon sizes
5. **Encryption key not set** — if script encryption is desired
6. **Custom user directory** — `project/application/config/custom_user_dir_name` not set for production

## Scene Reference Completeness

Every `res://` path in the project must resolve to an actual file. After file moves or deletions:
- Check all `.tscn` files for stale `ext_resource` paths
- Check all `.tres` files for stale `Resource` references
- Check `project.godot` for stale autoload paths
- Check export presets for stale paths in filters
