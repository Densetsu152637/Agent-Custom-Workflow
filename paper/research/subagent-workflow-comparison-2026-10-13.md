# RESEARCH-001: Subagent workflow comparison

Date/access checkpoint: 2026-10-13. Policy revision: `8690e97d9d33567f15eaedfb90a6c571c277c39e`, branch `main`, repository `Agent-Custom-Workflow`.

Exact user prompt:

> based on subagent workflow precedents from online, how does this custom one compare to some existing ones in terms of subagent efficiency, work speed, work precision and root agent utilisation of subagents?

## Scope and method

Compare the written custom policy with documented architectures and published evaluations. This is a policy assessment, not a benchmark of this repository's runtime. Gather primary sources, inspect actual local policy, distinguish source measurements from causal predictions, and critique consequential claims before synthesis. Local discovery was read-only; only these research artifacts were added. No workflow policy was changed.

The root coordinated three independent assignments and accepted their evidence after primary-source spot checks:

| Assignment | Configured model/effort | Verified tier and ceiling |
| --- | --- | --- |
| W1: official precedent gathering | `gpt-6.1-sol`, high | Specialist; balanced general ceiling |
| W2: difficult empirical interpretation and critique | `gpt-6-astra`, high | Frontier; balanced research exception |
| W3: local policy assessment and retained record | `gpt-6.1-sol`, high | Specialist; balanced general ceiling |

Capability mapping used host descriptions. Reliable cost comparisons and actual token telemetry were unavailable; no local benchmark was executed. The implementation of external systems was not audited: product documentation establishes documented behaviour, and research papers establish reported experiments, not parity with this workflow.

## Question map and conclusion

| Question | Criterion | Policy assessment; predicted effect | Unresolved evidence |
| --- | --- | --- | --- |
| Q1: Subagent efficiency | Accepted outcomes per total tokens/cost and coordination | Context isolation, compact handoffs and suitable model routing should reduce duplicate work. Mandatory delegation of even small cohesive root work adds fixed setup cost. | No matched local token/cost evaluation. |
| Q2: Work speed | End-to-end elapsed time, including tools, waits, integration and validation | Independent streams and critical-path scheduling can shorten execution. Root review and serial dependencies can dominate short or tightly coupled tasks. | No local elapsed-time baseline or root-queue measurement. |
| Q3: Work precision | First-pass acceptance, evidence correctness and escaped defects | Explicit ownership, revision-specific evidence, integrated acceptance and focused critique provide strong error controls. | Written rules do not prove consistent execution or adequate tests. |
| Q4: Root utilisation of subagents | Meaningful delegated output and root coordination per accepted outcome | Substantive delegation is mandatory; token delegation is prohibited. Root acceptance/integration can become a bottleneck. | No measured worker waiting time or root attention distribution. |

The strongest supported conclusion is architectural: this workflow prioritises meaningful delegation and verifiable acceptance. It is not demonstrated to be faster, cheaper or more accurate than an existing system. Expected benefits are largest for independent substantial work and less certain for short serial tasks.

## Local policy evidence ledger

`LOC` rows are observations at the policy revision above; predicted effects belong to the question map and recommendations. Links point to current files, while line locators identify the assessed revision.

