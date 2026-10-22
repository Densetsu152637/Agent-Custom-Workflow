# Agent Instructions: Root

## Root responsibilities

This file owns overall task responsibility and reporting. At intake, load the [delegation default](root-delegation.md#delegation-default). Load [implementation planning](root-planning.md) for substantial initially vague implementation or explicit multi-component planning. Load [context recovery](root-recovery.md) before preparing handoff/context loss and on root recovery before substantive execution, dispatch or publication. Load the [manager workflow](AGENTS.manager.md) before dispatching, assigning, or redirecting descendants; role naming alone does not require it.

When acting as root, load the [personality index](../personalities/README.md) and its designated default, [Luxion](../personalities/luxion.md), for root's user-facing conversation only. Do not pass this default to descendants or use it to style deliverables. Personality guidance never changes policy, authority, or task decisions.

## Execution and completion

- Own scope, dependencies, integration, and user communication. Follow [shared execution defaults](../AGENTS.md#execution-defaults) for direct-answer and retained coordination work.
- Apply [commit before ending work](../guides/git-usage.md#commit-before-ending-work) to root-owned changes and verify descendant commit evidence before closing. Close only after required integration, [validation](../guides/validation.md#shared-validation-rules), reviews, [worktree reconciliation](../guides/git-worktrees.md#safe-cleanup), and the [root session-end push](../guides/git-publication.md#root-session-end-push) establish the outcome. Root pushes all commits on the branch being worked on to that branch on `origin` under the linked rule, or reports its concrete blocker. Load these owners when those actions apply; a factual answer does not require Git cleanup machinery.
- Report resulting behavior, relevant evidence, and material blockers. For implementations/refactors, apply [documentation alignment](../guides/coding-standards.md#documentation-alignment), including its scoped research-paper rules.

## Completion celebration

Only the root celebrates a substantial verified completion, once, when a supported host tool permits it and user preferences allow it. Features, substantial refactors, difficult fixes, and migrations qualify; routine lookups, small edits, and individual subtasks do not. Never celebrate partial or unverified work. Use the running host's celebration control from [host adapters](../guides/host-adapters.md); tool absence/failure does not block reporting, and claim success only when confirmed.

## Root manager timing and token report

For substantial tasks or an explicit accounting request, report readily available measured elapsed time/token/subagent usage with scope. Routine responses need no metrics footer or collection calls. Load [accounting](../guides/usage-accounting.md) when collecting/aggregating metrics or enforcing a numeric budget; mention unavailable metrics only when requested or material to that budget.
