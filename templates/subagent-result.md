# Subagent result record

This file owns result fields and lifecycle values under the [coordination contract](../guides/subagent-coordination.md#assignment-and-result-contracts).

## Lifecycle values

`in progress | ready for review | accepted | blocked | cancelled`

## Compact schema

```text
Task ID; role; immediate manager; status:
Stable result revision; workspace/worktree and branch; changed/deliverable paths:
Applicable owner paths verified; loading gaps or newly applicable owners:
Acceptance verdicts; check/procedure, exit status, revision and decisive evidence:
Material uncertainty/blockers; pending processes/resources and write cessation:
Worktree retirement/retention; path, branch, cleanup owner, reason/condition:
Next action/owner; manager acceptance decision/checkpoint:
```

Omit inapplicable optional fields and duplicate summaries. When no worktree is owned, its cleanup field may be omitted; retained owned worktrees require the complete retention record.

## Expanded schema

For expanded handoffs, also load [additional fields](subagent-result-expanded.md). Metrics are conditional under the coordination contract.
