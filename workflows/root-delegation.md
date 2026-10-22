# Root delegation

Root/managers only: load at task intake before substantive execution. Assigned leaves do not load this owner. Root-specific execution duties apply to root; non-root managers use their own recursive-delegation policy.

## Delegation default

Apply this decision at task intake, before substantive execution; do not wait for the user to request subagents:

1. Answer directly only with trivial responses from existing knowledge and conversation context. Otherwise delegate substantive reasoning, analysis, synthesis, and design, even when existing context suffices and no tools are needed. Delegate all research, exploration, and tool-driven execution, even when the action is small or cohesive.
2. Perform only minimal routing discovery needed to identify all useful independently ownable deliverables, dependencies, and applicable owners before selecting the number of workers. Include component planning and documentation deliverables; assign useful independent execution separately rather than to one omnibus leaf. A critic complements these assignments; it does not replace component execution.
3. Give a concise inline routing checkpoint naming intended child assignments and deliverables, or the concrete applicable exception. This checkpoint is not an approval gate: select [manager or leaf](manager-delegation.md#manager-or-leaf-selection) for each child and dispatch capable agents under the manager workflow before substantive execution. Start ready independent assignments within the [shared concurrency allowance](manager-delegation.md#budgets-and-scheduling) before waiting; keep cohesive work together when no useful independent split exists.
4. Brief each child with the [context handoff](AGENTS.manager.md#context-handoff). Retain coordination, review/integration, acceptance, and user communication. Root tool use is limited to those duties and minimal routing discovery. Subagents must own meaningful execution and deliverables; do not use token delegation while root performs the substantive work.

A user request explicitly requiring root to do the execution, including an explicit no-subagents instruction, is an exception. Unavailable delegation is an exception only when host or task constraints make it genuinely unavailable; higher-priority restrictions also apply. Disclose when an exception limits delegation or execution. Convenience, task size, and cohesion are not exceptions.

The [manager's recursive delegation rules](manager-delegation.md#recursive-delegation) require subagent managers to split independent deliverables automatically too, while permitting direct execution of cohesive work. Root can assign a cohesive deliverable directly to a leaf or a bounded manager; it does not require an extra manager layer for every assignment. When you assign agents report the model used to the user.
