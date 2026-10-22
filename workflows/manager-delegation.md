# Manager delegation

Managers: load at assignment intake and before dispatch, redirection or acceptance. Ceilings and model/effort selection are in [manager policy](AGENTS.manager.md). Leaves do not load this.

## Recursive delegation

- Managers own their bounded workstreams, child assignments, dependencies, and integration decisions. Root-specific duties live in [AGENTS.root.md](AGENTS.root.md#root-responsibilities).
- At intake, every manager identifies independently ownable deliverables before choosing worker count, and assigns multiple ones separately without a reminder. This includes planning and documentation; a critic complements execution assignments. Give a concise routing checkpoint naming the assignments or a concrete constraint, then start ready children within the [shared concurrency allowance](#budgets-and-scheduling) before waiting; queue excess work. No-subagent instructions and host/task restrictions take precedence; disclose affected work.
- When no useful independent split exists, a non-root manager may execute cohesive work directly, or delegate for specialist execution or meaningful review. Reuse a worker for follow-ups under [context lifecycle](../guides/subagent-coordination.md#context-lifecycle). Dispatch cost alone does not justify combining independent deliverables or serializing ready work.
- Root's stricter [delegation default](root-delegation.md#delegation-default) applies to root-owned execution; do not insert a manager merely to bypass it. If delegation is unavailable, execute only within task authority or the root exception, and disclose the limitation.
- Choose each child's role under [manager or leaf selection](#manager-or-leaf-selection). Keep the hierarchy shallow: respect depth/host limits, require smaller deliverables at each layer; no cycles, unchanged-objective delegation, or managers for trivial work.
- Each agent has one immediate manager; only that manager assigns or redirects it. Route cross-workstream requests through managers. A leaf that finds a useful split reports it; its manager splits/reassigns or promotes it with an updated brief and manifest before it delegates (apply [handoff](../guides/subagent-recovery.md#stalls-and-recovery) to conflicting execution). Promotion replaces only the leaf role restriction, not inherited scope, caps, or user restrictions.
- Establish acceptance criteria, dependencies, shared contracts, and integration points before splitting large tasks. For planning or documentation, bound common assumptions/contracts first, then dispatch independently draftable deliverables in parallel; shared context or a single integration writer does not require one omnibus author. Stop splitting at cohesive, testable assignments. Duplicate work only for a deliberate comparison with a stated question.

## Manager or leaf selection

Root and every subagent manager apply this choice before dispatch; neither a profile name nor task difficulty alone selects the role:

| Work assigned to the child | Role and ownership |
| -------------------------- | ------------------ |
| One cohesive deliverable with bounded acceptance | Leaf with the applicable execution profile. |
| Independent deliverables whose coordination can remain with the current manager | Separate leaves, started in parallel when ready. |
| A bounded workstream with useful child deliverables and recurring dependency decisions, interface coordination, or integration/acceptance across them | Manager owning that workstream and its integrated result. |

- Assign the manager role automatically when the third case applies, including beneath another manager. Name its likely child deliverables and the coordination it removes from its parent. It applies this rule to descendants and retains integration/acceptance rather than forwarding reports.
- Its brief grants delegation within the workstream and inherited restrictions and provides the manager manifest, concurrency allocation/depth limits, interfaces, acceptance criteria and integration/cleanup ownership. Verify the host role exposes delegation tools; a Markdown label cannot grant them. If unavailable, keep coordination with the parent and flatten or queue; disclose the limitation.
- Reserve capacity for execution beneath a manager, counting managers where the host limit does. Do not fill the allowance with managers waiting on descendants; coordinate slots through the root, or flatten/queue.

## Budgets and scheduling

- Before dispatch, establish a concurrency limit, time/effort allowance, investigation stop condition, iteration/retry allowance, and checkpoint, bound to [process and iteration controls](manager-controls.md#process-and-iteration-controls). Honor user and host limits; a preset creates no token/cost caps.
- Without a user concurrency preference, start with at most three active children across the root task tree, or the smaller host limit; increase only when independent work, resources, and budget justify it. Coordinate through the root rather than three slots per subtree.
- Use a named milestone when a numeric allowance cannot be justified. Without enforcement controls, allowances are monitored checkpoints.
- Allocate child allowances from the parent's remaining budget, reserving integration/review time. Load [accounting](../guides/usage-accounting.md) only for numeric budget enforcement or required metrics.
- Run unblocking work first. Start ready independent assignments within the allowance before waiting; do not dispatch and wait one at a time. Serialize real dependencies, shared-resource conflicts, or host limits; apply [Git resource isolation](../guides/git-worktrees.md#parallel-work-and-worktrees) to concurrent writes/checks. Do not split cohesive work or create agents merely because slots are free.
- Checkpoint at the agreed milestone/allowance or on material change; narrow, queue, redirect, or escalate when acceptance is unreachable within scope. Budget exhaustion is not completion; explicit user budgets cannot be expanded without authorization.

## Documentation alignment

Apply [documentation alignment](../guides/coding-standards.md#documentation-alignment) during scoping, assignment, and acceptance.

## Dispatch and acceptance

- For a new worker, prefer fresh context plus its brief, including for siblings. Select the host's fresh-context option explicitly; a brief alone does not disable default history inheritance. Inherit history only when essential context cannot be captured otherwise; explain why. Apply [model selection](AGENTS.manager.md#model-and-effort-selection) before choosing a context path; reuse/inheritance must preserve the selected configuration. Pass only relevant decisions, interfaces, evidence and the paths required by [context handoff](AGENTS.manager.md#context-handoff), not the parent's transcript or other workers' full reports.

1. Read relevant context under [shared discovery](../AGENTS.md#context-and-discovery), then use the [assignment contract](../guides/subagent-coordination.md#assignment-and-result-contracts) and [context handoff](AGENTS.manager.md#context-handoff). Unknown paths require bounded discovery before implementation. For substantial initially vague implementation work, apply the [root implementation plan](root-planning.md#implementation-planning) before dispatching, and carry its decisions and dependencies into child assignments.
2. Select [manager or leaf](#manager-or-leaf-selection) first, then any applicable [execution profile](../profiles/README.md), contract, and [instruction manifest](../guides/subagent-coordination.md#instruction-manifest). State the role explicitly.
3. Apply [failure lesson selection](../learning/README.md#using-lessons) and the [model selection](AGENTS.manager.md#model-and-effort-selection), scheduling and mandatory [process controls](manager-controls.md) before dispatch.
4. Spot-check consequential assignments' [loading checkpoints](../guides/subagent-coordination.md#instruction-manifest) against read traces or complete authoritative context and one or two task-critical rules; record inaccessible traces as a verification limit. Check the work against the rules at acceptance; a read alone does not prove compliance. No separate audit agent or acknowledgement gate.
5. Use [coordination](../guides/subagent-coordination.md) for checkpoints and handoffs, [Git integration](../guides/git-worktrees.md#integration) for code changes, [documentation alignment](#documentation-alignment), and [validation](../guides/validation.md#shared-validation-rules) for acceptance evidence. Coordinate path ownership before direct edits to active child work.
6. Apply [commit before ending work](../guides/git-usage.md#commit-before-ending-work) to manager-owned changes and verify child commit evidence before acceptance or transfer. Add independent critique for material risk against a focused question. Record acceptance through the [result contract](../guides/subagent-coordination.md#assignment-and-result-contracts). Required external repository approvals remain governed by the [Git guide](../guides/git-publication.md#pull-requests-and-merge-rules).
7. Route reusable failure candidates through [catalog maintenance](../learning/README.md#maintaining-lessons) and perform any authorized cleanup under [Git cleanup](../guides/git-worktrees.md#safe-cleanup).
