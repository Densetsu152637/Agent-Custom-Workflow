# Agent instructions

## Scope and policy ownership

Follow higher-priority and repository-level instructions and explicit user constraints. Unless assigned otherwise, act as the root. At task intake, load and apply the [root delegation default](workflows/AGENTS.root.md#delegation-default): automatically dispatch capable subagents for non-trivial work without waiting for a user request, subject to its exceptions. Load the manager workflow when directing descendants.

This file owns shared priority, discovery, execution defaults, and the companion index. Each companion owns its topic; link to it and load applicable sections rather than duplicating policy. Profiles describe assignments, not permissions or instruction priority. Companions inherit this file. Keep links and consumers current when moving rules; do not assume automatic discovery.

## Workflows

- Root: [Responsibilities and reporting](workflows/AGENTS.root.md).
- Root personality: [Default and specialist-personality guidance](personalities/README.md).
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
- Git operations or parallel editing: [Git usage](guides/git-usage.md).
- Creating or changing GitHub Actions workflows: [GitHub Actions](guides/github-actions.md).
- Container/Compose operations: [Container usage](guides/container-usage.md).
- Configuration or secrets: [Environment configuration](guides/environment-configuration.md).
- Reusable failure lessons: [Learning](learning/README.md).

## Editing and temporary artifacts

- Edit authoritative files in the assigned checkout with permitted tools; use [Git isolation](guides/git-usage.md#parallel-work-and-worktrees) where required. Review diffs or stable artifacts, without ad hoc backup/draft trees or routine one-off installer/check scripts.
- Use host permissions for protected targets; shadow drafts do not replace authorization.
- Create scratch artifacts only for a concrete task/tool need, at an assigned temporary location separate from deliverables. Keep their scope minimal, clean them when unneeded, and preserve required [handoff evidence](guides/subagent-coordination.md#assignment-and-result-contracts).

## Context and discovery

- Before affected work, load its applicable owners and relevant README/source sections, including nested instructions. A link is not a requirement to load its target: follow the stated trigger. Discover progressively; avoid whole-repository dumps.
- Apply domain triggers to the reasoning being requested, including plans and reviews. Read-only scope, prohibited execution, or missing data/media limits what can be done or concluded; it does not remove the relevant methods owner. Loading an owner does not grant execution authority or a capability exception. Before declaring that no additional owner applies, check both indexes above; a tool-specific guide complements, rather than replaces, a triggered domain workflow.
- Complete authoritative text already available in current context counts as loaded. Reuse it while unchanged; reread changed sections, missing text, or sources represented only by a summary after compaction/handoff. Record exact owner paths for delegated work under the coordination contract.
- Count only text actually returned or supplied as loaded. A successful read command with truncated output does not establish a complete read. Recover missing applicable text one file or smaller line range at a time before opening unrelated owners; reduce the range again if output still truncates. Claim a complete file or named section only when all of its text was returned; otherwise report the covered ranges and remaining gap. Unrelated sections need not be reread merely to claim completeness.
- Search narrowly, return bounded excerpts/logs/diffs, and widen only when needed. Retain decisive evidence instead of repeating raw output.
- Apply skills/plugins to the actual requested workflow, not broad keyword overlap. When authoring skill descriptions, keep triggers short and specific; put detailed procedures in conditionally loaded references.

## Execution defaults

- Establish the outcome, scope, known paths, acceptance checks, and stopping condition. Resolve routine choices from available evidence; ask only for missing information or authority that materially affects the result.
- Keep related work together and pass compact deltas. Use fresh context for unrelated assignments; suggest a new chat when unrelated history materially impedes direct work, without creating one unless requested.
- When effort controls are exposed, use low for routine edits/extraction, medium for ordinary implementation/debugging, and deeper effort for difficult uncertain analysis. Honor explicit settings and host controls; instructions do not change hidden runtime settings.
- Keep communication and evidence proportional to the task. Stop exploration and checks when acceptance is established; preserve mandatory gates under [validation](guides/validation.md#shared-validation-rules).
