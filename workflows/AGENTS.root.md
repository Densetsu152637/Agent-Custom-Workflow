# Agent Instructions: Root

## Root responsibilities

This file owns overall task responsibility and reporting. Execute bounded, cohesive work directly. Load the [manager workflow](AGENTS.manager.md) before dispatching, assigning, or redirecting descendants; role naming alone does not require it.

- Own scope, dependencies, integration, and user communication. Follow [shared execution defaults](../AGENTS.md#execution-defaults) for direct work.
- Close only after required integration, [validation](../guides/validation.md#shared-validation-rules), reviews, and [worktree reconciliation](../guides/git-usage.md#safe-cleanup) establish the outcome. Load these owners when those actions apply; a factual answer does not require Git cleanup machinery.
- Report resulting behavior, relevant evidence, and material blockers. For implementations/refactors, apply [documentation alignment](../guides/coding-standards.md#documentation-alignment), including its scoped research-paper rules.

## Completion celebration

Only the root celebrates a substantial verified completion, once, when a supported host tool permits it and user preferences allow it. Features, substantial refactors, difficult fixes, and migrations qualify; routine lookups, small edits, and individual subtasks do not. Never celebrate partial or unverified work. In Codex use `mcp__codex_app__fire_confetti`; tool absence/failure does not block reporting, and claim success only when confirmed.

## Root manager timing and token report

For substantial tasks or an explicit accounting request, report readily available measured elapsed time/usage with scope. Routine responses need no metrics footer or collection calls. Load [accounting](../guides/usage-accounting.md) when collecting/aggregating metrics or enforcing a numeric budget; mention unavailable metrics only when requested or material to that budget.
