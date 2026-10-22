# Host adapters

Load the running host's section to map host-neutral terms (dispatch, fresh context, effort, worktrees, cancellation, celebration) to tools. Adapters change no policy, authority, or priority; host system instructions and user settings take precedence. A control absent from the live tool list is unavailable.

## Claude Code

Loading:

- `CLAUDE.md` imports [AGENTS.md](../AGENTS.md) with `@AGENTS.md`. Imports are eager; companion links are not. Resolve links relative to the containing file.
- For use in every project, `~/.claude/CLAUDE.md` imports this repository's `CLAUDE.md` by absolute path, escaping spaces (`@D:/Git\ Repositories/Agent-Custom-Workflow/CLAUDE.md`).
- Subagents load `CLAUDE.md`, so they receive [AGENTS.md](../AGENTS.md) and default to root until their brief assigns a role; that never extends to loading a personality. Built-in `Explore` and `Plan` agents skip `CLAUDE.md`; use them only for routing discovery that needs no manifest.

Workflow term mapping:

| Workflow term | Claude Code control |
| ------------- | ------------------- |
| Dispatch a child | `Agent` with `subagent_type: "general-purpose"`; the brief and manifest carry role, profile, and owners. |
| Fresh context | Any non-`fork` `subagent_type`. `fork` inherits the parent transcript; use it only when inheritance is justified under [dispatch](../workflows/manager-delegation.md#dispatch-and-acceptance). |
| Reuse a worker | `SendMessage` to the agent ID returned at dispatch. |
| Start ready assignments in parallel | Several `Agent` calls in one message; they notify on completion. Do not poll. |
| Cancellation | `TaskStop`. |
| Depth limit | Three subagent layers below the main conversation by default (`CLAUDE_CODE_MAX_SUBAGENT_SPAWN_DEPTH`). At the limit the `Agent` tool is removed. |
| Turn limit | No per-dispatch control; turn limits are monitored allowances. |
| Model selection | `Agent` `model` parameter (`haiku`, `sonnet`, `opus`, `fable`). Report the selected model to the user. |
| Effort | `Agent` `effort` parameter; this workflow's [effort defaults](../AGENTS.md#execution-defaults) are the explicit instruction that permits setting it. |
| Parallel write isolation | `Agent` `isolation: "worktree"`, or `EnterWorktree`/`ExitWorktree` for the current session. The app syncs a worktree with its base through `sync_with_base_branch` where available. See managed worktrees below. |
| Routing checkpoint / progress | Inline text; the desktop app's task list (`update_plan`) tracks root progress. |
| Completion celebration | None available; skip it. |

Tier mapping, unless the user supplies another: Economy `haiku`, Specialist `sonnet`, Frontier `opus`. Map other aliases only from documented capability under [model selection](../workflows/AGENTS.manager.md#model-and-effort-selection).

Managed worktrees (where available; verify against the live tool list). Policy, records, and cleanup stay with [worktrees](git-worktrees.md):

- `Agent` `isolation: "worktree"` removes the worktree when the agent made no changes; otherwise the result returns its path and branch, which the manager enters in the [worktree record](git-worktrees.md#worktree-record) and reconciles under [safe cleanup](git-worktrees.md#safe-cleanup).
- `EnterWorktree` creates (under `.claude/worktrees/`) or, with `path`, enters a worktree; `ExitWorktree` acts only on one `EnterWorktree` created this session. Root and managers use them; a worker only when assigned. Record the worktree; never pass `discard_changes: true` to bypass a refusal, which returns to the [handoff gate and recovery](git-worktrees.md#handoff-gate-and-recovery) preserve step.
- The desktop app's `clean_up_worktrees` and `discard_kept_worktree` are the archive path for app-made worktrees, used under [safe cleanup](git-worktrees.md#safe-cleanup); their `include_uncommitted`, `delete_sessions`, and discard options are the unrecoverable-work tools that rule gates.

Additional folders:

- `/add-dir`, `--add-dir`, or the app's folder controls grant access to other directories. Their `CLAUDE.md` loads only with `CLAUDE_CODE_ADDITIONAL_DIRECTORIES_CLAUDE_MD=1`; their `AGENTS.md` does not load. Treat their instructions as unloaded until read.

## Codex

- `~/.codex/AGENTS.md` points to this repository's [AGENTS.md](../AGENTS.md).
- Subagents use Codex's agent tools under `[agents]` in `~/.codex/config.toml`; the brief and manifest carry the role and profile.
- Completion celebration: `mcp__codex_app__fire_confetti`.
