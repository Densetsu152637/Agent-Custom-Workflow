# Usage accounting

Load for requested metrics, aggregation, or numeric budget enforcement under [root reporting](../workflows/AGENTS.root.md#root-timing-and-token-report).

- Use actual exposed telemetry; state scope (prompt, goal, session or leaf), source and checkpoint. Never label goal usage as session usage.
- Include tool/wait time without summing concurrent durations. Aggregate each leaf's record once; do not add cumulative snapshots or recount cached/reasoning tokens.
- Quotas, context capacity, word counts and estimates are not token usage. If telemetry is absent, say so once. Only the root reports overall totals; children give local metrics only when requested.
