# Agent Instructions: Audio Workflow

## Specialized capability ceiling

Use the [manager ceiling rules](AGENTS.manager.md#capability-ceilings) and [model selection](AGENTS.manager.md#model-and-effort-selection) to dispatch and configure audio assignments. This section owns audio qualification and the scoped maximum:

| Selected preset | Maximum audio tier |
| --------------- | ------------------ |
| light | Specialist with verified audio capability |
| balanced | Frontier with verified audio capability |
| heavy | Frontier with verified audio capability |

- The scoped ceiling replaces the general ceiling only for assignments consuming actual audio inputs. It remains available through a cheaper general manager. Verify both audio capability and recording access, including supported formats, duration, and input limits; transcripts, waveforms, or tool summaries alone do not constitute listening evidence.
- Managers, code writers, audio-generation orchestration, and text-only transcript reviewers or summarizers retain the general ceiling. Do not pass this exception to unrelated descendants; split mixed assignments into audio digestion and general execution.
- Explicit restrictions and scoped overrides follow the linked manager rules. Every selected audio model must have verified support for the assigned task, such as speech recognition or acoustic analysis; one does not establish the other. Select sufficient capability for recording quality, language, overlapping speakers, and ambiguity.

## Audio inputs

Use [manager dispatch](AGENTS.manager.md#dispatch-and-acceptance), the [leaf workflow](AGENTS.leaf.md) for leaf listeners, and [coordination](../guides/subagent-coordination.md) for handoffs/recovery.

- Supply accessible recording paths/references and source revisions, requested deliverable, language and known speaker context when available, acceptance criteria, and specific questions in the assignment brief. State whether the task needs a verbatim transcript, content digest, acoustic review, or a combination.
- Inspect the actual recording. Preserve the original; when decoding, resampling, channel separation, or segmentation is needed, use supported tools and record transformations and offsets so findings map back to the source timeline. Avoid removing channels or sounds relevant to acceptance.
- Split by recording, time range, or evaluation dimension within supported input limits. Use overlap at segment boundaries when needed to preserve words and speaker transitions; retain source timestamps and reconcile duplicated passages and cross-segment context.
- Distinguish complete listening from sampling. Track inspected ranges and gaps; do not judge unheard intervals or claim complete coverage from sampled excerpts.

## Digestion and repair loop

1. For speech, extract the requested content with source timestamps and consistent speaker labels. Mark unintelligible, uncertain, or overlapping passages instead of inventing words or identities. Verify consequential names, numbers, dates, quotes, decisions, and action owners against the recording; retain unresolved uncertainty.
2. Produce the requested digest, grouping key points, decisions, action items, and open questions where relevant. Anchor consequential claims to recording time ranges, distinguish stated content from inference, and reconcile segment results without duplicate content or lost qualifications. Do not invent decisions, owners, or deadlines.
3. For acoustic review, inspect relevant intelligibility, clipping, distortion, noise, dropouts, timing, channel balance, music, or other sound events against acceptance criteria. Use measurement tools when a numerical claim requires them; neither a transcript nor listening alone proves an exact signal measurement. For interactive playback, also perform functional checks; a recording alone cannot prove application behavior.
4. Return per-recording or per-range pass/fail/unable-to-verify findings with timestamps, severity where applicable, observable evidence, and correction. Include the artifact revision, listening coverage, and meaningful uncertainty; separate observed sounds and spoken claims from interpretation or preferences.
5. Route repairs through the [manager workflow](AGENTS.manager.md#recursive-delegation) to the assigned editor. The editor produces a stable new revision. Apply [shared validation rules](../guides/validation.md#shared-validation-rules) to reinspection; recheck changed audio or transcript passages and dependent digest conclusions, including affected segment boundaries.
6. Allow at most three repair/recheck retries after the initial failure, subject to tighter user/assignment limits. This audio-repair allowance replaces the [shared recovery default](../guides/subagent-coordination.md#stalls-and-recovery); other recovery mechanics remain there.

Report the exact listening limitation for inaccessible, unsupported, or inadequate inputs and complete unaffected checks; do not mark audio acceptance passed without usable audio evidence. If only a transcript is accessible, report the result as transcript-based and leave acoustic claims and fidelity to the recording unverified.
