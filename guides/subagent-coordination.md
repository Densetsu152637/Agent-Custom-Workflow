# Subagent coordination

Root only: owns brief and manifest construction and worker reuse. Leaves do not load this; their loading, checkpoint and return duties live in the [leaf entrance](../workflows/AGENTS.leaf.md). [Root dispatch](../workflows/root-dispatch.md) owns dispatch; load [stalls and recovery](subagent-recovery.md) only for its triggers.

## Assignment and result contracts

- After discovery, supply an explicit [brief](../templates/subagent-brief.md): compact for bounded work with stable inputs, expanded for multiphase work, replacement, cross-stream integration or consequential uncertainty. Include the relevant stage excerpt and path of the [plan document](../workflows/root-planning.md#plan-document), decisions and dependencies; on updates send changes only.
- Every handoff uses the [result schema](../templates/subagent-result.md) under the leaf's [return duties](../workflows/AGENTS.leaf.md#execution-and-return): `ready for review` from the leaf, `accepted` recorded only by root after checking it. Choose compact or expanded per the brief rule above; resume a stopped leaf only by reuse.

## Instruction manifest

- Give exact owner paths relative to an explicit absolute root, with role/domain labels and section names, per the [context handoff](../workflows/root-dispatch.md#context-handoff). Never include [personality](../personalities/README.md) files.
- Hosts load [AGENTS.md](../AGENTS.md), which routes every leaf to the [leaf entrance](../workflows/AGENTS.leaf.md); do not list either. The manifest names only the profile file and the sections the goal triggers from the [leaf index](../workflows/AGENTS.leaf.md#leaf-index) (usually [validation rules](validation.md#shared-validation-rules) plus one domain or Git section). Name sections, not whole files; read-only leaves need no Git mutation rules. Omitting an untriggered owner is the token budget, not a gap.
- Complete unchanged authoritative text in the recipient's context counts as loaded under [shared loading rules](../AGENTS.md#context-and-discovery); paths and the parent's claim do not.

## Context lifecycle

- Reuse a leaf for related follow-ups with compact deltas, so it keeps its loaded owners; use fresh context for unrelated work.
- When context or failed approaches impede work, replace or reset the worker through supported controls, preserving the result and artifacts.
- Before compaction, handoff or a long pause, keep resumable state in the record or a compact checkpoint, separate from [durable lessons](../learning/README.md). Root recovery: [root context recovery](../workflows/root-recovery.md#context-recovery).
- Keep decisive excerpts and artifact paths, not full logs; integrate results by changed decisions, not echoed reports.
