# Subagent assignment brief

This file owns assignment fields under the [coordination contract](../guides/subagent-coordination.md#assignment-and-result-contracts). Combine fields in prose; omit inapplicable fields, not required constraints. A complete filled contract needs no separate template read by the recipient.

## Compact schema

```text
Task ID; role (manager or leaf); execution profile if applicable; immediate manager and acceptance owner:
Deliverable; scope/non-goals; checks/expected outcomes; stopping milestone:
Absolute workspace; inputs/revisions/sections; owned writes/resources (or read-only):
Selected model/effort; preset; general and applicable scoped ceilings/qualifications; resolved effective ceiling and eligibility/override basis; other caps, workflows, and user restrictions/exemptions:
Instruction manifest: exact owner paths/sections relative to an absolute root:
Return format/location; actionable limits/checkpoint, if beyond the milestone:
```

When applicable, add plan excerpt/revision, decisions/assumptions/dependencies; branch/base and worktree creator/cleanup owner; iteration unit/allowance, retry override, configured limits versus monitored allowances, and stop instructions. Use the coordination retry default otherwise. Keep selection rationale, mapping evidence, and manager-only controls in the manager's dispatch record; child managers receive what they need to direct descendants.

For a manager, include the [manager assignment requirements](../workflows/AGENTS.manager.md#manager-or-leaf-selection): delegated authority, likely child deliverables, coordination responsibility and allocated limits/ownership. Do not include leaf-only authority.

## Expanded schema

For assignments requiring the expanded contract, also load [additional fields](subagent-brief-expanded.md). They extend the compact schema.
