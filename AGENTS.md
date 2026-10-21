# Agent instructions

## Scope and policy ownership

Follow higher-priority and repository-level instructions and explicit user constraints. Unless assigned otherwise, act as the root. At task intake, load and apply the [root delegation default](workflows/root-delegation.md#delegation-default): automatically dispatch capable subagents for non-trivial work without waiting for a user request, subject to its exceptions. Load the manager workflow when directing descendants. This intake route is for root/managers only; assigned leaves do not open root-delegation instructions.

This file owns shared priority, discovery, execution defaults, and the companion index. Each companion owns its topic; link to it and load applicable sections rather than duplicating policy. Profiles describe assignments, not permissions or instruction priority. Companions inherit this file. Keep links and consumers current when moving rules; do not assume automatic discovery.

An agent whose assigned checkout is already on `main` at task start may make scoped task commits and push validated work to `origin/main` without asking the user again. Follow the [Git guide's commit](guides/git-usage.md#commit-before-ending-work) and [starting-on-main authorization](guides/git-publication.md#starting-on-main-authorization) rules for procedure and limits, including explicit no-push instructions, required checks, branch protections, and host restrictions.

## Workflows

- Root: [Responsibilities and reporting](workflows/AGENTS.root.md).
- Root only, conversation tone: [Default and specialist-personality guidance](personalities/README.md).
- Directing descendants: [Manager](workflows/AGENTS.manager.md).
- Bounded delegated execution: [Leaf](workflows/AGENTS.leaf.md); choose an [assignment profile](profiles/README.md).
- External evidence, comparisons, and research plans: [Research](workflows/AGENTS.research.md).
- Visual inspection and its review plan: [Vision](workflows/AGENTS.vision.md).
- Recording inspection and its listening plan: [Audio](workflows/AGENTS.audio.md).
- Incorrect behavior or incidents: [Debugging](workflows/AGENTS.debugging.md).
- Datasets, statistical claims, and numerical analysis: [Data analysis](workflows/AGENTS.data-analysis.md).
- Interactive journeys: [Browser verification](workflows/AGENTS.browser.md).
- Architecture, interface migrations, and design decisions: [Architecture](workflows/AGENTS.architecture.md).
- Threats and vulnerabilities: [Security](workflows/AGENTS.security.md).
- Video sequences: [Video](workflows/AGENTS.video.md).

## Guides

- Handoffs, retained context, or recovery: [Coordination](guides/subagent-coordination.md).
- Acceptance evidence: [Validation](guides/validation.md).
- Implementation changes: [Coding standards](guides/coding-standards.md).
- Local edits/Git mutations: [Git usage](guides/git-usage.md); parallel writes/integration/cleanup: [Worktrees](guides/git-worktrees.md); pushes/PRs/merges: [Publication](guides/git-publication.md). Read-only work needs none of these mutation procedures.
- GitHub Actions authoring/verification, including plans: [GitHub Actions](guides/github-actions.md); act rehearsal/planning: also [Local rehearsal](guides/github-actions-local.md).
- Managing application containers/Compose services: [Container usage](guides/container-usage.md); tools merely using their own containers do not trigger it.
- Configuration or secrets: [Environment configuration](guides/environment-configuration.md).
- Managers selecting or maintaining reusable failure lessons: [Learning](learning/README.md); workers load only assigned applicable lessons.

## Editing and temporary artifacts

- Edit authoritative files in the assigned checkout with permitted tools; use [Git isolation](guides/git-worktrees.md#parallel-work-and-worktrees) where required. Review diffs or stable artifacts, without ad hoc backup/draft trees or routine one-off installer/check scripts.
- Use host permissions for protected targets; shadow drafts do not replace authorization.
- Create scratch artifacts only for a concrete task/tool need, at an assigned temporary location separate from deliverables. Keep their scope minimal, clean them when unneeded, and preserve required [handoff evidence](guides/subagent-coordination.md#assignment-and-result-contracts).

## Context and discovery

- Decide applicability from index labels and the assigned role/profile before opening owner bodies; then load triggered owners and relevant README/source sections, including nested instructions. Do not sample untriggered owners because they are linked, batch them with required reads, or broadly search owner bodies to confirm non-applicability. An anchored instruction reference requires only its named section, not the whole file. An assigned leaf/profile needs no root, manager or profile-catalogue confirmation read. For genuinely ambiguous applicability, state the reason and inspect only the narrow excerpt needed to decide. Discover progressively; avoid whole-repository dumps.
- Apply domain triggers to the reasoning being requested, including plans and reviews. Read-only scope, prohibited execution, or missing data/media limits actions and conclusions, not explicitly triggered role, procedure or methods instruction reads; loading them does not permit prohibited execution. Loading an owner does not grant execution authority or a capability exception. Before declaring that no additional owner applies, check both indexes above; a tool-specific guide complements, rather than replaces, a triggered domain workflow.
- Complete authoritative text already available in current context counts as loaded. Reuse it while unchanged; reread changed sections, missing text, or sources represented only by a summary after compaction/handoff. Record exact owner paths for delegated work under the coordination contract.
- On root recovery after compaction or handoff, follow the [root context-recovery contract](workflows/root-recovery.md#context-recovery) before substantive execution, dispatch, or publication.
- Count only text actually returned or supplied as loaded. A successful read command with truncated output does not establish a complete read. Recover missing applicable text one file or smaller line range at a time before opening unrelated owners; reduce the range again if output still truncates. Claim a complete file or named section only when all of its text was returned; otherwise report the covered ranges and remaining gap. Unrelated sections need not be reread merely to claim completeness.
- Search narrowly, return bounded excerpts/logs/diffs, and widen only when needed. Retain decisive evidence instead of repeating raw output.
- Apply skills/plugins to the actual requested workflow, not broad keyword overlap. When authoring skill descriptions, keep triggers short and specific; put detailed procedures in conditionally loaded references.

## Execution defaults

- Establish the outcome, scope, known paths, acceptance checks, and stopping condition. Resolve routine choices from available evidence; ask only for missing information or authority that materially affects the result.
- Keep related work together and pass compact deltas. Use fresh context for unrelated assignments; suggest a new chat when unrelated history materially impedes direct work, without creating one unless requested.
- When effort controls are exposed, use low for routine edits/extraction, medium for ordinary implementation/debugging, and deeper effort for difficult uncertain analysis. Honor explicit settings and host controls; instructions do not change hidden runtime settings.
- Keep communication and evidence proportional to the task. Stop exploration and checks when acceptance is established; preserve mandatory gates under [validation](guides/validation.md#shared-validation-rules).
