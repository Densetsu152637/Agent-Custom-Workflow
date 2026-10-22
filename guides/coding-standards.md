# Coding standards

## Apply these rules

- Follow project/framework conventions and existing helpers. Make the smallest cohesive change meeting requirements; no speculative abstractions or unrelated rewrites.
- Refactors must adapt the affected system wherever the new design requires it, including consumers, interfaces, integrations, tests, and documentation. Remove superseded pieces; do not add compatibility shims or parallel paths solely to preserve the old design. Keep this bounded to the affected system and follow explicit user instructions about preservation, compatibility, or scope.
- Validate untrusted input at boundaries; preserve failures, cancellation, and resource cleanup. Never report failure as success.
- Load [coding conventions](coding-conventions.md) when introducing a language/framework without established conventions, designing/reviewing API or state contracts, or changing error/cancellation/resource handling; routine edits following existing patterns do not need it. Do not change working code's paradigm merely to follow defaults.

## Documentation alignment

- Reflect every repository implementation/refactor in relevant project documents in the same task: identify affected docs during scoping, assign ownership with implementation, and update behavior, interfaces, configuration, architecture, and usage; add focused documentation where missing.
- Compare affected documents with the final implementation during acceptance and report unresolved gaps. For research implementations with a maintained research paper, also load [scoped paper-update rules](../workflows/AGENTS.research-paper.md#update-the-paper-after-a-refactor); ordinary software work needs no paper artifacts.

## Validation and completion

- Add/update behavior-focused tests for material behavioral changes and regressions, covering relevant edge/failure paths. No tests that mirror implementation, and no runtime tests for prose-only or reversible low-impact edits without behavioral risk.
- Run required project format/lint, type/build, and focused checks under [validation](validation.md#shared-validation-rules). Broaden or repeat only for relevant changes, failures, unresolved concerns, or mandatory gates.
- Measure before claiming performance gains.
