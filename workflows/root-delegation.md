# Root delegation

Root/managers only; load at task intake. Leaves do not load this. Non-root managers use their own recursive-delegation policy.

## Delegation default

Apply at task intake, without waiting for the user to request subagents:

1. Answer directly only with trivial responses from existing knowledge and conversation context. Otherwise delegate substantive reasoning, analysis, synthesis, and design, even when existing context suffices and no tools are needed. Delegate all research, exploration, and tool-driven execution, even when the action is small or cohesive.
2. Perform only minimal routing discovery to identify independently ownable deliverables, dependencies, and applicable owners before choosing the worker count. Include planning and documentation deliverables; assign independent execution separately, not to one omnibus leaf. A critic complements component execution, not replaces it.
3. Give a concise inline routing checkpoint naming intended child assignments, or the applicable exception; it is not an approval gate. Select [manager or leaf](manager-delegation.md#manager-or-leaf-selection) per child and dispatch before substantive execution. Start ready independent assignments within the [shared concurrency allowance](manager-delegation.md#budgets-and-scheduling) before waiting; keep cohesive work together when no useful split exists.
4. Brief each child with the [context handoff](AGENTS.manager.md#context-handoff). Root retains coordination, review/integration, acceptance, and user communication; its tool use is limited to those and routing discovery. Subagents must own meaningful execution; no token delegation while root does the substantive work.

Exceptions: a user request requiring root to execute (including no-subagents), or delegation genuinely unavailable under host/task constraints; higher-priority restrictions also apply. Disclose when an exception limits delegation. Convenience, task size, and cohesion are not exceptions.

[Recursive delegation](manager-delegation.md#recursive-delegation) applies the same split to subagent managers. Root may assign a cohesive deliverable directly to a leaf or bounded manager; no extra manager layer is required. When assigning agents, report the model used to the user.
