# Agent Instructions: Debugging and Incident Investigation Workflow

## Scope and inputs

Use this workflow for incorrect behavior, regressions, exceptions, intermittent failures, or incidents. It owns causal investigation; [coding standards](../guides/coding-standards.md) own implementation and the [validation guide](../guides/validation.md) owns shared evidence requirements.

For delegated work, use [manager dispatch](AGENTS.manager.md#dispatch-and-acceptance), the [leaf workflow](AGENTS.leaf.md) for leaf investigators, and [coordination](../guides/subagent-coordination.md) for handoffs and recovery.

- Establish expected and observed behavior, impact, affected versions/environments, reproduction inputs, and the first known failing and last known working states. Separate supplied reports from reproduced observations.
- Read relevant entry points, contracts, recent changes, tests, and logs. Record the runtime/configuration and source revision; handle sensitive evidence under [environment configuration](../guides/environment-configuration.md#configuration-output).
- For an active incident, distinguish immediate containment from root-cause repair. Record temporary mitigation, its limits, and the responsible follow-up owner. Scope live-system actions through the manager; investigation does not grant production mutation authority.

## Investigation

1. Reproduce with the smallest representative case. Record steps, expected/actual results, frequency, and relevant state. If reproduction is unavailable, preserve evidence and label conclusions provisional.
2. Maintain a compact hypothesis ledger: candidate cause, supporting/contradicting evidence, discriminating check, and result. Follow the causal path from inputs through state changes to the failure; do not infer causation from the newest change or a suspicious log alone.
3. Prioritize experiments that distinguish competing explanations. Change one relevant factor at a time where practical; use controlled comparisons, targeted instrumentation, or revision bisection when suitable. Preserve the failing evidence before changes and isolate mutable test resources under [Git usage](../guides/git-usage.md#parallel-work-and-worktrees).
4. For timing or concurrency failures, examine ordering, cancellation, resource ownership, and external dependencies. Measure frequencies and timing when those support a claim; a single successful rerun does not establish an intermittent fix.
5. Use a bounded checkpoint under [shared execution defaults](../AGENTS.md#execution-defaults), or [manager scheduling](AGENTS.manager.md#budgets-and-scheduling) when directing descendants. Stop when the causal chain is supported, remaining hypotheses cannot change the repair, or access/budget prevents further discrimination. Use [recovery](../guides/subagent-coordination.md#stalls-and-recovery) for failed milestones; ordinary hypothesis experiments are not recovery retries.

## Repair and validation

- Return the causal explanation, precise evidence locators, rejected alternatives, and the smallest repair to the assigned implementer through the manager. Distinguish a workaround from a root-cause fix and retain unresolved contributors.
- Where feasible, demonstrate the relevant failure on the old revision and success on the repaired revision with the same regression check. Validate affected behavior and meaningful adjacent failure paths under [shared validation](../guides/validation.md#shared-validation-rules).
- For incidents, verify recovery against the affected service behavior and relevant observation window, including any residual temporary mitigation. Report symptom resolution separately from certainty about the cause.
- Deliver reproduction steps, tested revisions/environment, experiment outcomes, root-cause confidence, repair/mitigation, and remaining uncertainty. Submit genuinely reusable lessons through [catalog maintenance](../learning/README.md#maintaining-lessons).
