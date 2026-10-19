# Subagent result record

This file owns result fields and lifecycle values under the [coordination contract](../guides/subagent-coordination.md#assignment-and-result-contracts).

## Lifecycle values

`in progress | ready for review | accepted | blocked | cancelled`

## Compact schema

```text
Task ID; status; result/artifact paths and stable revision:
Acceptance verdicts with check/procedure, exit status and decisive evidence:
Loading checkpoint reference; subsequent reads/gaps and material limitations:
Required next action/owner; writes stopped, outstanding processes/cleanup, if applicable:
```

Reference unchanged assignment metadata rather than repeating role, manager, workspace, branch, or input revision; state changes and the tested revision explicitly. Report reached limits/control gaps. Retained owned worktrees require path, branch, cleanup owner, reason and cleanup condition. Only the manager records acceptance.

Aim for at most 200 words of handoff metadata, excluding the requested deliverable. Use more for necessary findings, evidence, or recovery; never truncate acceptance coverage to meet a word target. Link saved artifacts instead of copying their contents. For an inline deliverable, return it once with minimal metadata. Send one canonical result through the host's automatic final-result delivery when available; use an explicit message only if needed for delivery or a timely blocker, without repeating the full result in both channels. Progress reports contain material deltas, not repeated inventories or recaps.

## Expanded schema

For expanded handoffs, also load [additional fields](subagent-result-expanded.md). Metrics are conditional under the coordination contract.
