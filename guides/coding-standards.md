# Coding standards

## Apply these rules

- Follow project/framework conventions and existing helpers. Make the smallest cohesive change meeting requirements; avoid speculative abstractions or unrelated rewrites.
- Keep contracts, state, effects, ownership, and error paths clear. Validate untrusted input at boundaries; preserve failures, cancellation, and resource cleanup. Never expose secrets or report failure as success.
- Use configured formatters/linters; keep changes focused. Comments explain constraints and non-obvious behavior, and public contracts document relevant units/invariants.
- Load relevant [coding conventions](coding-conventions.md) when introducing a language/framework without established conventions, designing/reviewing API or state contracts, or changing error/cancellation/resource handling. Routine edits following existing patterns do not require that reference. Do not change working code's paradigm merely to follow defaults.

## Documentation alignment

- Reflect every repository implementation/refactor in relevant project documents in the same task. Identify affected docs during scoping; assign ownership with implementation. Update behavior, interfaces, configuration, architecture, and usage to match the final result; add focused documentation where missing.
- Compare affected documents with the final implementation during acceptance and report unresolved gaps. For research implementations, also load [scoped paper-update rules](../workflows/AGENTS.research.md#update-the-paper-after-a-refactor).

## Validation and completion

- Add/update behavior-focused tests for material behavioral changes and regressions. Cover relevant edge/failure paths; avoid tests that mirror implementation or runtime tests for prose-only changes and reversible low-impact edits without a behavioral risk.
- Run required project format/lint, type/build, and focused checks under [validation](validation.md#shared-validation-rules). Broaden or repeat only for relevant changes, failures, unresolved concerns, or mandatory gates.
- Review the diff for unintended behavior, unrelated edits, secrets, stale docs, and resource/error handling. Measure before claiming performance gains.
