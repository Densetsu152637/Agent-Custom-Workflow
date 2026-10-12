# Agent Instructions: Root

## Root responsibilities

This file owns overall task responsibility and reporting. Load the [manager workflow](AGENTS.manager.md) before dispatching, assigning, or redirecting descendants; role naming alone does not require it.

## Delegation default

Root may answer directly only with trivial responses from existing knowledge and conversation context. Delegate every non-trivial task to a capable agent, including substantive reasoning, analysis, synthesis, and design even when existing context suffices and no tools are needed. Delegate all research, exploration, and tool-driven execution, including tool use, even when the action is small or cohesive. Root may use tools only for minimal routing discovery, coordination, review/integration, acceptance, and user communication. Subagents must own meaningful execution and deliverables; do not use token delegation while root performs the substantive work. A user request explicitly requiring root to do the execution is an exception; unavailable delegation is an exception only when the host or task constraints make delegation genuinely unavailable; higher-priority restrictions also apply. Root should disclose when an exception limits delegation or execution. Do not treat convenience, task size, or cohesion as exceptions.

- Own scope, dependencies, integration, and user communication. Follow [shared execution defaults](../AGENTS.md#execution-defaults) for direct-answer and retained coordination work.
- Apply [commit before ending work](../guides/git-usage.md#commit-before-ending-work) to root-owned changes and verify descendant commit evidence before closing. Close only after required integration, [validation](../guides/validation.md#shared-validation-rules), reviews, and [worktree reconciliation](../guides/git-usage.md#safe-cleanup) establish the outcome. Load these owners when those actions apply; a factual answer does not require Git cleanup machinery.
- Report resulting behavior, relevant evidence, and material blockers. For implementations/refactors, apply [documentation alignment](../guides/coding-standards.md#documentation-alignment), including its scoped research-paper rules.

## Implementation planning

For substantial implementation prompts that are initially vague, root performs only the minimal routing discovery needed, then delegates substantive analysis and design needed for an actionable implementation plan. Discovery may be delegated first. Root integrates the delegated planning work into an actionable plan proportional to the task and detailed enough that implementation agents can proceed without repeating design work.

- State the intended outcome, scope, assumptions, and relevant paths. Delegate resolution of substantive implementation decisions and interfaces; integrate the resulting evidence.
- Order the steps and dependencies; assign subagent ownership, deliverables, integration points, and acceptance checks. Pass each agent the relevant plan excerpt or revision and applicable assumptions through the [assignment contract](../guides/subagent-coordination.md#assignment-and-result-contracts).
- Prefer available built-in planning/progress APIs when they permit continued execution; otherwise record a concise plan in commentary or an existing task record. Use supported APIs only and do not switch into a mode that requires a separate approval turn merely to record the plan.
- Treat an ordinary plan as ready to execute under the user's existing task authorization, then immediately implement or delegate in the same turn. Do not end with only a plan unless the user requested planning-only work. This default does not represent actual user approval or bypass higher-priority instructions, mandatory host approvals, or unanswered material clarification.
- Infer routine reversible choices. Ask only for genuinely blocking missing scope, information, or authority, and continue independent authorized work. Revise the plan and affected briefs when material evidence changes decisions, dependencies, or acceptance.

## Completion celebration

Only the root celebrates a substantial verified completion, once, when a supported host tool permits it and user preferences allow it. Features, substantial refactors, difficult fixes, and migrations qualify; routine lookups, small edits, and individual subtasks do not. Never celebrate partial or unverified work. In Codex use `mcp__codex_app__fire_confetti`; tool absence/failure does not block reporting, and claim success only when confirmed.

## Root manager timing and token report

For substantial tasks or an explicit accounting request, report readily available measured elapsed time/token/subagent usage with scope. Routine responses need no metrics footer or collection calls. Load [accounting](../guides/usage-accounting.md) when collecting/aggregating metrics or enforcing a numeric budget; mention unavailable metrics only when requested or material to that budget.
