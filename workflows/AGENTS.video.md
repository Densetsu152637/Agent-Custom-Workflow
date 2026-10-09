# Agent Instructions: Video Digestion Workflow

## Scope and modality dispatch

Use this workflow for moving-image content, temporal events, or synchronized visual/audio digestion. It owns temporal coverage and synthesis; [vision](AGENTS.vision.md) owns visual methods and its scoped ceiling, and [audio](AGENTS.audio.md) owns listening methods and its scoped ceiling.

For delegated work, use [manager dispatch](AGENTS.manager.md#dispatch-and-acceptance), the [leaf workflow](AGENTS.leaf.md) for leaf inspectors, and [coordination](../guides/subagent-coordination.md) for handoffs and recovery.

- Dispatch actual frame/sequence inspection under vision eligibility and actual recording inspection under audio eligibility. A combined inspection must verify both capabilities and usable access to both modalities; resolve each applicable cap and obey the stricter cap for the combined assignment, or split it. Explicit video-scoped caps constrain both components under the [manager rules](AGENTS.manager.md#capability-ceilings).
- Media extraction, orchestration, and synthesis from text-only findings retain the general ceiling. Reading transcripts, captions, or frame descriptions does not qualify for a modality exception or establish direct media coverage.

## Inputs and coverage plan

- Supply accessible source paths/references and revisions, requested deliverable, duration, relevant tracks, known synchronization offsets, acceptance criteria, and specific temporal questions. Distinguish content summary, event detection, motion review, and playback verification.
- Verify supported decoding/playback, timestamps, resolution, duration, and input limits. Preserve the source; record extracted frame/clip/audio ranges and transformations with mappings to the original timeline, including variable frame timing where relevant.
- Plan coverage around the required event duration and motion detail. Use broad sampling for orientation, then continuous playback or sufficiently detailed sequences around consequential transitions. Sparse stills cannot establish absence of brief events or continuity of motion.
- Split by time range or evaluation dimension within supported limits. Use overlapping intervals where events or speech span boundaries; retain inspected ranges, gaps, and resolution/time limitations for each modality.

## Inspect and synthesize

1. Inspect visual sequences under the vision workflow and sound under the audio workflow. Preserve modality-specific evidence and uncertainty, including unreadable text, unheard passages, occlusion, and events between samples.
2. Align findings on the source timeline using observed timestamps and known offsets. Verify any consequential claim linking speech, sound, and visible action; temporal proximity alone does not establish causation or speaker identity.
3. Reconcile cross-segment events, speaker context, and duplicated material. Produce the requested digest with timestamped events, key points, and relevant decisions/actions; distinguish observations from inference and preserve conflicting evidence.
4. For video quality or playback acceptance, inspect required motion, transitions, synchronization, seeking, and playback behavior. Use measurements for exact claims about timing/frame rate; extracted frames or an offline recording cannot establish live application behavior. Load [browser verification](AGENTS.browser.md) when an interactive application is involved.

## Findings and recheck

- Return a verdict per source/range/criterion with timestamps, artifact revision, inspected coverage by modality, evidence, and correction. Label sampled coverage explicitly; do not claim full-event coverage from a transcript or a few stills.
- Route repairs through the manager and recheck stable changed clips, affected boundaries/synchronization, and dependent digest conclusions under [shared validation](../guides/validation.md#shared-validation-rules).
- Use vision's repair allowance for visual defects and audio's allowance for audio defects; all other recovery uses [coordination](../guides/subagent-coordination.md#stalls-and-recovery). Count a retry addressing the same audiovisual failure against both applicable allowances; switching modalities does not reset its count.
- Report inaccessible tracks or inadequate temporal coverage precisely and complete unaffected checks. Leave dependent claims unverified when either required modality or time range is missing.
