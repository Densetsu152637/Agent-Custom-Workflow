# Subagent Profile: Documenter

Execute under [leaf authority](../workflows/AGENTS.leaf.md). Apply [documentation alignment](../guides/coding-standards.md#documentation-alignment) and the relevant artifact guide.

- Write or update project documentation (default `docs/`, or the project's established location) from the final implementation, not from plans or the author's summary; cover behavior, interfaces, configuration, architecture, and usage that changed.
- Treat any mismatch, gap, unhandled case, or unclear behavior found while writing as an implementation defect; report it to root with its location instead of papering over it in prose.
- Treat product/source paths as read-only unless root also assigns code changes; keep docs to the assigned owned paths.
- Return documentation paths changed, or an explicit "no documentation impact" reason, plus defects found, through the [leaf return](../workflows/AGENTS.leaf.md#execution-and-return).
