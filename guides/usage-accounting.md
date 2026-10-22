# Usage accounting

Load for requested metrics, aggregation, or numeric budget enforcement under [root reporting](../workflows/AGENTS.root.md#root-manager-timing-and-token-report). This guide owns accounting definitions.

- Use actual exposed telemetry. State scope (prompt, goal, session, or subtree), source, and checkpoint; note final-response tokens not yet counted. Never label goal usage as session usage.
- Record elapsed start before work; include tool/wait time through the checkpoint without summing concurrent durations. Label late-start timing partial.
- Aggregate root/descendant records via immediate managers once each. Do not add cumulative snapshots together or recount cached/reasoning tokens included in totals. Keep incompatible provider definitions separate.
- Quotas, context capacity, word counts, and estimates are not token usage. If needed telemetry is absent, say so briefly; no repeated collection attempts without a new source.
- Overall reporting belongs to the root. Child records include local metrics only when requested or needed for the allocated budget, with scope/checkpoint or an unavailable reason.
