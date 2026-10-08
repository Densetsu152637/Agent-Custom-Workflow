# Subagent result record

This file owns result fields and lifecycle values. Use them under the [result contract](../guides/subagent-coordination.md#assignment-and-result-contracts).

```text
Task ID; objective; role/profile; immediate manager:
Status: in progress | ready for review | accepted | blocked | cancelled
Result revision: commit plus scoped diff/patch, content hash, or artifact version:
Workspace/worktree; branch; base/input revision:
Instruction loading: exact paths read; gaps/newly applicable owners reported:
Deliverable/change/patch paths; interface impacts; integration order:
Acceptance criteria: satisfied, unsatisfied, or unverified, with evidence:
Checks: command/procedure; passed/failed/unrun; exit status if applicable;
  tested revision; evidence/log paths and decisive excerpts:
Assumptions, uncertainty, limitations, and unresolved disagreements:
Blockers; failed approaches; retry count and changed approach:
Pending commands/processes/resources; ownership and whether writes stopped:
Next action; responsible owner; requested integration/manager decision:
Measured elapsed/usage: scope/checkpoint/source, or unavailable with reason:
Reusable failure candidate: applicability/evidence, or none:
Acceptance owner/decision/checkpoint: manager completes after review:
```
