# Git publication

Load before publication, PR creation/update/merge, or root session-end publication of repository work. Establish starting-branch evidence during local preflight; switching branches later grants no starting-main authority. Read-only work and scoped local edits alone do not require this publication module.

## Starting-on-main authorization

An agent whose assigned checkout is already on `main` at the start of its work is authorized to push validated, committed work to `origin/main` without asking the user for additional permission, including when `main` is the default branch. This applies to root and subagents; establish the starting branch during preflight. Subagents coordinate acceptance and publication with their immediate manager to avoid conflicting pushes. Switching to `main` later does not grant this authorization. Normal fast-forward pushes only: explicit no-push instructions, required checks, branch protections, and higher-priority or host restrictions still apply.

## Root session-end push

When finishing a session with repository work, root must push all commits reachable from the branch being worked on to the same branch on `origin`, including commits that predate the current task. This is the default push authorization; explicit user instructions not to push and higher-priority or host restrictions take precedence. Non-root agents return committed results for root to review and integrate unless explicitly assigned a push or covered by the [starting-on-main authorization](#starting-on-main-authorization).

1. Complete required integration, validation, reviews, task-owned commits, and worktree reconciliation. Confirm the active checkout, named branch, commit SHA, and `origin` URL under [scope and preflight](git-usage.md#scope-and-preflight). Do not choose another branch or remote if the intended destination is unclear.
2. Push only that branch with an explicit destination, for example `git push origin "HEAD:refs/heads/<branch>"` after replacing `<branch>` with the confirmed branch name. If upstream tracking is missing, add `--set-upstream` to this same push. Never use `--all`, `--mirror`, tag pushes, or force options for this default; do not publish unrelated branches.
3. Verify the push succeeded and the matching branch on `origin` contains the final local commit; report the branch, commit SHA, and push outcome. A rejected or unverified push does not establish completion of this step.
4. If a missing remote, detached HEAD, authentication, permissions, non-fast-forward rejection, protection, explicit no-push instruction, or another concrete blocker prevents the push, preserve local commits and report the blocker, unpushed SHA(s), and recovery owner. Do not bypass restrictions, rewrite shared history, or silently substitute another destination.

## Pull requests and merge rules

- When creating or changing workflow files, load [GitHub Actions guidance](github-actions.md) for authoring, local verification, and hosted runtime controls.
- Use the repository's PR template when present. Describe the problem, resulting behavior, relevant context, validation, and remaining limitations. If no template exists, use those fields directly.
- Required CI/CD checks, including configured GitHub Actions, must pass for the revision being merged. Local checks do not replace required CI; unavailable checks are unverified, not passed.
- Require at least one System Architect (SA) approval and any additional repository-mandated reviews. The author must not approve or merge their own PR. A subagent review is useful evidence but does not substitute for required repository approval.
- Merge only within the user's authorization and repository protections. Keep PR title and description aligned with the final diff. Do not message reviewers unless authorized.
- After confirmed merge, delete the task-owned source branch when no longer needed and retire its worktree under [safe cleanup](git-worktrees.md#safe-cleanup). Preserve branches still used by another stream; record deferred cleanup. Worktree retirement also applies to preserved results that do not require a PR merge.
