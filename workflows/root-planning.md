# Root implementation planning

Root only: load for substantial initially vague implementation prompts or explicit multi-component planning, including planning-only work. Delegated workers receive the relevant plan excerpt; they do not load root procedures merely to consume it.

## Implementation planning

For substantial implementation prompts that are initially vague, or explicit multi-component planning requests including planning-only work, root performs only minimal routing discovery, then delegates substantive analysis and design. Discovery may be delegated first. Root integrates the delegated work into an actionable plan proportional to the task and detailed enough that implementation agents can proceed without repeating design work.

- State the intended outcome, scope, assumptions, and relevant paths. Delegate resolution of substantive implementation decisions and interfaces; integrate the resulting evidence.
- Order the steps and dependencies; assign subagent ownership, deliverables, integration points, and acceptance checks. Pass each agent the relevant plan excerpt or revision and applicable assumptions through the [assignment contract](../guides/subagent-coordination.md#assignment-and-result-contracts).
- Prefer available built-in planning/progress APIs when they permit continued execution; otherwise record a concise plan in commentary or an existing task record. Use supported APIs only and do not switch into a mode that requires a separate approval turn merely to record the plan.
- Treat an ordinary plan as ready to execute under the user's existing task authorization, then immediately implement or delegate in the same turn. Do not end with only a plan unless the user requested planning-only work. This default does not represent actual user approval or bypass higher-priority instructions, mandatory host approvals, or unanswered material clarification.
- Infer routine reversible choices. Ask only for genuinely blocking missing scope, information, or authority, and continue independent authorized work. Revise the plan and affected briefs when material evidence changes decisions, dependencies, or acceptance.
