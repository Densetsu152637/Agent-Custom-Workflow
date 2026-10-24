# Agent instructions

## Scope and policy ownership

Unless assigned otherwise, act as the root. At task intake a manager loads and applies the [root delegation default](workflows/root-delegation.md#delegation-default): dispatch capable subagents for non-trivial work without waiting for a user request, subject to its exceptions. Load the manager workflow when directing descendants. Assigned leaves do not open root-delegation instructions.

The top-level root (the main conversation agent) must load its [personality](personalities/README.md), the one the personal instruction file [declares](personalities/README.md#selection), at intake, before its first user-facing reply. Host output styles govern reply form and never waive loading; on conflict the host or user style wins on form. Every dispatched agent, including child managers, never loads or adopts a personality.

This file owns shared priority, discovery, execution defaults, and the companion index. Each companion owns its topic; link rather than duplicate. Profiles describe assignments, not permissions or priority. Companions inherit this file. Keep links and consumers current when moving rules.

An agent whose assigned checkout is already on `main` at task start may make scoped task commits and push validated work to `origin/main` without asking the user again. Procedure and limits (no-push instructions, required checks, branch protections, host restrictions) follow [commit](guides/git-usage.md#commit-before-ending-work) and [starting-on-main authorization](guides/git-publication.md#starting-on-main-authorization).

## Workflows

- Root: [Responsibilities and reporting](workflows/AGENTS.root.md).
- Root only, conversation tone: [Personality selection and loading](personalities/README.md).
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

- Host tool mapping (Claude Code, Codex): [Host adapters](guides/host-adapters.md).
- Handoffs, retained context, or recovery: [Coordination](guides/subagent-coordination.md).
- Acceptance evidence: [Validation](guides/validation.md).
- Implementation changes: [Coding standards](guides/coding-standards.md); function/class structure and design patterns with per-language idioms: [Pattern guides](guides/patterns/README.md).
- Local edits/Git mutations: [Git usage](guides/git-usage.md); parallel writes/integration/cleanup: [Worktrees](guides/git-worktrees.md); pushes/PRs/merges: [Publication](guides/git-publication.md).
- GitHub Actions authoring/verification, including plans: [GitHub Actions](guides/github-actions.md); act rehearsal/planning: also [Local rehearsal](guides/github-actions-local.md).
- Managing application containers/Compose services: [Container usage](guides/container-usage.md); tools merely using their own containers do not trigger it.
- Configuration or secrets: [Environment configuration](guides/environment-configuration.md).
- Managers selecting or maintaining reusable failure lessons: [Learning](learning/README.md); workers load only assigned applicable lessons.

## Editing and temporary artifacts

- Edit authoritative files in the assigned checkout; use [Git isolation](guides/git-worktrees.md#parallel-work-and-worktrees) where required. No ad hoc backup/draft trees or routine one-off installer/check scripts. Shadow drafts do not replace host authorization for protected targets.
- Create scratch artifacts only for a concrete need, at an assigned temporary location separate from deliverables; clean them up and preserve required [handoff evidence](guides/subagent-coordination.md#assignment-and-result-contracts).

## Context and discovery

- Decide applicability from index labels and the assigned role/profile before opening owner bodies; then load triggered owners and relevant sections, including nested instructions. Do not sample untriggered owners or search owner bodies to confirm non-applicability. An anchored reference requires only its named section. An assigned leaf/profile needs no root, manager or profile-catalogue read. For genuinely ambiguous applicability, inspect only the narrow excerpt needed.
- Apply domain triggers to the reasoning requested, including plans and reviews. Read-only scope, prohibited execution, or missing data/media limits actions and conclusions, not triggered instruction reads; loading an owner grants no execution authority or capability exception. Before declaring that no additional owner applies, check both indexes above; a tool-specific guide complements a triggered domain workflow.
- Complete authoritative text already in context counts as loaded; reuse it while unchanged. Reread changed sections, missing text, or sources represented only by a summary after compaction/handoff. Record exact owner paths for delegated work under the coordination contract.
- On root recovery after compaction or handoff, follow the [root context-recovery contract](workflows/root-recovery.md#context-recovery) before substantive execution, dispatch, or publication.
- Count only text actually returned as loaded; truncated output is not a complete read. Recover missing text one file or smaller range at a time. Claim a complete file or section only when all of it was returned; otherwise report covered ranges and the gap.
- Apply skills/plugins to the actual requested workflow, not keyword overlap. Skill descriptions keep triggers short; detailed procedures go in conditionally loaded references.

## Execution defaults

- Resolve routine choices from available evidence; ask only for missing information or authority that materially affects the result.
- Keep related work together and pass compact deltas; use fresh context for unrelated assignments. Suggest a new chat when unrelated history materially impedes direct work, without creating one unless requested.
- When effort controls are exposed, use low for routine edits/extraction, medium for ordinary implementation/debugging, deeper for difficult uncertain analysis. Honor explicit settings and host controls.
- Stop exploration and checks when acceptance is established; preserve mandatory gates under [validation](guides/validation.md#shared-validation-rules).
