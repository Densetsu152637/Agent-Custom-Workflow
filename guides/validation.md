# Validation

This guide owns common validation evidence. Discover applicable methods through the [workflow index](../AGENTS.md#workflows). Load [container usage](container-usage.md#compose-validation-sequence) only for container/Compose work; it owns identity, readiness and the Compose check sequence.

## Shared validation rules

- Wait for the project’s documented readiness condition before dependent checks. If healthchecks do not represent required readiness, use the documented application probe or relevant logs; preserve diagnostic evidence under these shared rules.
- Discover required commands/procedures and expected outcomes from relevant READMEs/configuration and the assignment brief. Run checks appropriate to the changed behavior and required review; use [coding standards](coding-standards.md#validation-and-completion) to decide code-test coverage.
- Check the actual artifact/revision. Capture command/procedure, exit status where applicable, tested revision, and decisive evidence/log locator. A concise direct-work report suffices; delegated work uses the selected [result schema](../templates/subagent-result.md). Non-code review must also identify the artifact checked.
- Distinguish passed, failed, and unrun checks. Inaccessible inputs, unavailable checks, stale evidence, or insufficient coverage are unverified, not passed. Retain acceptance criteria; route changes to scope through the manager rather than weakening a check to obtain success.
- Validate the integrated result; isolated passing branches/workstreams cannot establish their combination passes. Rerun affected checks after relevant input/output changes, and do not repeat unaffected passing checks without a reason. Earlier approval does not approve later revisions.
- Start with the smallest meaningful check set covering the changed behavior and required gates. Broaden only for failures, new changes, unresolved concerns, or a mandatory check. Once acceptance passes, continue toward completion rather than repeating checks for reassurance; never omit required CI/review gates to save tokens.
- Report material limitations and unresolved failures; do not claim completion from evidence that does not establish the required behavior. Functional acceptance needs observed behavior; domain methods and their coverage requirements remain in the applicable workflows.
