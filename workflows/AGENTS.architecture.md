# Agent Instructions: Architecture and Design Review Workflow

## Scope and inputs

Use this workflow for substantial technical design, interface boundaries, migrations, or review of consequential design choices. It owns design reasoning and decision records; [coding standards](../guides/coding-standards.md) own implementation conventions.

For delegated work, use [manager dispatch](AGENTS.manager.md#dispatch-and-acceptance), the [leaf workflow](AGENTS.leaf.md) for leaf designers/reviewers, and [coordination](../guides/subagent-coordination.md) for handoffs and recovery.

- Establish the concrete problem, behavioral requirements, non-goals, compatibility obligations, operational constraints, and measurable acceptance criteria. Identify decisions already accepted and the owner of unresolved product/technical choices.
- Map the relevant current architecture from actual sources: contracts, dependencies, state/data ownership, deployment boundaries, extension points, and known failure modes. Distinguish implemented behavior from aspirational documentation.
- Record uncertainty that could change the design. Load [research](AGENTS.research.md), [data analysis](AGENTS.data-analysis.md), or [security review](AGENTS.security.md) when the decision needs their methods; each scoped exception retains its own eligibility.

## Alternatives and decision

1. Compare a small set of viable alternatives, including retaining or minimally extending the current design when feasible. Evaluate each against the same requirements and relevant complexity, performance, reliability, security, compatibility, and operational costs.
2. Describe contracts, invariants, dependency direction, state/resource ownership, failure handling, and concurrency boundaries. Specify versioning, rollout, migration, and rollback where they affect the design; inspect callers and consumers before changing a shared contract.
3. Resolve consequential uncertainty with the smallest useful prototype, measurement, contract check, or focused critique. Mark projected performance and cost as estimates with assumptions until measured; avoid building multiple full implementations merely to compare ideas.
4. Select the simplest viable design that meets the criteria. Record the reasons, rejected alternatives, tradeoffs, unresolved risks, and conditions that would warrant revisiting the choice. Escalate requirement changes through the manager rather than silently broadening scope.

## Review and handoff

- Apply the [critic profile](../profiles/AGENTS.critic.md) to consequential assumptions, hidden coupling, failure paths, migration feasibility, and operational burden. Resolve material objections with evidence and preserve disagreements that remain unsettled.
- Produce a concise decision record plus affected interfaces, compatibility/migration plan, dependency-ordered implementation slices, ownership, and validation criteria. Use diagrams only when they clarify relationships or behavior.
- Validate design claims and contract/prototype evidence under [shared validation](../guides/validation.md#shared-validation-rules). Acceptance of a design does not establish that its implementation works; hand implementation to the assigned editor and verify the integrated result separately.
- Set a bounded checkpoint under [shared execution defaults](../AGENTS.md#execution-defaults), or [manager scheduling](AGENTS.manager.md#budgets-and-scheduling) for delegated work. Stop when decision-relevant uncertainty is resolved or cannot be reduced within scope; identify the exact remaining decision/input rather than extending design indefinitely.
