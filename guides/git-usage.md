# Git usage

## Scope and preflight

Load this core before local edits or Git mutations. Read-only work needs no mutation, commit or publication procedures. Load [worktrees and integration](git-worktrees.md) for parallel write streams, integration or worktree cleanup; load [publication](git-publication.md) for pushing, PR/merge operations and root session-end publication. The authorized [root session-end push](git-publication.md#root-session-end-push) is governed there. Other publication, merging, and contacting reviewers require separate task authorization.

Before edits or Git mutations:

1. Confirm the repository and checkout with `git rev-parse --show-toplevel`, `git status --short --branch`, and `git worktree list --porcelain`.
2. Identify the intended base branch/commit, current branch, active worktrees, and existing staged, unstaged, and untracked changes. Inspect relevant diffs; do not assume a clean checkout or that the current branch is the requested base.
3. Preserve changes owned by the user or other agents. Do not reset, clean, stash, overwrite, switch their branch, or rewrite their commits to make your task easier.
4. If the folder is not a repository, report that and perform applicable file work. Do not initialize a repository unless requested.

## Branches and commits

| Change         | Branch prefix | Commit type               |
| -------------- | ------------- | ------------------------- |
| Feature        | `feat/`       | `feat`                    |
| Fix            | `fix/`        | `fix`                     |
| Temporary work | `temp/`       | `temp` (local convention) |
| Maintenance    | `chore/`      | `chore`                   |
| Documentation  | `docs/`       | `docs`                    |
| Formatting     | `style/`      | `style`                   |
| Refactor       | `refactor/`   | `refactor`                |
| Tests          | `test/`       | `test`                    |
| CI             | `ci/`         | `ci`                      |

- Use a short descriptive branch suffix, for example `feat/login-page`. Follow a required host prefix if one exists. Do not rename an existing user branch merely to satisfy this convention.
- Use `<type>(<optional-scope>): <imperative summary>`, for example `fix(auth): reject expired tokens`. Mark breaking changes with `!` and describe their impact in the body.
- Keep each commit focused on one coherent change with its relevant tests/docs. Avoid unrelated formatting and generated noise. Correct unpublished task-owned commits when needed; do not rewrite shared history without authorization.
- Stage explicit owned paths or reviewed hunks. Inspect both `git diff` and `git diff --cached` as relevant, and run `git diff --cached --check` before committing. Never include someone else's staged changes, credentials, or unrelated files; avoid blanket staging in a dirty shared checkout.
- Commit only on the assigned authorized branch under [commit before ending work](#commit-before-ending-work); do not commit or push to an unrelated branch without authorization. Do not force-push without explicit authorization; if authorized, use an appropriate lease and verify the expected remote state.

## Commit before ending work

Every agent, including root, managers, and leaves, must commit its intended task-owned repository changes before normal completion, termination, handoff, replacement, or cancellation when it controls that transition. This includes documentation and tests. Read-only work needs no commit; do not create empty commits. Explicit user instructions not to commit and higher-priority restrictions take precedence. Non-Git work follows [scope and preflight](#scope-and-preflight); do not initialize a repository to satisfy this rule.

Authorization to work in an assigned checkout includes scoped local commits on its assigned branch and root's [session-end push](git-publication.md#root-session-end-push). Non-root agents need explicit push authorization or the [starting-on-main authorization](git-publication.md#starting-on-main-authorization); merging and committing on unrelated branches remain separately authorized.

1. Review the actual owned changes and run appropriate checks under [validation](validation.md#shared-validation-rules). Inspect existing staging and preserve others' changes. Stage only intended owned paths or hunks, never blanket-add files, secrets, or another contributor's work. If existing staging cannot be safely separated, stop the commit and report the ownership blocker.
2. Inspect the complete staged diff and run `git diff --cached --check` before committing. Use a focused commit under [branches and commits](#branches-and-commits). Before a controlled interruption of incomplete work, make a recoverable checkpoint commit where possible; label it as incomplete and record validation limitations. A checkpoint does not establish acceptance or passing checks.
3. Verify the resulting commit SHA and inspect status for remaining owned staged, unstaged, or untracked changes. Commit intended residual changes before ending work; report the SHA, validation evidence, and any residuals with their ownership and reason through the [result contract](subagent-coordination.md#assignment-and-result-contracts).
4. If identity, hooks, permissions, conflicting ownership, or another real blocker prevents committing, preserve the work and report the concrete blocker and recovery owner. Do not bypass hooks or permissions, change Git configuration to force a commit, or claim that finalization succeeded. Abrupt forced shutdown may prevent a checkpoint; this rule applies wherever controls permit.
