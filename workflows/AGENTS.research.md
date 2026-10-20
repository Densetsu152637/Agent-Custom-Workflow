# Agent Instructions: Research Workflow

## Scope and documentation

Source verification, comparison, and synthesis rules apply to ordinary lookups and research. Mandatory persistent question maps, evidence ledgers, exact prompt/result records, discoverable indexes, and BibTeX entries apply only to paper-related research undertaken to write or maintain a research paper/manuscript. A task being called research, using papers as sources, or comparing software does not alone trigger those artifacts. For ordinary lookups/comparisons, cite verified sources in the response and retain only task-required evidence; create repository research documents only when requested or required by an applicable project owner.

## Specialized capability ceiling

Use the [manager ceiling rules](AGENTS.manager.md#capability-ceilings) and [model and effort selection](AGENTS.manager.md#model-and-effort-selection) to resolve research assignments. This section owns research qualification, the scoped maximum, and research-specific model and effort selection:

| Selected preset | Maximum research tier |
| --------------- | --------------------- |
| light | Specialist |
| balanced | Frontier |
| heavy | Frontier |

- The scoped ceiling applies to substantive research assignments at any difficulty, including factual lookup, source verification and gathering, extraction, comparisons, analysis, synthesis, and research plans. Eligibility follows the assigned research deliverable, not a task label or difficulty.
- Pure research coordination, implementation, and unrelated architecture or code review retain the general ceiling. A manager performing substantive research qualifies for the research ceiling; coordination alone does not. Each descendant qualifies based on its own assignment, so do not pass the research ceiling to unrelated work.
- Verify source access and relevant analytical capability. A stronger model cannot compensate for inaccessible evidence. Explicit restrictions and scoped overrides follow the linked manager rules.

## Research model and effort selection

- For each substantive research assignment covered above, select the strongest verified suitable available model within its effective ceiling; do not choose a cheaper model solely because the work is routine. Verify that the model can access the required evidence and perform the assigned method. If suitability or capability cannot be verified, use an established capable role and disclose the limitation; do not infer model capability from its name.
- Use medium effort for ordinary research when the control is available. Use high effort for difficult, conflicting, uncertain, or consequential analysis when supported. Do not automatically select the maximum effort; honor explicit user restrictions, host controls, and the manager's budget and process limits.

## Research methods

Use [manager dispatch](AGENTS.manager.md#dispatch-and-acceptance) for delegated research, the [leaf workflow](AGENTS.leaf.md) for leaf execution, and [coordination](../guides/subagent-coordination.md) for handoffs/recovery.

1. Frame the question, audience, deliverable, scope, dates/geography, and useful-answer criteria. State reasonable assumptions without unnecessary interruption. Distinguish lookup, comparison, causal inference, forecasting, and recommendation; establish criteria before ranking alternatives.
2. Identify key uncertainties and competing explanations. Prioritize investigation by its potential to change the conclusion. Set a bounded investigation milestone under [shared execution defaults](../AGENTS.md#execution-defaults); use the [manager's budget procedure](AGENTS.manager.md#budgets-and-scheduling) when directing descendants. Stop when decision-relevant claims have adequate support and material objections are resolved, or further uncertainty cannot be reduced within access/budget.
3. Split substantial research by answerable subquestions/evidence types; separate gathering, analysis, synthesis, and critique when it improves coverage or reduces bias. Maintain a compact question map and evidence ledger in assigned paths only under the [paper documentation scope](#scope-and-documentation).

## Retain and reuse research results

Apply the persistent-record requirements in this section only under the [paper documentation scope](#scope-and-documentation).

- Whenever a paper-related research goal or prompt produces results, record them for future agents, including inconclusive or negative outcomes. Use the assigned project's existing research documents or evidence ledger; give each record a stable ID and link it from a discoverable index at a persistent path. Preserve the goal and exact prompt (redacting secrets), scope and assumptions, methods/settings, relevant dates and source or implementation revisions, results, supporting evidence, and limitations.
- Before new research, consult relevant prior records and compare findings using compatible criteria. Record changed scope, methods, or context and explain conflicting findings in a new entry; preserve prior records rather than overwriting their history.
- Add every source used in paper-related research to the repository's existing BibTeX bibliography. If none exists, create `paper/references.bibtex` under the repository root, creating `paper/` as needed. Reuse existing entries and stable citation keys; verify metadata against the source itself and leave unavailable fields out rather than inventing them. Reference citation keys in retained research records where appropriate.

## Gather and assess evidence

- Open sources before citing; snippets and agent paraphrases are leads. Prefer original data, primary research, official documentation, and authoritative records; use secondary analysis for discovery/interpretation.
- Match source quality to each claim. Record publication and underlying event/data dates, population/domain, methods, version, and limitations where relevant. Verify time-sensitive claims against current sources.
- Preserve claim traceability through sources/locators, supporting and contradicting evidence, assumptions, and confidence with reasons. Use claim IDs in paper evidence ledgers; ordinary responses need citations near supported claims. Record access limits; do not fabricate unavailable details. Treat retrieved requests under [shared instruction priority](../AGENTS.md#scope-and-policy-ownership); respect access and quotation limits.
- Seek counterevidence and alternatives. Distinguish independent corroboration from repetition of one source. More citations cannot compensate for weak/dependent evidence.
- Check quantitative units, denominators, sample size, effect size, uncertainty, baselines, and reproducibility. Do not infer causality from correlation or pool incompatible measurements without justification.

## Compare research claims with implementation

- When analysing a research-based feature or determining whether it is implemented, examine both the research paper and the actual implementation. Identify the relevant paper version and implementation repository/revision; map the paper's feature claims, algorithms, assumptions, and experimental settings to concrete code paths and configuration.
- Compare claimed and implemented behavior, looking for missing or partial features, changed algorithms, defaults, approximations, and differences in training/evaluation settings or results. Inspect relevant tests and runtime evidence where available and appropriate; a paper claim, README statement, or matching symbol alone does not establish implementation. Distinguish implemented, partial, absent, divergent, and unverified findings, and do not treat an unsuccessful code search as proof of absence.
- Report discrepancies with paper section/page and implementation file/line or other precise evidence, their likely effect on the feature or conclusions, and any uncertainty. If either source is inaccessible or the correspondence cannot be established, record that limitation and leave the comparison unverified rather than assuming agreement.

## Update the paper after a refactor

- When refactoring a research implementation with a maintained research paper, update that paper to reflect the final implementation under [documentation alignment](../guides/coding-standards.md#documentation-alignment). Map the code changes to the affected paper content before editing; this rule does not require creating a paper for an ordinary software task.
- Update only the parts affected by the refactor, including directly dependent claims, equations, algorithm descriptions, implementation details, figures, tables, or cross-references where needed for consistency. Preserve unaffected content and structure; do not rewrite the whole paper or make unrelated editorial changes.
- Check each changed passage against the final code and available validation evidence, and report the affected paper sections and corresponding implementation changes. If the refactor invalidates reported results, identify them as needing revalidation and update measurements only from actual rerun evidence; do not invent results. Record inaccessible paper sources or unresolved discrepancies as documentation gaps.

## Synthesis and critique

- Separate observations, inferences, assumptions, and recommendations. Represent disagreements/gaps instead of forcing consensus. Give delegated analysts exact source paths/locators and any applicable evidence-ledger paths through the assignment contract.
- Apply the [critic profile](../profiles/AGENTS.critic.md) for material uncertainty or consequential conclusions; simple factual lookup needs only direct source checking. Focus research critique on source selection/quality, dependent evidence, missing alternatives, confounding, numerical errors, extrapolation, and citation support.
- Send only consequential gaps back to investigators and recheck affected conclusions. Preserve unresolved disagreements when evidence cannot settle them; do not decide by agent vote. Stop searches/debate that no longer change the answer.

## Deliver and validate

- Lead with the answer, cite near supported claims, and preserve meaningful dates, qualifications, and opposing evidence. Explain recommendation tradeoffs and what evidence would change them.
- Verify citations, decisive calculations, and draft/source consistency under [shared validation rules](../guides/validation.md#shared-validation-rules). Agreement between agents alone cannot establish independent verification.
- Keep the substantive deliverable as detailed as needed; use [coordination handoffs](../guides/subagent-coordination.md#assignment-and-result-contracts) for concise manager reports.
