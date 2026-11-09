# Validation

This guide owns common validation evidence. Discover applicable methods through the [leaf index](../workflows/AGENTS.leaf.md#leaf-index). Load [container usage](container-usage.md#compose-validation-sequence) only for container/Compose work; it owns identity, readiness and the Compose check sequence.

## Shared validation rules

- Run builds, tests and lints that the project's CI covers under [CI-first checks](#ci-first-checks).
- Wait for the project's documented readiness condition before dependent checks. If healthchecks do not represent required readiness, use the documented application probe or relevant logs.
- Discover required commands and expected outcomes from READMEs/configuration and the assignment brief. Use [coding standards](coding-standards.md#validation-and-completion) to decide code-test coverage.
- Check the actual artifact/revision. Capture command/procedure, exit status, tested revision, and decisive evidence/log locator. Direct work may report concisely; delegated work uses the selected [result schema](../templates/subagent-result.md). Non-code review must identify the artifact checked.
- Distinguish passed, failed, and unrun checks. Inaccessible inputs, unavailable checks, stale evidence, or insufficient coverage are unverified, not passed. Do not weaken a check to obtain success; route scope changes through root.
- Validate the integrated result; isolated passing branches cannot establish their combination passes. Rerun affected checks after relevant changes; earlier approval does not approve later revisions.
- Start with the smallest check set covering the changed behavior and required gates; broaden only for failures, new changes, unresolved concerns, or a mandatory check. Once acceptance passes, do not repeat checks for reassurance; never omit required CI/review gates to save tokens.
- Report material limitations and unresolved failures. Functional acceptance needs observed behavior; domain methods and coverage requirements remain in the applicable workflows.

## CI-first checks

Local builds and test suites (for example `cargo build`, `cargo test`, `cargo clippy`) can take long and saturate the user's disk and CPU, so CI is the default place to run them.

- When the project's CI (such as GitHub Actions on push or PR) runs a check, do not run that check locally. Commit, push under [publication](git-publication.md) authority, and use the hosted result for the pushed revision as the evidence; read failing job logs instead of reproducing the whole run locally.
- An agent without authority to push the revision leaves CI-covered checks unrun and reports them as pending CI with the commit SHA. Root obtains the CI result after integration, normally from its [session-end push](git-publication.md#root-session-end-push), and evaluates goals that depend on it from that result.
- Fall back to local runs only when CI is unavailable for the check: no CI configured, CI does not cover it, no remote or push path exists, hosted runs cannot start (outage, quota, billing, disabled Actions), or the user asks for a local run. Record the reason. Even then, run the narrowest command covering the change (one crate, package or test target, not the whole workspace), and do not run several heavy builds in parallel.
- Fast, low-load checks that do not build the project (formatters, single-file linters, `actionlint`) may still run locally before committing.
- Waiting on CI is not a pass: the check stays unverified until the hosted run for that revision completes.
