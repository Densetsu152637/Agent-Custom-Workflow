# Root implementation planning

Root only: load for substantial vague implementation prompts or explicit multi-component planning, including planning-only work. Workers receive the relevant plan excerpt; they do not load this file.

## Implementation planning

Root performs only minimal routing discovery, then delegates substantive analysis and design (discovery may be delegated first), and integrates the results into an actionable plan proportional to the task, detailed enough that implementation agents need not repeat design work.

- Define the [goals](AGENTS.root.md#goals) first and include them in the plan, with intended outcome, scope, assumptions, and relevant paths. Delegate resolution of substantive implementation decisions and interfaces.
- Order steps and dependencies; assign subagent ownership, deliverables, integration points, and acceptance checks drawn from the goals. Pass each agent the relevant plan excerpt or revision and assumptions through the [assignment contract](../guides/subagent-coordination.md#assignment-and-result-contracts).
- Prefer built-in planning/progress APIs that permit continued execution; otherwise record a concise plan in commentary or an existing task record. Do not enter a mode requiring a separate approval turn merely to record the plan.
- An ordinary plan is ready to execute under the user's existing authorization: implement or delegate in the same turn; end with only a plan for planning-only work. This is not actual user approval and does not bypass higher-priority instructions, mandatory host approvals, or unanswered material clarification.
- Infer routine reversible choices; ask only for blocking missing scope, information, or authority, and continue independent authorized work. Revise the plan, goals (stating the revision), and affected briefs when material evidence changes decisions, dependencies, or acceptance.