| ID | Exact owner/locator | Observed rule | Relevance |
| --- | --- | --- | --- |
| LOC-01 | [Root](../../workflows/AGENTS.root.md), line 9 | Delegate every nontrivial task and all tool execution, including small/cohesive actions; root retains routing, coordination, review and acceptance; workers must own meaningful output. | Q1/Q4: strong utilisation, fixed delegation overhead. |
| LOC-02 | [Manager](../../workflows/AGENTS.manager.md), lines 26-35 | Select least-cost verified suitable capability by assignment, record model/tier/effort/ceiling, disclose unavailable reliable cost comparisons. | Q1: sound routing procedure, unproven cost optimum. |
| LOC-03 | [Manager](../../workflows/AGENTS.manager.md), lines 41-45 | Child managers may execute bounded cohesive work directly; each added layer must shrink useful deliverables; no policy depth limit. | Q1/Q4: avoids pointless recursion if enforced. |
| LOC-04 | [Manager](../../workflows/AGENTS.manager.md), lines 48-54 | Start with at most three active children tree-wide; expand with justification; unblock dependencies first; parallelise independent work; batch trivial changes; add managers only to reduce parent load. | Q1/Q2/Q4: bounded parallel scheduling. |
| LOC-05 | [Coordination](../../guides/subagent-coordination.md), lines 7-12 | Proportional compact/expanded contracts, persistent evidence references, unique task IDs, immediate-manager acceptance and conditional metrics. | Q1/Q3: traceable handoffs without duplicate summaries. |
| LOC-06 | [Coordination](../../guides/subagent-coordination.md), lines 16-19 | Accessible exact owner manifest; five mandatory policy/profile owners per leaf; missing instructions stop affected execution. | Q1/Q3: reliable instruction loading with setup overhead. |
| LOC-07 | [Coordination](../../guides/subagent-coordination.md), lines 23-26 | Fresh context for unrelated work, related-worker reuse with compact deltas, retained checkpoints and bounded outputs. | Q1: controls context growth and repeated discovery. |
| LOC-08 | [Validation](../../guides/validation.md), lines 7-12 | Check actual artifact/revision, distinguish passed/failed/unrun, validate integration, rerun affected checks only, use smallest meaningful check set without omitting gates. | Q2/Q3: precise acceptance and fewer redundant checks. |
| LOC-09 | [Critic](../../profiles/AGENTS.critic.md), lines 5-9; [Validator](../../profiles/AGENTS.validator.md), lines 5-8 | Independent focused critique; actionable substantiated findings; preserve disagreement; validator cannot repair or relax acceptance. | Q3: safeguards against false completion and anchoring. |
| LOC-10 | [Accounting](../../guides/usage-accounting.md), lines 5-9 | Actual scoped telemetry only; elapsed includes tools/waits without summing concurrent durations; no cumulative double counting. | Q1/Q2: valid accounting definitions, no throughput benchmark. |

The precision advantage is a design inference about explicit controls. It is not an observed difference in defect rate. Mandatory manifests and manager acceptance improve traceability but consume context and root attention; their net value depends on task complexity and consequences.

## Precedent evidence ledger

All sources were opened on the access date. Bibliography keys are in [references.bibtex](../references.bibtex). Documentation is mutable and should be rechecked before relying on product limits. Source excerpts were paraphrased; no verbatim article passages were retained.

