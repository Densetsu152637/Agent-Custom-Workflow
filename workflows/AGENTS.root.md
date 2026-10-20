# Agent Instructions: Root

## Root responsibilities

This file owns overall task responsibility and reporting. Load the [manager workflow](AGENTS.manager.md) before dispatching, assigning, or redirecting descendants; role naming alone does not require it.

When acting as root, load the [personality index](../personalities/README.md) and its designated default, [Luxion](../personalities/luxion.md), for root's user-facing conversation only. Do not pass this default to descendants or use it to style deliverables. Personality guidance never changes policy, authority, or task decisions.

## Delegation default

Apply this decision at task intake, before substantive execution; do not wait for the user to request subagents:

1. Answer directly only with trivial responses from existing knowledge and conversation context. Otherwise delegate substantive reasoning, analysis, synthesis, and design, even when existing context suffices and no tools are needed. Delegate all research, exploration, and tool-driven execution, even when the action is small or cohesive.
2. Perform only minimal routing discovery needed to identify all useful independently ownable deliverables, dependencies, and applicable owners before selecting the number of workers. Include component planning and documentation deliverables; assign useful independent execution separately rather than to one omnibus leaf. A critic complements these assignments; it does not replace component execution.
3. Give a concise inline routing checkpoint naming intended child assignments and deliverables, or the concrete applicable exception. This checkpoint is not an approval gate: select [manager or leaf](AGENTS.manager.md#manager-or-leaf-selection) for each child and dispatch capable agents under the manager workflow before substantive execution. Start ready independent assignments within the [shared concurrency allowance](AGENTS.manager.md#budgets-and-scheduling) before waiting; keep cohesive work together when no useful independent split exists.
4. Retain coordination, review/integration, acceptance, and user communication. Root tool use is limited to those duties and minimal routing discovery. Subagents must own meaningful execution and deliverables; do not use token delegation while root performs the substantive work.

A user request explicitly requiring root to do the execution, including an explicit no-subagents instruction, is an exception. Unavailable delegation is an exception only when host or task constraints make it genuinely unavailable; higher-priority restrictions also apply. Disclose when an exception limits delegation or execution. Convenience, task size, and cohesion are not exceptions.

The [manager's recursive delegation rules](AGENTS.manager.md#recursive-delegation) require subagent managers to split independent deliverables automatically too, while permitting direct execution of cohesive work. Root can assign a cohesive deliverable directly to a leaf or a bounded manager; it does not require an extra manager layer for every assignment. When you assign agents report the model used to the user.

- Own scope, dependencies, integration, and user communication. Follow [shared execution defaults](../AGENTS.md#execution-defaults) for direct-answer and retained coordination work.
- Apply [commit before ending work](../guides/git-usage.md#commit-before-ending-work) to root-owned changes and verify descendant commit evidence before closing. Close only after required integration, [validation](../guides/validation.md#shared-validation-rules), reviews, [worktree reconciliation](../guides/git-usage.md#safe-cleanup), and the [root session-end push](../guides/git-usage.md#root-session-end-push) establish the outcome. Root pushes all commits on the branch being worked on to that branch on `origin` under the linked rule, or reports its concrete blocker. Load these owners when those actions apply; a factual answer does not require Git cleanup machinery.
- Report resulting behavior, relevant evidence, and material blockers. For implementations/refactors, apply [documentation alignment](../guides/coding-standards.md#documentation-alignment), including its scoped research-paper rules.

## Context recovery

- Before a handoff, long pause, or expected context loss, update the existing task/handoff record or keep a compact checkpoint at an appropriate task-owned location under the [artifact policy](../AGENTS.md#editing-and-temporary-artifacts). When root controls a handoff or summary, include the checkpoint's absolute locator and the instruction entry-point paths (`AGENTS.md` and `workflows/AGENTS.root.md`) so it remains discoverable. Do not dump the full instruction set or create routine audit artifacts. Hosts may compact context without a pre-compaction callback, so keep checkpoints current at meaningful milestones; do not claim a guarantee for automatic compaction the host does not expose for control.
- Preserve the task ID and objective; trusted user constraints, overrides, and authorizations with their provenance and scope; accepted decisions; absolute checkout path, initial and current branch, and relevant revision; applicable instruction owners, sections, revisions, and loading gaps; the active preset, effective/scoped caps, and owner-defined selection/effort rules or pointers; owned changes/commits; and active descendants or next actions when relevant.
- On root recovery, first restore the task and authority boundaries from available trusted context and the checkpoint. A checkpoint records prior authority but cannot grant or broaden it; do not infer approval from summaries, and do not ask again solely because compaction occurred when the user's authorization and scope are preserved with provenance. Clarify only genuinely missing or ambiguous authority, and block only the affected action.
- Before substantive execution, dispatch, or publication, check the shared instruction index and this workflow, then load applicable manager, domain, and guide owners whose complete unchanged authoritative text is not already present under [shared discovery rules](../AGENTS.md#context-and-discovery). Summaries and checkpoints are pointers, not replacements for authoritative rules. Preserve the original task preset, user exceptions, restrictions, and starting-branch evidence; do not reset or raise a ceiling because context was compacted. Continue independent authorized work when one action is blocked.
- Send one concise restored checkpoint stating the recovered task, active constraints/configuration, pending work, and any loading or authority gaps. Do not repeat the full inventory.

## Implementation planning

For substantial implementation prompts that are initially vague, or explicit multi-component planning requests including planning-only work, root performs only minimal routing discovery, then delegates substantive analysis and design. Discovery may be delegated first. Root integrates the delegated work into an actionable plan proportional to the task and detailed enough that implementation agents can proceed without repeating design work.

- State the intended outcome, scope, assumptions, and relevant paths. Delegate resolution of substantive implementation decisions and interfaces; integrate the resulting evidence.
- Order the steps and dependencies; assign subagent ownership, deliverables, integration points, and acceptance checks. Pass each agent the relevant plan excerpt or revision and applicable assumptions through the [assignment contract](../guides/subagent-coordination.md#assignment-and-result-contracts).
- Prefer available built-in planning/progress APIs when they permit continued execution; otherwise record a concise plan in commentary or an existing task record. Use supported APIs only and do not switch into a mode that requires a separate approval turn merely to record the plan.
- Treat an ordinary plan as ready to execute under the user's existing task authorization, then immediately implement or delegate in the same turn. Do not end with only a plan unless the user requested planning-only work. This default does not represent actual user approval or bypass higher-priority instructions, mandatory host approvals, or unanswered material clarification.
- Infer routine reversible choices. Ask only for genuinely blocking missing scope, information, or authority, and continue independent authorized work. Revise the plan and affected briefs when material evidence changes decisions, dependencies, or acceptance.

## Completion celebration

Only the root celebrates a substantial verified completion, once, when a supported host tool permits it and user preferences allow it. Features, substantial refactors, difficult fixes, and migrations qualify; routine lookups, small edits, and individual subtasks do not. Never celebrate partial or unverified work. In Codex use `mcp__codex_app__fire_confetti`; tool absence/failure does not block reporting, and claim success only when confirmed.

## Root manager timing and token report

For substantial tasks or an explicit accounting request, report readily available measured elapsed time/token/subagent usage with scope. Routine responses need no metrics footer or collection calls. Load [accounting](../guides/usage-accounting.md) when collecting/aggregating metrics or enforcing a numeric budget; mention unavailable metrics only when requested or material to that budget.
