# Agent Instructions: Audio Workflow

## Specialized capability ceiling

Use the [manager ceiling rules](AGENTS.manager.md#capability-ceilings) and [model selection](AGENTS.manager.md#model-and-effort-selection). This section owns audio qualification and the scoped maximum.

| Selected preset | Maximum audio tier |
| --------------- | ------------------ |
| light | Specialist with verified audio capability |
| balanced | Frontier with verified audio capability |
| heavy | Frontier with verified audio capability |

- The scoped ceiling replaces the general ceiling only for assignments consuming actual audio inputs, and remains available through a cheaper general manager. Verify audio capability and recording access (formats, duration, input limits); transcripts, waveforms, or tool summaries alone are not listening evidence.
- Managers, code writers, audio-generation orchestration, and text-only transcript reviewers or summarizers retain the general ceiling. Do not pass this exception to unrelated descendants; split mixed assignments into audio digestion and general execution.
- Each selected audio model needs verified support for the assigned task; speech recognition and acoustic analysis do not imply each other. Select sufficient capability for recording quality, language, overlapping speakers, and ambiguity.

## Audio inputs

For delegated work, use [manager dispatch](manager-delegation.md#dispatch-and-acceptance), the [leaf workflow](AGENTS.leaf.md) for leaf listeners, and [coordination](../guides/subagent-coordination.md) for handoffs/recovery.

- Supply recording paths/references and revisions, requested deliverable, language and known speaker context, acceptance criteria, and specific questions. State whether the task needs a verbatim transcript, content digest, acoustic review, or a combination.
- Inspect the actual recording and preserve the original. When decoding, resampling, channel separation, or segmentation is needed, record transformations and offsets so findings map to the source timeline; do not remove channels or sounds relevant to acceptance.
- Split by recording, time range, or evaluation dimension within input limits. Overlap segment boundaries to preserve words and speaker transitions; retain source timestamps and reconcile duplicated passages.
- Distinguish complete listening from sampling. Track inspected ranges and gaps; do not judge unheard intervals or claim full coverage from sampled excerpts.

## Digestion and repair loop

1. For speech, extract the requested content with source timestamps and consistent speaker labels. Mark unintelligible, uncertain, or overlapping passages instead of inventing words or identities. Verify consequential names, numbers, dates, quotes, decisions, and action owners against the recording.
2. Produce the requested digest (key points, decisions, action items, open questions). Anchor consequential claims to time ranges and distinguish stated content from inference. Do not invent decisions, owners, or deadlines.
3. For acoustic review, inspect relevant intelligibility, clipping, distortion, noise, dropouts, timing, channel balance, and sound events against acceptance criteria. Use measurement tools for numerical claims; neither a transcript nor listening alone proves an exact signal measurement. For interactive playback, also perform functional checks; a recording alone cannot prove application behavior.
4. Return per-recording or per-range pass/fail/unable-to-verify findings with timestamps, severity, observable evidence, correction, artifact revision, listening coverage, and uncertainty. Separate observed sounds and spoken claims from interpretation or preferences.
5. Route repairs through the [manager workflow](manager-delegation.md#recursive-delegation) to the assigned editor, who produces a stable new revision. Recheck changed audio or transcript passages, affected segment boundaries, and dependent digest conclusions under [shared validation rules](../guides/validation.md#shared-validation-rules).
6. Allow at most three repair/recheck retries after the initial failure, subject to tighter user/assignment limits. This replaces the [shared recovery default](../guides/subagent-recovery.md#stalls-and-recovery); other recovery mechanics remain there.

For inaccessible, unsupported, or inadequate inputs, report the exact listening limitation and complete unaffected checks; do not mark audio acceptance passed without usable audio evidence. If only a transcript is accessible, report the result as transcript-based and leave acoustic claims and fidelity to the recording unverified.
