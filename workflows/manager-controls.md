# Manager process controls

Managers: load before dispatch and when changing limits or handling checkpoints. Mandatory when directing descendants; not for leaves.

## Process and iteration controls

1. Inspect documented host/tool controls before dispatch and configure supported concurrency/depth, turn/tool-call limits, timeouts, and cancellation; do not invent APIs or add a standalone runtime. A polling/wait timeout bounds observation only unless the tool documents that it stops execution.
2. Record enforceable limits, monitored allowances, unavailable controls and cancellation in the dispatch record. Send the child its actionable limits, iteration unit/allowance or milestone, and checkpoint/stop instructions, marking enforced versus monitored; omit unavailable-control lists. Recovery retries follow [stalls and recovery](../guides/subagent-recovery.md#stalls-and-recovery); iteration allowances cannot reset them.
3. If the host lacks a required control, use the immediate manager's active-child count, observed iterations, bounded tool calls, and milestone checkpoints as the fallback. Inspect progress at checkpoints, stop dispatching when an allowance is reached, and stop/cancel or redirect running work through available controls. If cancellation is unavailable, request a stop, report the limitation, and verify write/process cessation before transferring ownership. Prompt instructions are monitored requests, not enforcement.
4. Review the result at the checkpoint. Continue only within remaining scope/allowance, or repair scope and obtain budget authority under [recovery](../guides/subagent-recovery.md#stalls-and-recovery). A stopped process or exhausted allowance is incomplete until acceptance evidence establishes otherwise.
