# Agent Instructions: Security Review Workflow

## Specialized capability ceiling

Use the [manager ceiling rules](AGENTS.manager.md#capability-ceilings) and [model selection](AGENTS.manager.md#model-and-effort-selection). This section owns security qualification and the scoped maximum.

| Selected preset | Maximum security tier |
| --------------- | --------------------- |
| light | Specialist |
| balanced | Frontier |
| heavy | Frontier |

- The scoped ceiling replaces the general ceiling only for bounded difficult threat modeling or adversarial analysis of consequential vulnerabilities, such as authorization bypass, privilege escalation, or interacting trust-boundary failures. It remains available through a cheaper general manager.
- Routine checklist review, scanner execution/triage, dependency inventory, managers, code repair, and unrelated reviews retain the general ceiling. Source/behavior verification within a qualifying analysis stays in scope. Split mixed assignments; do not pass the exception to unrelated descendants.
- Verify access to relevant code/configuration and suitable security reasoning capability; the exception cannot compensate for inaccessible evidence.

## Scope and threat model

For delegated work, use [manager dispatch](manager-delegation.md#dispatch-and-acceptance), the [leaf workflow](AGENTS.leaf.md) for leaf reviewers, and [coordination](../guides/subagent-coordination.md) for handoffs and recovery.

- Establish the review objective, authorized targets/environment, revision, and expected controls. A focused review is not a whole-system assurance claim.
- Identify assets, attacker capabilities, entry points, trust boundaries, and sensitive data flows from actual sources. Load [architecture](AGENTS.architecture.md) when design reasoning is also needed and [research](AGENTS.research.md) for external advisory/source verification.
- Prefer source review and controlled local tests with synthetic data. Active probing must stay within authorized targets, methods, and resources; a security assignment does not grant access or mutation permissions. Handle credentials and sensitive output under [environment configuration](../guides/environment-configuration.md#secret-handling).

## Review and substantiation

1. Trace untrusted inputs and authority decisions through the system: authentication, server-side authorization, tenant/object boundaries, validation/encoding, secret exposure, and resource limits as applicable.
2. Examine bypass and failure paths (alternate endpoints, state transitions, replay/races, default/error behavior). Distinguish an absent visible control from a verified exploitable path.
3. Treat scanner findings as leads: verify affected versions, configuration, reachability, prerequisites, and mitigations; record false positives. Do not claim exploitability from a package name or severity label alone.
4. Substantiate each finding with source/behavior locators, attacker prerequisites, attack path, impact, severity rationale, confidence, and the smallest repair and verification. Label unconfirmed candidates; avoid reproducing secrets or unnecessary exploit data.

## Repair and acceptance

- Route remediation through the manager to the assigned implementer; keep review separate from implementation ownership. Prefer fixes at the trust boundary and inspect dependent paths that could retain the bypass.
- Verify, under [shared validation](../guides/validation.md#shared-validation-rules), the failure on the vulnerable revision where feasible, rejection on the repaired revision, and continued success for legitimate authorized behavior.
- Deliver the threat model, tested revision/surfaces, findings, coverage, residual risk, and checks left unrun. A no-findings verdict applies only to the inspected scope; it does not establish the system is secure.
