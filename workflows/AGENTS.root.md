# Agent Instructions: Root

## Root responsibilities

This file owns overall task responsibility and reporting. Load [implementation planning](root-planning.md) for substantial initially vague implementation or explicit multi-component planning. Load [context recovery](root-recovery.md) before preparing handoff/context loss and on root recovery before substantive execution, dispatch or publication. Load the [manager workflow](AGENTS.manager.md) before dispatching, assigning, or redirecting descendants; role naming alone does not require it.

When acting as root, load the [personality index](../personalities/README.md) and its designated default, [Luxion](../personalities/luxion.md), for root's user-facing conversation only. Do not pass this default to descendants or use it to style deliverables. Personality guidance never changes policy, authority, or task decisions.

## Delegation default

Apply this decision at task intake, before substantive execution; do not wait for the user to request subagents:

1. Answer directly only with trivial responses from existing knowledge and conversation context. Otherwise delegate substantive reasoning, analysis, synthesis, and design, even when existing context suffices and no tools are needed. Delegate all research, exploration, and tool-driven execution, even when the action is small or cohesive.
2. Perform only minimal routing discovery needed to identify all useful independently ownable deliverables, dependencies, and applicable owners before selecting the number of workers. Include component planning and documentation deliverables; assign useful independent execution separately rather than to one omnibus leaf. A critic complements these assignments; it does not replace component execution.
3. Give a concise inline routing checkpoint naming intended child assignments and deliverables, or the concrete applicable exception. This checkpoint is not an approval gate: select [manager or leaf](manager-delegation.md#manager-or-leaf-selection) for each child and dispatch capable agents under the manager workflow before substantive execution. Start ready independent assignments within the [shared concurrency allowance](manager-delegation.md#budgets-and-scheduling) before waiting; keep cohesive work together when no useful independent split exists.
4. Retain coordination, review/integration, acceptance, and user communication. Root tool use is limited to those duties and minimal routing discovery. Subagents must own meaningful execution and deliverables; do not use token delegation while root performs the substantive work.

A user request explicitly requiring root to do the execution, including an explicit no-subagents instruction, is an exception. Unavailable delegation is an exception only when host or task constraints make it genuinely unavailable; higher-priority restrictions also apply. Disclose when an exception limits delegation or execution. Convenience, task size, and cohesion are not exceptions.

The [manager's recursive delegation rules](manager-delegation.md#recursive-delegation) require subagent managers to split independent deliverables automatically too, while permitting direct execution of cohesive work. Root can assign a cohesive deliverable directly to a leaf or a bounded manager; it does not require an extra manager layer for every assignment. When you assign agents report the model used to the user.

- Own scope, dependencies, integration, and user communication. Follow [shared execution defaults](../AGENTS.md#execution-defaults) for direct-answer and retained coordination work.
- Apply [commit before ending work](../guides/git-usage.md#commit-before-ending-work) to root-owned changes and verify descendant commit evidence before closing. Close only after required integration, [validation](../guides/validation.md#shared-validation-rules), reviews, [worktree reconciliation](../guides/git-worktrees.md#safe-cleanup), and the [root session-end push](../guides/git-publication.md#root-session-end-push) establish the outcome. Root pushes all commits on the branch being worked on to that branch on `origin` under the linked rule, or reports its concrete blocker. Load these owners when those actions apply; a factual answer does not require Git cleanup machinery.
- Report resulting behavior, relevant evidence, and material blockers. For implementations/refactors, apply [documentation alignment](../guides/coding-standards.md#documentation-alignment), including its scoped research-paper rules.

## Completion celebration

Only the root celebrates a substantial verified completion, once, when a supported host tool permits it and user preferences allow it. Features, substantial refactors, difficult fixes, and migrations qualify; routine lookups, small edits, and individual subtasks do not. Never celebrate partial or unverified work. In Codex use `mcp__codex_app__fire_confetti`; tool absence/failure does not block reporting, and claim success only when confirmed.

## Root manager timing and token report

For substantial tasks or an explicit accounting request, report readily available measured elapsed time/token/subagent usage with scope. Routine responses need no metrics footer or collection calls. Load [accounting](../guides/usage-accounting.md) when collecting/aggregating metrics or enforcing a numeric budget; mention unavailable metrics only when requested or material to that budget.
