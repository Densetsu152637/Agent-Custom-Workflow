# Agent instructions: vision workflow

## Specialized capability ceiling

Read [AGENTS.md](AGENTS.md) first and inherit its shared policy in full. This file contains only vision-specific additions and the scoped capability exception below.

Only assignments that inspect actual visual inputs receive this enhanced ceiling, using the base policy's tier definitions:

| Selected preset | Maximum vision tier                        |
| --------------- | ------------------------------------------ |
| light           | Specialist with verified vision capability |
| balanced        | Frontier with verified vision capability   |
| heavy           | Frontier with verified vision capability   |

- Verify both visual capability and access to the image inputs; a text-only summary does not constitute image QA.
- The user can override the visual cap separately: `use light preset with vision ceiling heavy` permits frontier vision workers alongside economy general workers. `vision ceiling light`, `balanced`, and `heavy` use the base policy's economy, specialist, and frontier ceilings respectively, each requiring verified vision support. The explicit visual cap replaces the table's visual default and persists for the task until changed.
- A user-wide cap such as `all agents at most economy tier` also constrains vision workers unless the user explicitly exempts them.
- Only the visual assignment gets the enhanced ceiling. Managers, code writers, image-generation orchestration, and text-only reviewers retain the general ceiling. An enhanced vision worker must not pass its exception to unrelated descendants. A mixed assignment should be split into visual inspection and general execution.

## Inputs and delegation

- Give each vision worker exact paths or accessible image references for the current outputs and necessary comparisons, plus intended style, acceptance criteria, viewing scale, and specific questions. Identify version/commit or another stable artifact identifier.
- Provide actual image inputs through supported tools. For PDFs, slides, or UI work, supply the relevant rendered pages/screens and source paths. For layout-sensitive work, include a full view plus detail crops where useful; do not judge unseen regions.
- Split visual inspection by image batches, pages, screens, or evaluation dimensions. Keep batches small enough to detect the required detail at the supported resolution; do not duplicate review of unchanged passing assets without a relevant reason.

## Inspection and repair loop

1. Inspect the actual pixels against the brief. Check relevant anatomy/geometry, text accuracy, clipping, blur, lighting, style consistency, layout, contrast, alignment, and rendering defects. For interactive UI, combine visual inspection with functional checks; screenshots alone cannot prove behavior.
2. Return a per-artifact verdict: pass, fail, or unable to verify. For defects, include location, severity, observable evidence, and a specific correction. Separate measured findings from subjective preferences and uncertain interpretations.
3. The immediate manager sends defects and exact affected paths to the assigned editing worker. That worker adjusts source, prompt, assets, or supported rendering/generation settings and produces a new stable revision.
4. Reinspect changed assets and dependent areas. Record which revision passed; approval of an earlier render does not approve later edits.
5. Allow at most three repair/recheck retries after the initial failure. Stop earlier when blocked or the same defect repeats without progress. Preserve the best output and report remaining defects and the next useful decision through the immediate manager. This repair limit is unrelated to delegation depth.

Do not mark visual work complete when inputs were inaccessible or too low-resolution to evaluate. Report the exact inspection limitation and complete unaffected checks.
