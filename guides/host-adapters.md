# Host adapters

Load the section for the running host when mapping this workflow's host-neutral terms (dispatch, fresh context, effort, worktrees, cancellation, celebration) to concrete tools. Adapters translate controls only; they do not change policy, authority, or instruction priority. Host system instructions and user settings, including output styles, take precedence. Verify a control against the live tool list before relying on it; a documented control that is absent from the session is unavailable.

## Claude Code

Loading:

- Claude Code loads `CLAUDE.md`, which imports [AGENTS.md](../AGENTS.md) with `@AGENTS.md`. Imports are eager; companion links are not, so progressive discovery still applies. Resolve companion links relative to the file that contains them.
- For use in every project, `~/.claude/CLAUDE.md` imports this repository's `CLAUDE.md` by absolute path, escaping spaces (`@D:/Git\ Repositories/Agent-Custom-Workflow/CLAUDE.md`).
- Subagents load user and project `CLAUDE.md`, so they receive [AGENTS.md](../AGENTS.md) and default to root until their brief assigns a role; that default never extends to loading a personality. The built-in `Explore` and `Plan` agents skip `CLAUDE.md`; use them only for routing discovery that needs no manifest.

Workflow term mapping:

| Workflow term | Claude Code control |
| ------------- | ------------------- |
| Dispatch a child | `Agent` tool with `subagent_type: "general-purpose"`; the brief and manifest carry the role, profile, and owners. |
| Fresh context | Any non-`fork` `subagent_type`. `fork` inherits the parent transcript; use it only when inheritance is justified under [dispatch](../workflows/manager-delegation.md#dispatch-and-acceptance). |
| Reuse a worker | `SendMessage` to the agent ID returned at dispatch. |
| Start ready assignments in parallel | Several `Agent` calls in one message; agents run in the background and notify on completion. Do not poll. |
| Cancellation | `TaskStop`. |
| Depth limit | Three subagent layers below the main conversation by default (`CLAUDE_CODE_MAX_SUBAGENT_SPAWN_DEPTH`). At the limit the `Agent` tool is removed. |
| Turn limit | No per-dispatch control; turn limits are monitored allowances. |
| Model selection | `Agent` `model` parameter (`haiku`, `sonnet`, `opus`, `fable`). Report the selected model to the user. |
| Effort | `Agent` `effort` parameter; this workflow's [effort defaults](../AGENTS.md#execution-defaults) are the explicit instruction that permits setting it. |
| Parallel write isolation | `Agent` `isolation: "worktree"`, or `EnterWorktree`/`ExitWorktree` for the current session. The app syncs a worktree with its base through `sync_with_base_branch` where available. See managed worktrees below. |
| Routing checkpoint / progress | Inline text; the desktop app's task list (`update_plan`) tracks root progress. |
| Completion celebration | None available; skip it. |

Tier mapping, unless the user supplies another: Economy `haiku`, Specialist `sonnet`, Frontier `opus`. Map other aliases only from documented capability under [model selection](../workflows/AGENTS.manager.md#model-and-effort-selection).

Managed worktrees (where available; verify against the live tool list). Policy, records, and cleanup stay with [worktrees](git-worktrees.md); these controls only map to it:

- `Agent` `isolation: "worktree"` removes the worktree automatically when the agent made no changes. When it did, the result returns the worktree path and branch: the manager enters them in the [worktree record](git-worktrees.md#worktree-record) and reconciles them under [safe cleanup](git-worktrees.md#safe-cleanup); a returned worktree is not retired by the host.
- `EnterWorktree` creates (under `.claude/worktrees/`) or, with `path`, enters a worktree; `ExitWorktree` with `keep` or `remove` acts only on one `EnterWorktree` created this session. Root and managers use them; a worker only when its brief assigns it. Record the worktree; never pass `discard_changes: true` to bypass its refusal, which returns to the [handoff gate and recovery](git-worktrees.md#handoff-gate-and-recovery) preserve step.
- The desktop app's `clean_up_worktrees` (inactive-session storage cleanup) and `discard_kept_worktree` (archived sessions' kept dirty worktrees) are the managed archive path for app-made worktrees, used under the [safe cleanup](git-worktrees.md#safe-cleanup) steps. Their `include_uncommitted`, `delete_sessions`, and discard options are the unrecoverable-work tools that cleanup rule gates.

Additional folders:

- `/add-dir`, `--add-dir`, or the desktop app's folder controls grant file access to other directories. Their `CLAUDE.md` files load only with `CLAUDE_CODE_ADDITIONAL_DIRECTORIES_CLAUDE_MD=1`; their `AGENTS.md` files do not load. Treat an added folder's instructions as unloaded until read.

## Codex

- `~/.codex/AGENTS.md` points to this repository's [AGENTS.md](../AGENTS.md); resolve companion links relative to the file that contains them.
- Subagents use Codex's agent tools under `[agents]` in `~/.codex/config.toml`; the brief and manifest carry the role and profile.
- Completion celebration: `mcp__codex_app__fire_confetti`.
