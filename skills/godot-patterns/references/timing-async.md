# Timing & Async Patterns in Godot 4

Reference file for gc-godot-timing-reviewer agent. Compiled from GitHub issues, forum threads, and official documentation.

## Signal Emission in _ready()

Emitting signals in `_ready()` is unsafe because sibling nodes and parent nodes may not have completed their own `_ready()` yet. Listeners connected in a parent's `_ready()` will miss signals emitted by children during their `_ready()`.

**Mitigation:** Use `call_deferred()` to delay emission until the current frame's tree processing completes.

```gdscript
# Unsafe — listeners may not be connected yet
func _ready() -> void:
    initialized.emit()

# Safe — deferred to after tree is ready
func _ready() -> void:
    initialized.emit.call_deferred()
```

Source: Godot docs (signal connection best practices), GDQuest Signals Best Practices

## await Race Conditions

GDScript coroutines (`await`) suspend execution and resume later. If the awaited object is freed or the scene changes during suspension, the coroutine resumes in an invalid state.

**Common patterns:**
- `await get_tree().create_timer(1.0).timeout` — safe if node stays in tree
- `await target.animation_finished` — unsafe if `target` is freed during wait
- `await some_signal` in `_ready()` — blocks `_ready()` completion, delaying children

**Guard pattern:**
```gdscript
await get_tree().create_timer(1.0).timeout
if not is_instance_valid(target):
    return
```

Source: gdscript.com coroutine guide, community patterns

## queue_free() with Active Coroutines

Calling `queue_free()` on a node with an active coroutine does NOT immediately cancel the coroutine. The coroutine runs one more frame after `queue_free()` is called, potentially accessing freed resources.

Source: Godot #93608

**Mitigation:** Set a flag before `queue_free()` and check it in the coroutine:
```gdscript
var _is_freeing: bool = false

func die() -> void:
    _is_freeing = true
    queue_free()

func _some_coroutine() -> void:
    await get_tree().create_timer(0.5).timeout
    if _is_freeing:
        return
    # ... continue
```

## Deferred Call Execution Timing

`call_deferred()` schedules a call for "later in the frame," but the exact timing is not documented. The Godot docs do not specify WHEN deferred calls execute relative to `_process()`, `_physics_process()`, signals, and tree notifications.

Source: godot-docs #6488 (still open as of 2026-03)

**Practical guidance:** Deferred calls execute after the current notification/callback stack unwinds, before the next frame. Don't depend on ordering between multiple deferred calls.

## _process vs _unhandled_input Ordering

Within a single frame, Godot processes in this order:
1. `_input()` — raw input events
2. `_unhandled_input()` — input not consumed by GUI
3. `_process()` — per-frame logic
4. `_physics_process()` — fixed-step physics

Input callbacks fire before process callbacks in the same frame. Code that reads input state in `_process()` gets the result of input processed earlier in the same frame.

## Autoload Initialization Order

Autoloads initialize in the order they appear in Project Settings → Autoload list. If Autoload B depends on Autoload A, A must be listed first. There is no dependency declaration mechanism — order is purely positional.

**Risk:** Reordering autoloads in project settings silently breaks dependencies.

## Signal Connections on Dynamic Nodes

Connecting to signals on dynamically created nodes creates a reference. If the node is freed with `queue_free()` without disconnecting, the connection becomes dangling. Built-in signals auto-disconnect on free, but custom signals connected with `CONNECT_REFERENCE_COUNTED` do not always clean up in all cases.

**Best practice:** Disconnect in `_exit_tree()` if the signal source may outlive the listener.

## call_group() + queue_free() Reliability

`get_tree().call_group("mobs", "queue_free")` is unreliable without a frame wait. The group iteration may skip nodes that are freed during iteration, or process nodes after they're queued for deletion.

Source: godot-docs #11717

**Mitigation:** Process in reverse or collect nodes first:
```gdscript
var mobs: Array[Node] = get_tree().get_nodes_in_group("mobs")
for mob in mobs:
    mob.queue_free()
```