| ID/key | Source and locator | Supported comparison | Limits |
| --- | --- | --- | --- |
| EXT-01 `anthropicClaudeCodeSubagents` | [Create custom subagents](https://code.claude.com/docs/en/sub-agents), “Choose between subagents and main conversation” and “Let subagents spawn their own subagents” | Separate contexts and compact returns resemble this workflow. Claude guidance keeps quick, shared-context or latency-sensitive work in the main conversation; this workflow mandates delegation. Current documented default nesting is three layers. | Product guidance, not controlled efficiency evidence; do not describe subagents as universally unable to nest. |
| EXT-02 `anthropicClaudeCodeAgentTeams` | [Orchestrate teams of Claude Code sessions](https://code.claude.com/docs/en/agent-teams), subagent comparison and best practices | Teams support peer messaging/shared tasks; this workflow routes assignment/redirection through immediate managers. Peer collaboration may relieve a lead bottleneck while adding coordination and token use. | Architecture comparison; no measured relative result for this custom workflow. |
| EXT-03 `hadfield2025MultiAgentResearch` | [How we built our multi-agent research system](https://www.anthropic.com/engineering/multi-agent-research-system), benefits, prompting, parallel tools and appendix | Lead/worker decomposition, scoped assignments, context compression and persistent artifact references closely match this workflow. Anthropic reports 90.2% improvement over single Opus 4 on an internal research eval with an Opus 4/Sonnet 4 team; up to 90% time reduction combines parallel agents and tools; approximately 15 times chat tokens is a chat baseline. | Vendor internal results; no published sample, score or uncertainty for the 90.2% claim. Neither the timing nor token number isolates subagent effects against a matched single agent. |
| EXT-04 `erikS2024EffectiveAgents` | [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents), simplicity, orchestrator-workers and evaluator-optimizer | Orchestrator-worker and evaluator-optimizer precedents support bounded delegation and critique. The guidance favours the simplest sufficient architecture; universal root delegation is a stronger commitment. | Design guidance, not experimental proof of a winning topology. |
| EXT-05 `crewaiHierarchicalProcess` | [Hierarchical Process](https://docs.crewai.com/v1.15.27/en/learn/hierarchical-process), version 1.15.27, overview and implementation | Closest organisational analogue: a manager delegates by role/capability and validates results. CrewAI exposes a runtime hierarchical process plus iteration/rate controls; this repository supplies portable Markdown policy whose enforcement depends on the host and agent. | Documentation's efficiency claims are not comparative measurements. Runtime controls do not guarantee correct outcomes. |
| EXT-06 `microsoftAutoGenSelectorGroupChat` | [Selector Group Chat](https://microsoft.github.io/autogen/stable/user-guide/agentchat-user-guide/selector-group-chat.html), stable docs, team execution | This particular AutoGen team selects a speaker for each turn and broadcasts conversation history, with actual selection and termination controls. The custom workflow instead assigns independent bounded worker execution and summarised returns through managers. | Applies to SelectorGroupChat, not all AutoGen patterns; neither topology is measured against this custom policy. |
| EXT-07 `kim2026scalingagents` | [Towards a Science of Scaling Agent Systems](https://arxiv.org/abs/2512.08296v3), v3 revised 2026-04-08; sections 3.1 and 4.3 and limitations | Controlled study of 260 configurations, six benchmarks, five topologies and three model families reports strong task dependence: centralised coordination improved decomposable financial reasoning while collaborative variants harmed sequential planning and the studied software tasks. Supports testing task structure rather than assuming more agents improve performance. | Six task clusters limit inference; code/terminal evaluations used 20 tasks each. Several effects weaken under cluster-aware inference. No universal 45% routing threshold. Trace-error amplification measures extra computational work, not failure probability. Does not predict this workflow's performance. |
| EXT-08 `cemri2025mast` | [Why Do Multi-Agent LLM Systems Fail?](https://arxiv.org/abs/2503.13657v3), v3 revised 2025-10-26; MAST development and dataset | 1,642 traces across seven frameworks; taxonomy developed from 150 traces identifies 14 modes under system design, inter-agent alignment and verification. The custom contracts/ownership/acceptance rules address analogous failure classes. | Annotation/judge agreement is imperfect. A failure taxonomy does not prove this policy prevents those failures. |
| EXT-09 `xia2024agentless` | [Agentless: Demystifying LLM-based Software Engineering Agents](https://arxiv.org/abs/2407.01489v2), v2 revised 2024-10-29; approach and evaluation | Historical counterexample to complexity as a quality proxy: a fixed localisation, repair and validation pipeline was effective on the studied software-repair benchmark. Supports including a simple baseline in local evaluation. | Historical unmatched baselines and possible benchmark leakage; no current leaderboard claim or proof that fixed pipelines fit this user's broader tasks. |

The evidence supports task-dependent orchestration, not a benchmark ranking. Compared with CrewAI's hierarchy, the custom workflow specifies more repository-specific ownership, instruction-loading and revision-validation procedure. Compared with Claude's selective subagents and AutoGen's selected-speaker team, it commits more strongly to root delegation and manager-controlled acceptance. These are differences in documented design, not measured quality superiority.

## Recommendations

1. Preserve meaningful root delegation; reduce dispatch cost by batching related small actions into one cohesive worker assignment and reusing related workers with compact deltas. Existing rules already support this (LOC-04/07).
2. Keep trees shallow unless a new manager removes distinct dependency/integration work from its parent. Expand beyond three active children only for independent ready work with available tool, integration and validation capacity (LOC-03/04).
3. Retain exact-revision/integrated acceptance and focused critique for material uncertainty. These are the strongest precision controls; reduce repeated unaffected checks, not required gates (LOC-08/09).
4. Run a small matched evaluation across short serial tasks, decomposable research, isolated implementation streams and integration-heavy changes. Track accepted task success and escaped defects; all root/descendant tokens per accepted task including failed attempts; median/p90 end-to-end elapsed time including integration; first-pass worker acceptance and rework; root review queue, time and tokens. Match model/effort/tool/acceptance conditions; report unavailable telemetry honestly (LOC-10). A small pilot can expose large differences but cannot establish reliable p90 estimates or universal routing rules.
5. If later measurements justify it and the user wants a different utilisation tradeoff, test a narrowly scoped root-direct variant for short cohesive tasks. This would require an explicit policy change: current root rules prohibit task size/cohesion as exceptions. It is an optional experiment, not the default recommendation.

## Limitations and reuse

This record does not rank workflows by benchmark score. Local policy, vendor product guidance and heterogeneous research evaluations are different evidence types. External results cannot establish this workflow's token efficiency, speed, correctness or model suitability. Cross-provider token/cost definitions must remain separate. Future entries should retain this historical assessment and explain changes in policy revision, tasks, models, tools, budgets or acceptance criteria rather than overwrite its findings.
