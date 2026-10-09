# Usage accounting

Load for requested/substantial-task metrics, aggregation, or numeric budget enforcement under [root reporting](../workflows/AGENTS.root.md#root-manager-timing-and-token-report). This guide owns accounting definitions.

- Use actual exposed telemetry. State scope (prompt, goal, session, or subtree), source, and checkpoint; distinguish final-response tokens not yet counted. Never label goal usage as cumulative session usage.
- Record elapsed start before work when measuring; include tool/wait time through the checkpoint, without summing concurrent durations. Label late-start timing partial.
- Aggregate root/descendant records via immediate managers once each. Do not add cumulative snapshots together or recount cached/reasoning tokens included in totals. Keep incompatible provider definitions separate.
- Quotas, context capacity, file word counts, and estimates are not actual token usage. If requested/budget-critical telemetry is absent, say so briefly; do not generate repeated collection attempts without a new source.
- Overall reporting belongs to the root. Child records include available local metrics only when requested or needed for the allocated budget, with scope/checkpoint or an unavailable reason. Prefer existing telemetry over additional tool calls.
