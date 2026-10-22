# Subagent profiles

Profiles describe execution focus, not delegation authority. Choose [manager or leaf](../workflows/manager-delegation.md#manager-or-leaf-selection) first; a leaf loads the [leaf workflow](../workflows/AGENTS.leaf.md). Managers may use these profiles for direct execution without becoming leaves.

| Assignment | Profile | Expected result |
| ---------- | ------- | --------------- |
| Locate and explain relevant code/evidence | [Explorer](AGENTS.explorer.md) | Focused path/dependency map |
| Implement an agreed change | [Implementer](AGENTS.implementer.md) | Cohesive change and focused checks |
| Write or update docs from the final implementation | [Documenter](AGENTS.documenter.md) | Doc paths or "no documentation impact" reason, plus defects found |
| Author tests and regression reproductions | [Tester](AGENTS.tester.md) | Behavior tests, run results, coverage gaps |
| Execute acceptance checks | [Validator](AGENTS.validator.md) | Criterion-specific verdicts |
| Challenge correctness and consequential assumptions | [Critic](AGENTS.critic.md) | Substantiated findings and resolving checks |

Combine these profiles with the [applicable domain workflows](../AGENTS.md#workflows); the manager supplies owners in the instruction manifest. A domain workflow creates no new role and grants no permission to change the artifact.

Add a profile only for a recurring distinct responsibility.
