# Subagent stalls and recovery

Load when inputs, authority or progress are insufficient, at failed milestones or iteration/process limits, and before replacement, reassignment or ownership transfer. Ordinary successful execution needs only the coordination core.

## Stalls and recovery

- Report missing inputs, authority/ownership conflicts, inaccessible tools, or repeated failures without new evidence. Check exposed progress or a bounded checkpoint; silence alone is not a stall.
- At iteration/process limits, stop at the assigned checkpoint and report limits/control gaps. Only the immediate manager redirects or authorizes continuation under its [host-control and fallback procedure](../workflows/manager-controls.md#process-and-iteration-controls).
- Preserve cause, decisive evidence, attempted hypotheses and smallest next action. Retry transient failures with a reason; change approach for deterministic failures.
- Use the brief's retry allowance, otherwise an applicable specialist allowance or at most two recovery retries after the failed milestone. Ordinary hypothesis experiments are not retries; rescoping cannot cosmetically reset counts.
- At the limit or on missing authority, the manager repairs scope/context/tools before [capability escalation](../workflows/AGENTS.manager.md#model-and-effort-selection). Ask the user only for information, authority or budget the manager cannot supply.
- Before replacement/reassignment, preserve results/artifacts, stop conflicting writes/processes and verify cessation before transfer. Prevent late overwrites of accepted revisions. Block only affected dependencies; preserve limitations and route [reusable lessons](../learning/README.md#maintaining-lessons).
