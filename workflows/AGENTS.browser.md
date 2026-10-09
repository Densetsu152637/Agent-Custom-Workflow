# Agent Instructions: Browser and Interactive Verification Workflow

## Scope and inputs

Use this workflow to verify websites or interactive applications through actual user journeys. It owns behavioral inspection; [vision](AGENTS.vision.md) owns visual inspection and [audio](AGENTS.audio.md) owns listening checks. Load relevant browser/computer-use skills and use supported host controls.

For delegated work, use [manager dispatch](AGENTS.manager.md#dispatch-and-acceptance), the [leaf workflow](AGENTS.leaf.md) for leaf testers, and [coordination](../guides/subagent-coordination.md) for handoffs and recovery.

- Identify the target URL/application, build/revision, environment, user role, starting state, relevant device/viewport, required journeys, and expected outcomes. Match coverage to the changed behavior and supported platforms.
- Establish service readiness under [validation](../guides/validation.md#readiness). Use assigned accounts, fixtures, and isolated sessions/resources where available; define ownership and cleanup for state created by checks under [Git resource isolation](../guides/git-usage.md#parallel-work-and-worktrees).
- Identify steps with external effects, such as sending, purchasing, publishing, or changing shared records. Execute them only within existing authorization and assigned resources; use an available sandbox for verification and report any untested live behavior.

## Journey verification

1. Start from a known state and follow the supported user interaction path. Observe the interface before choosing controls; record actions and decisive state transitions so the journey can be reproduced.
2. Check the result at the level required by the criterion: rendered state, navigation, stored state after reload/reopening, and server/API effects when relevant and accessible. A click, successful request, or screenshot alone does not establish the entire outcome.
3. Cover relevant empty, loading, error, retry, cancellation, invalid-input, and permission states. For asynchronous behavior, check stale responses and repeated actions when they could affect correctness.
4. Exercise keyboard operation, focus movement, labels, and relevant assistive semantics when accessibility is in scope. Inspect responsive behavior at the required sizes; report the actual device/browser coverage rather than generalizing from one viewport.
5. Use network, console, accessibility-tree, and application evidence to resolve ambiguous behavior when supported. Redact sensitive data under [environment configuration](../guides/environment-configuration.md#configuration-output); inaccessible internals remain unverified.

## Findings and recheck

- Return a verdict per journey/criterion with target revision, starting state, steps, expected/actual outcome, evidence locators, and relevant browser/device details. Separate functional defects from visual findings and environment/tool failures.
- Route repairs through the manager to the assigned editor. Recheck the stable repaired revision and affected dependent journeys under [shared validation](../guides/validation.md#shared-validation-rules); use [coordination recovery](../guides/subagent-coordination.md#stalls-and-recovery) for retries.
- If only static output or screenshots are accessible, complete those checks with the appropriate domain workflow and leave interactive behavior unverified. Preserve required evidence and clean up authorized task-created state using the applicable resource owner.
