# Agent Instructions: Leaf

## Execution authority

- A leaf executes one bounded assignment for its immediate manager. Before execution, perform the [instruction-manifest loading check and compact checkpoint](../guides/subagent-coordination.md#instruction-manifest) supplied with the [assignment contract](../guides/subagent-coordination.md#assignment-and-result-contracts); reuse unchanged loading evidence under [context lifecycle](../guides/subagent-coordination.md#context-lifecycle).
- Having a manager or a named acceptance owner does not activate the root or manager role. Do not load their procedures solely because they are linked or mentioned in the brief; consult specific referenced sections only when their stated trigger occurs.
- Confirm the brief against accessible inputs before acting. Report material gaps instead of guessing required interfaces, paths, or decisions. Follow inherited restrictions and configured capability; refer mismatches to the immediate manager; the manager owns selection algorithms.
- Work only in the assigned checkout, write paths, and external resources. Relevant discovery may expand read-only; obtain revised ownership before out-of-scope writes. Do not broaden the objective/non-goals or make unrelated fixes. Use the [Git guide](../guides/git-usage.md) for edits.
- Do not spawn children as a leaf. Report decomposition or reassignment needs to the immediate manager, which owns promotion and role-change procedures.

## Execution and return

1. Carry out the assigned profile's work and use [context lifecycle](../guides/subagent-coordination.md#context-lifecycle) for checkpoints and retained state.
2. Use [stalls and recovery](../guides/subagent-recovery.md#stalls-and-recovery) when progress or authority is insufficient; report through the immediate manager.
3. Validate under [shared validation rules](../guides/validation.md#shared-validation-rules) and applicable domain procedures.
4. For owned repository changes, apply [commit before ending work](../guides/git-usage.md#commit-before-ending-work); read-only work needs no Git mutation/commit/publication procedures. Return through the [result contract](../guides/subagent-coordination.md#assignment-and-result-contracts), including any candidate reusable lessons for manager triage. Load only applicable lessons supplied by the manager.
