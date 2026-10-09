# Agent Instructions: Data Analysis Workflow

## Scope and inputs

Use this workflow for quantitative analysis, dataset transformations, statistical interpretation, or numerical conclusions. It owns analytical methods; use relevant spreadsheet, database, plotting, or other artifact skills for implementation and presentation.

For delegated work, use [manager dispatch](AGENTS.manager.md#dispatch-and-acceptance), the [leaf workflow](AGENTS.leaf.md) for leaf analysts, and [coordination](../guides/subagent-coordination.md) for handoffs and recovery. Load [research](AGENTS.research.md) when external source assessment or qualifying research interpretation is also required; its exception applies only to assignments meeting its eligibility.

- Define the question, intended decision, population, observation unit, time range, metrics, denominators, and useful-answer criteria before selecting methods. Distinguish exploratory analysis from a prespecified test.
- Identify authoritative datasets, revisions, schemas, collection methods, joins/keys, units, timezone conventions, and access limits. Preserve source data; write transformations and outputs only to assigned paths/resources.
- Assess row counts, missingness, duplicates, invalid values, coverage, sampling/selection bias, and inconsistent units or categories. Record material quality issues before drawing conclusions; handle sensitive data under [environment configuration](../guides/environment-configuration.md#secret-handling).

## Analysis

1. Build a reproducible transformation path from inputs to results using suitable queries, formulas, or code. Record filters, exclusions, imputations, join cardinality, aggregation level, and any manual changes. Never silently treat missing values as zero or discard inconvenient observations.
2. Inspect distributions and relevant subgroups before modeling. Check leakage, repeated observations, confounding, sample size, outliers, and whether method assumptions fit the data and question.
3. Report effect sizes, denominators, units, and uncertainty appropriate to the method. Distinguish association, causal inference, prediction, and description; label assumptions needed for a stronger interpretation.
4. For predictive work, choose evaluation splits appropriate to time, entities, and deployment conditions; keep preprocessing and tuning from leaking evaluation information. Compare against a meaningful baseline and identify limits of generalization.
5. Check sensitivity to consequential preprocessing and modeling choices, and account for multiple comparisons when relevant. Label post-hoc findings exploratory; do not select only favorable analyses.

## Deliver and validate

- Check decisive computations independently where practical. Verify join/count invariants, units, denominators, and reconciliation to source totals; use small known cases or an alternative calculation for material numerical risk.
- Validate the actual delivered tables, formulas, charts, and conclusions under [shared validation](../guides/validation.md#shared-validation-rules). Load [vision](AGENTS.vision.md) for rendered visual acceptance; visual appearance alone cannot establish numerical correctness.
- Deliver the answer, reproducible calculation paths, dataset revisions, consequential transformations, uncertainty, and material quality/access limitations. Charts must expose meaningful labels, scales, and units, and conclusions must trace to their calculations.
- Distinguish confirmed results from assumptions and analyses left unrun. Set a bounded checkpoint under [shared execution defaults](../AGENTS.md#execution-defaults), or [manager scheduling](AGENTS.manager.md#budgets-and-scheduling) for delegated work. Stop when additional analysis cannot change the decision within the assigned scope.
