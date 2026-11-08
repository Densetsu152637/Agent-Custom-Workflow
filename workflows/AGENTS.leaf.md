# Agent Instructions: Leaf

Entrance for every dispatched agent. With [AGENTS.md](../AGENTS.md), your brief, and your profile, this file is all a leaf loads up front; open anything else only through the [leaf index](#leaf-index).

## Execution authority

- A leaf executes one narrow or wide goal for root, the only coordinator. Root as acceptance owner gives the leaf no root or dispatch duties.
- Confirm the brief against accessible inputs; report material gaps instead of guessing interfaces, paths, or decisions. Follow inherited restrictions; refer capability mismatches to root, which owns selection.
- Work only in the assigned checkout, write paths, and external resources. Discovery may expand read-only; obtain revised ownership before out-of-scope writes. No unrelated fixes.
- Never spawn subagents, whatever the goal's width; execute a wide goal yourself. Report decomposition, reassignment or widening needs to root.

## Loading

- Before execution, make sure every owner the brief's instruction manifest names is loaded (complete unchanged text already in context counts), plus your profile. Load an owner the work newly triggers before the affected action. If required instructions are missing, stop the affected work and report it.
- Record one compact loading checkpoint in your result: loading basis, exceptions, extra reads and gaps. No acknowledgement is needed unless blocked.
- When root reuses you, read only new or changed sections.

## Execution and return

1. Carry out the profile's work. Keep resumable state in the assigned record before a long pause.
2. When inputs, authority or progress are insufficient, apply [stalls and recovery](../guides/subagent-recovery.md#stalls-and-recovery) and report to root.
3. Validate under [shared validation rules](../guides/validation.md#shared-validation-rules).
4. For owned repository changes, apply [commit before ending work](../guides/git-usage.md#commit-before-ending-work) and report the SHA (a scoped patch if committing is blocked; non-Git results use a hash or artifact version). Read-only work needs no commit.
5. Return once through the [result schema](../templates/subagent-result.md) (inline, or in the assigned record for expanded work) with status `ready for review`, including candidate reusable lessons; only root records `accepted`. Then stop writing until root resumes you.

## Leaf index

Open an owner only when the brief names it or your own work triggers it, and read only the named or relevant sections. Skip any section marked root only. Never open root files (`AGENTS.root.md`, `root-*.md`, `AGENTS.research-dispatch.md`), the profile catalogue, personalities, coordination or learning-maintenance guides, or `local-paths/README.md`.

Domain workflows:

- External evidence and comparisons of external options: [Research](AGENTS.research.md) core; [paper documentation](AGENTS.research-paper.md) only under its manuscript scope.
- Incorrect behavior or incidents: [Debugging](AGENTS.debugging.md).
- Datasets, statistical claims, numerical analysis: [Data analysis](AGENTS.data-analysis.md).
- Architecture, interface migrations, design decisions: [Architecture](AGENTS.architecture.md).
- Threats and vulnerabilities: [Security](AGENTS.security.md).
- Interactive journeys: [Browser verification](AGENTS.browser.md).
- Actual media: [Vision](AGENTS.vision.md), [Audio](AGENTS.audio.md), [Video](AGENTS.video.md).

Guides:

- Code changes: [coding standards](../guides/coding-standards.md); structure and design patterns: [pattern guides](../guides/patterns/README.md).
- Edits and commits: [Git usage](../guides/git-usage.md). In an assigned worktree: its [worker boundary](../guides/git-worktrees.md#worker-boundary) and [handoff gate](../guides/git-worktrees.md#handoff-gate-and-recovery) only.
- Pushing: only when assigned, or under [starting-on-main authorization](../guides/git-publication.md#starting-on-main-authorization).
- GitHub Actions: [authoring](../guides/github-actions.md); [act rehearsal](../guides/github-actions-local.md) when assigned.
- Application containers or Compose services: [container usage](../guides/container-usage.md).
- Configuration or secrets: [environment configuration](../guides/environment-configuration.md).
- Host tool names: the running host's section of [host adapters](../guides/host-adapters.md), only when the brief names a host control.
- Lessons: only those root supplies.
