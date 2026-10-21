# Git worktrees and integration

Load for parallel write streams, worktree creation/use, integration, or task-created worktree reconciliation and cleanup. Apply [local Git preflight](git-usage.md#scope-and-preflight) before edits or Git mutations. Read-only review in an existing stable checkout does not require mutation procedures.

## Parallel work and worktrees

- Give each concurrent write stream its own branch and worktree. Reuse an existing suitable task-owned worktree when safe. Read-only reviewers and planners may share a stable checkout; planners can return inline drafts to one integration writer. A single-writer restriction serializes writes, not independent read-only planning. If worktrees are unavailable or prohibited, serialize writers rather than switching branches in a shared directory.
- The coordinating manager assigns integration and cleanup owners and records each stream's owner, absolute worktree path, branch, base commit, owned files, dependencies, and required checks. Pass this record in each agent's brief; apply [worktree cleanup ownership](#safe-cleanup) throughout the task.
- Prefer the host's managed-worktree tools when available and follow their lifecycle rules. Otherwise use Git worktrees. Each worker runs commands with an explicit working directory or `git -C` pointing to its assigned worktree.
- Worktrees isolate files and indexes, but share repository metadata and refs. Never check out the same branch in multiple worktrees with force options. Coordinate branch/ref mutations and repository-wide configuration or maintenance through one owner. Avoid global Git configuration changes.
- Start independent streams from an agreed committed base. New worktrees do not contain another checkout's uncommitted changes. Transfer required changes explicitly as reviewed commits or a scoped patch, with ownership and user changes preserved.
- Isolate build outputs, ports, test databases, generated artifacts, and temporary paths too. A worktree does not isolate external services. Serialize tests that mutate the same resource.
- Before doing work in parallel, see if there are overlapping file/API changes and contracts, as these can be serialised before parallel work starts. Serialize changes to shared schemas, lockfiles, migrations, or interfaces when they would conflict during integration.

CLI example, after resolving the actual paths and base commit (replace all placeholders; do not execute them literally):

```text
git -C "<repository>" worktree add -b feat/task-component "<new-worktree-path>" "<base-commit>"
git -C "<new-worktree-path>" status --short --branch
```

## Integration

1. Use the [coordination result contract](subagent-coordination.md#assignment-and-result-contracts) and [result schema](../templates/subagent-result.md) for worker handoffs; include the assigned Git checkout/branch and commit SHA under [commit before ending work](git-usage.md#commit-before-ending-work). A scoped patch is a recovery artifact when a disclosed blocker prevents committing. Hand off only a stable result.
2. One integration owner applies results in dependency order in the assigned integration checkout. Use the repository's merge/cherry-pick convention; do not blindly apply both a branch merge and its commits.
3. Resolve conflicts by understanding both changes and their contracts. Coordinate unclear intent with the responsible manager. Do not accept all of one side or discard unrelated edits to make conflicts disappear.
4. Inspect the combined diff and apply [shared validation rules](validation.md#shared-validation-rules) to the integrated revision.
5. Pause only the dependent integration step when blocked; continue independent authorized work. Report unresolved conflicts and failing checks explicitly.

## Safe cleanup

- Creating a worktree includes responsibility for its retirement; cleanup of task-created worktrees is part of the task's default scope. The coordinating manager owns reconciliation of all worktrees created for its workstream, including descendants' worktrees; the root verifies reconciliation across the task before closing it. For direct work, the creating agent owns cleanup. Delegating removal does not transfer accountability unless the receiving owner explicitly accepts it.
- Track every task-created worktree from creation through retirement, including its absolute path, branch, creating stream, cleanup owner, and current use. Before task completion, archive or safely remove every such worktree that is no longer needed. An inactive worktree is not, by itself, evidence of ownership or safe removal; do not remove pre-existing, shared, primary, pinned, or user-retained worktrees without applicable ownership and host authorization.
- For every retained worktree, report its absolute path, branch, cleanup owner, concrete reason for retention, and the condition or next action that permits cleanup. Pending review, required artifacts, active consumers, or a host restriction may justify retention; task completion alone does not justify leaving an unused worktree behind. On cancellation or handoff, retire unneeded worktrees or explicitly transfer/report outstanding cleanup under the same rules.
- Confirm all agents/processes have stopped using the worktree. Inspect tracked and untracked changes and needed ignored artifacts; preserve required outputs before removal.
- Verify the result was integrated or otherwise preserved. A squash merge may require checking PR status and resulting content rather than relying solely on ancestry.
- Archive managed worktrees through their host tool. For ordinary worktrees, use `git worktree remove "<verified-worktree-path>"`; do not recursively delete the directory or use force to bypass dirty-worktree protection.
- Remove only task-owned branches after checking they are no longer checked out or needed. Use normal branch deletion where possible; do not force-delete merely because squash history is not recognized as merged.
- Report the final branch/worktree state, validation results, and any deliberately preserved changes or deferred cleanup.
