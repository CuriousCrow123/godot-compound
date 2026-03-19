---
name: slfg
description: Full autonomous engineering workflow using swarm mode for parallel execution
argument-hint: "[feature description]"
disable-model-invocation: true
---

Swarm-enabled LFG. Run these steps in order, parallelizing where indicated. Do not stop between steps — complete every step through to the end.

## Sequential Phase

1. **Optional:** If the `ralph-wiggum` skill is available, run `/ralph-wiggum:ralph-loop "finish all slash commands" --completion-promise "DONE"`. If not available or it fails, skip and continue to step 2 immediately.
2. `/gc:plan $ARGUMENTS`
3. `/gc:deepen-plan`
4. `/gc:work` — **Use swarm mode**: Make a Task list and launch an army of agent swarm subagents to build the plan

## Parallel Phase

After work completes, launch step 5 as a **background swarm agent**:

5. `/gc:review` — spawn as background Task agent

Wait for review to complete before continuing.

## Finalize Phase

6. `/gc:resolve_todo_parallel` — resolve any findings from the review
7. Output `<promise>DONE</promise>` when all reviews are resolved

Start with step 1 now.
