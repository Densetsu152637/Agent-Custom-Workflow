# Git worktrees and integration

Load for parallel write streams, worktree creation/use, integration, or task-created worktree reconciliation and cleanup. Apply [local Git preflight](git-usage.md#scope-and-preflight) before edits or Git mutations. Read-only review in an existing stable checkout does not require mutation procedures.

## Parallel work and worktrees

- Give each concurrent write stream its own branch and worktree. Reuse an existing suitable task-owned worktree when safe. Read-only reviewers and planners may share a stable checkout; planners can return inline drafts to one integration writer. A single-writer restriction serializes writes, not independent read-only planning. If worktrees are unavailable or prohibited, serialize writers rather than switching branches in a shared directory.
- Admission, before dispatching parallel writers: the manager compares each stream's files, APIs/contracts, shared schemas, lockfiles, migrations, build outputs, generated artifacts, temporary paths, ports, databases, and external services. On overlap, serialize in dependency order or reassign to one stream before work starts. A worktree isolates files and indexes, not external services; serialize tests that mutate the same resource.
- Admit a stream only once its [record](#worktree-record) entry exists. Name its branch with the task ID (for example `feat/wt-1-component`, under the [branch convention](git-usage.md#branches-and-commits)). Place the worktree at a task-ID-specific path outside every other checkout's tracked tree. Start from an agreed committed base; uncommitted changes do not carry over, so transfer them as reviewed commits or a scoped patch, preserving ownership and user changes.
- Prefer the host's managed-worktree tools when available and follow their lifecycle rules; otherwise use Git worktrees. Worktrees share repository metadata and refs. Never check out one branch in several worktrees with force options. Route branch/ref mutations and repository-wide configuration or maintenance through one owner; avoid global Git configuration changes.
- Worker boundary: a worker runs commands with an explicit working directory or `git -C` in its assigned worktree and writes only there, to its owned files. It does not create nested worktrees or branches, switch branches, rebase/reset/delete other branches or refs, run `git worktree prune`, or touch another stream's worktree. On needing an out-of-scope write or discovering overlap, it stops that action, preserves state, and reports to its manager.
- Base drift: the manager alone decides whether a stream updates from a moved base (for example an upstream contract change); the stream's writer then merges or rebases only in its own worktree, rebasing only unshared commits, and reruns affected checks. Never force-push shared branches. Otherwise defer reconciliation to [integration](#integration).

CLI example, after resolving the actual paths and base commit (replace all placeholders; do not execute them literally):

```text
git -C "<repository>" worktree add -b feat/<task-id>-component "<new-worktree-path>" "<base-commit>"
git -C "<new-worktree-path>" status --short --branch
```

## Worktree record

One manager-owned record per task-created worktree, kept by the coordinating manager that created it; a child manager's entries roll into its parent's. Fields: task ID, absolute path, branch, base commit, creator, cleanup owner, owned files/resources, dependencies and required checks, state, and (when applicable) recovery ref or retention reason/condition. Briefs carry the stream's entry by these field names.

States: `planned` (manager, before creation) → `active` (manager, after `git worktree list --porcelain` shows it) → `handed off` (manager, on a handoff that passes the gate) → `integrated` (integration owner supplies proof) or `preserved` (recovery commit/patch recorded) → `retired` (cleanup owner supplies removal evidence). `retained` (reason, condition, owner) may replace any state after `active`. The manager records each transition from the named actor's evidence. Transferring accountability requires explicit acceptance.

### Handoff gate and recovery

- A stream is handed off only when `git -C "<path>" status --porcelain --untracked-files=all` shows nothing except declared artifacts, the head SHA and branch are reported, its processes, ports, containers, and services are stopped or named to an accepting owner, and generated artifacts are listed. The worker reports this through the [result schema](../templates/subagent-result.md) and stops writing.
- For a failed, cancelled, crashed, or dirty-orphaned stream, stop writers and preserve before any retirement: a checkpoint commit on a recovery branch or a scoped patch with path/hash, recorded in the entry. Never delete or clean to make the problem disappear. A worktree absent from the record is not task-owned; report it.

## Integration

1. Use the [coordination result contract](subagent-coordination.md#assignment-and-result-contracts) and [result schema](../templates/subagent-result.md) for worker handoffs, accepted only after the handoff gate; include the assigned Git checkout/branch and commit SHA under [commit before ending work](git-usage.md#commit-before-ending-work). A scoped patch is a recovery artifact when a disclosed blocker prevents committing. Hand off only a stable result.
2. One integration owner applies results in dependency order in the assigned integration checkout. Use the repository's merge/cherry-pick convention; do not blindly apply both a branch merge and its commits.
3. Resolve conflicts by understanding both changes and their contracts. Coordinate unclear intent with the responsible manager. Do not accept all of one side or discard unrelated edits to make conflicts disappear.
4. Inspect the combined diff and apply [shared validation rules](validation.md#shared-validation-rules) to the integrated revision.
5. Pause only the dependent integration step when blocked; continue independent authorized work. Report unresolved conflicts and failing checks explicitly.

## Safe cleanup

- Creating a worktree includes responsibility for its retirement; cleanup of task-created worktrees is part of the task's default scope. The coordinating manager owns reconciliation of all worktrees created for its workstream, including descendants'; the root verifies it across the task before closing. For direct work, the creating agent owns cleanup. Delegating removal does not transfer accountability unless the receiving owner explicitly accepts it.
- An inactive worktree is not, by itself, evidence of ownership or safe removal; do not remove pre-existing, shared, primary, pinned, or user-retained worktrees without applicable ownership and host authorization. Task completion alone does not justify leaving an unused worktree; pending review, required artifacts, active consumers, or a host restriction may justify retention. On cancellation or handoff, retire unneeded worktrees or explicitly transfer outstanding cleanup.
- The cleanup owner runs, in order, before declaring cleanup done:
  1. Compare `git worktree list --porcelain` with the record: each entry is listed (or verified gone), and unrecorded worktrees stay untouched.
  2. Per worktree, confirm no agent or process uses it; inspect `git -C "<path>" status --porcelain --untracked-files=all --ignored`; preserve required outputs.
  3. Prove integration: the branch head is an ancestor of the integration branch, or for squash/rebase merges the PR is merged and the owned paths' content matches (`git diff` empty or explained). Otherwise record a preserved ref or patch and keep the worktree `retained`.
  4. Retire: a managed worktree through its host tool; otherwise `git worktree remove "<verified-path>"` with no force and no recursive delete. Report a locked worktree as retained; unlock only a lock this task set whose holder has stopped. A dirty refusal returns to step 2.
  5. Delete only task-owned branches not checked out elsewhere or needed, with `git branch -d`; never `-D` for unrecognized squash history. Remote branch deletion follows [publication](git-publication.md#pull-requests-and-merge-rules).
  6. Run `git worktree prune` only for task-owned metadata whose directory is verified gone (check `--dry-run` first).
  7. Re-run the list and branch inventories against the record.
- Reconciliation report, one line per record entry: task ID, path, branch, `retired` (removal and integration/preserved-ref evidence) or `retained` (reason, cleanup condition, cleanup owner), plus validation results and unrecorded observations. Root's close requires every entry terminal (`retired` or `retained`).
