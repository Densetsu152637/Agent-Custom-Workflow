# Agent Instructions: Vision Workflow

## Specialized capability ceiling

Use the [manager ceiling rules](AGENTS.manager.md#capability-ceilings) and [model selection](AGENTS.manager.md#model-and-effort-selection). This section owns vision qualification and the scoped maximum.

| Selected preset | Maximum vision tier |
| --------------- | ------------------- |
| light | Specialist with verified vision capability |
| balanced | Frontier with verified vision capability |
| heavy | Frontier with verified vision capability |

- The scoped ceiling replaces the general ceiling only for assignments inspecting actual visual inputs, and remains available through a cheaper general manager. Verify visual capability and image access; text-only summaries do not constitute image QA. Select sufficient capability for input detail and ambiguity.
- Managers, code writers, image-generation orchestration, and text-only reviewers retain the general ceiling. Do not pass this exception to unrelated descendants; split mixed assignments into visual inspection and general execution.

## Visual inputs

For delegated work, use [manager dispatch](manager-delegation.md#dispatch-and-acceptance), the [leaf workflow](AGENTS.leaf.md) for leaf inspectors, and [coordination](../guides/subagent-coordination.md) for handoffs/recovery.

- Supply current outputs and comparisons as accessible image paths/references, plus intended style, viewing scale, acceptance criteria, and specific questions.
- For PDFs, slides, or UI, inspect actual rendered pages/screens. Do not judge unseen regions or inaccessible/insufficient-resolution inputs.
- Split by image batch, page, screen, or evaluation dimension, in batches small enough to detect required detail.

## Inspection and repair loop

1. Inspect pixels for the relevant defects. For interactive UI, also perform functional checks; screenshots alone cannot prove behavior.
2. Return per-artifact pass/fail/unable-to-verify findings with location, severity, observable evidence, and correction. Separate measured defects from preferences.
3. Route repairs through the [manager workflow](manager-delegation.md#recursive-delegation) to the assigned editor, who produces a stable new revision. Reinspect changed assets and dependent visual regions under [shared validation rules](../guides/validation.md#shared-validation-rules).
4. Allow at most three repair/recheck retries after the initial failure, subject to tighter user/assignment limits. This replaces the [shared recovery default](../guides/subagent-recovery.md#stalls-and-recovery); other recovery mechanics remain there.

For inaccessible or inadequate inputs, report the exact limitation and complete unaffected checks; do not mark visual acceptance passed without usable visual evidence.
