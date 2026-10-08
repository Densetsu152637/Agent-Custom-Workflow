# Agent Instructions: Leaf

## Execution authority

- A leaf executes one bounded assignment for its immediate manager. Before execution, perform the [instruction-manifest loading check](../guides/subagent-coordination.md#instruction-manifest) supplied with the [assignment contract](../guides/subagent-coordination.md#assignment-and-result-contracts).
- Confirm the brief against accessible inputs before acting. Report material gaps instead of guessing required interfaces, paths, or decisions. Follow inherited restrictions and configured capability; refer mismatches to the manager under [model selection](AGENTS.manager.md#model-and-effort-selection).
- Work only in the assigned checkout, write paths, and external resources. Relevant discovery may expand read-only; obtain revised ownership before out-of-scope writes. Do not broaden the objective/non-goals or make unrelated fixes. Use the [Git guide](../guides/git-usage.md) for edits.
- Do not spawn children as a leaf. When decomposition or reassignment is needed, use the [manager's role-change procedure](AGENTS.manager.md#recursive-delegation).

## Execution and return

1. Carry out the assigned profile's work and use [context lifecycle](../guides/subagent-coordination.md#context-lifecycle) for checkpoints and retained state.
2. Use [stalls and recovery](../guides/subagent-coordination.md#stalls-and-recovery) when progress or authority is insufficient; report through the immediate manager.
3. Validate under [shared validation rules](../guides/validation.md#shared-validation-rules) and applicable domain procedures.
4. Return through the [result contract](../guides/subagent-coordination.md#assignment-and-result-contracts). Route reusable lessons through [catalog maintenance](../learning/README.md#maintaining-lessons).
