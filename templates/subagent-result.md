# Subagent result record

Owns result fields and lifecycle values under the [coordination contract](../guides/subagent-coordination.md#assignment-and-result-contracts).

## Lifecycle values

`in progress | ready for review | accepted | blocked | cancelled`

## Compact schema

```text
Task ID; status; result/artifact paths and stable revision:
Acceptance verdicts (each assigned goal/check true or false) with check/procedure, exit status and decisive evidence:
Loading checkpoint reference; subsequent reads/gaps and material limitations:
Required next action/owner; writes stopped, outstanding processes/cleanup, if applicable:
```

Reference unchanged assignment metadata; state changes and the tested revision. Report reached limits/control gaps. For an owned worktree, report the [handoff gate](../guides/git-worktrees.md#handoff-gate-and-recovery) evidence (head SHA, branch, clean status or declared artifacts, stopped processes/services) and, if retained, its path, cleanup owner, reason and cleanup condition. Only the manager records acceptance.

Aim for at most 200 words of handoff metadata, excluding the deliverable; exceed it for necessary findings, evidence, or recovery, never truncating acceptance coverage. Link saved artifacts instead of copying them. Return an inline deliverable once. Send one canonical result through the host's automatic final-result delivery when available; use an explicit message only if needed for delivery or a timely blocker, never duplicating the full result. Progress reports contain material deltas only.

## Expanded schema

For expanded handoffs, also load [additional fields](subagent-result-expanded.md).
