# GitHub Actions

This guide owns workflow authoring and local iteration. [Git usage](git-usage.md#pull-requests-and-merge-rules) owns merge gates; [validation](validation.md#shared-validation-rules) owns check evidence; [environment configuration](environment-configuration.md#secret-handling) owns secret handling.

## Author workflow files

- Put workflows in `.github/workflows/*.yml` or `*.yaml`. Inspect existing workflows, project scripts, required checks, and runner requirements first. Reuse the same formatter, linter, build, and test commands locally and in CI; keep application logic in project scripts rather than duplicating it in YAML.
- Choose explicit events and jobs. Use `pull_request` for PR checks and restrict `push` to branches needing post-merge validation to avoid duplicate runs on feature branches. Add `merge_group` checks when the repository's merge queue requires them. Keep required job names stable.
- Specify the runtime/toolchain and install dependencies from the committed lockfile. Select action versions compatible with the runner; follow repository pinning rules and prefer reviewed full commit SHAs for immutable references.
- Start with minimal `permissions`, typically `contents: read` for checkout and tests. Grant additional access only to jobs that need it. Untrusted PR code should not execute with privileged tokens or deployment secrets. See [GitHub token permissions](https://docs.github.com/en/actions/tutorials/authenticate-with-github_token).

Adapt this workflow skeleton to the consuming project. `scripts/check.sh` represents its existing check script; replace it and add its documented toolchain/dependency setup before running. The action tag is illustrative; resolve an approved version or SHA before adopting it.

```yaml
name: Checks
on:
  pull_request:
  push:
    branches: [main]
permissions:
  contents: read
concurrency:
  group: ${{ github.workflow }}-${{ github.event_name }}-${{ github.event.pull_request.number || github.ref }}
  cancel-in-progress: ${{ github.event_name == 'pull_request' }}
jobs:
  checks:
    runs-on: ubuntu-latest
    timeout-minutes: 10
    steps:
      - uses: actions/checkout@v6
        with:
          persist-credentials: false
      # Add the project's runtime and locked dependency installation here.
      - name: Project checks
        shell: bash
        run: bash scripts/check.sh
```

Syntax and events: [GitHub workflow reference](https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax). Checkout requirements: [actions/checkout](https://github.com/actions/checkout).

## Fast local checks

Run the project's check scripts directly first. Use [actionlint](https://github.com/rhysd/actionlint) to catch workflow syntax, expression, and related static errors; plain YAML validation alone does not understand Actions semantics.

```text
actionlint
```

Use [pre-commit](https://pre-commit.com/) for fast formatter, lint, whitespace, and workflow checks before a commit. Add hooks to the project's `.pre-commit-config.yaml`, following its existing pinned versions; actionlint documents a [pre-commit integration](https://github.com/rhysd/actionlint/blob/main/docs/usage.md#pre-commit). After pre-commit and the configured hook dependencies are installed:

```text
pre-commit install
pre-commit run --all-files
```

Keep expensive integration tests and full container runs outside the default fast hook. Hooks give early feedback; run the same relevant checks in CI as well.

## Run workflows locally with act

For Linux container jobs, install and start Docker Engine or Docker Desktop (using Linux containers on Windows). Install [nektos/act](https://nektosact.com/installation/index.html) using one package manager already available on the host:

```text
# Homebrew (macOS/Linux)
brew install act
# Chocolatey (Windows)
choco install act-cli
# Scoop (Windows)
scoop install act
```

From the consuming repository root, these commands list PR jobs, run PR workflows, or narrow execution to one file/job:

```text
act pull_request -l
act pull_request
act pull_request -W .github/workflows/checks.yml -j checks
act pull_request -W .github/workflows/checks.yml -j checks -e event.json
```

Use a sanitized `event.json` fixture containing the PR fields your expressions read, for example:

```json
{"pull_request":{"number":42,"head":{"ref":"feature/example"},"base":{"ref":"main"}}}
```

Select a runner image with the required tools; act's default images are not identical to hosted runners. Linux Docker images do not reproduce native Windows/macOS jobs. act also supports opt-in [host execution](https://nektosact.com/usage/runners.html), which runs directly on the machine and still does not recreate GitHub's hosted image.

Provide only needed local secrets using act's secure prompt, such as `act pull_request -s MY_SECRET`; use ignored secret files only under the linked secret-handling guide. GitHub's automatic token and environment secrets are not supplied locally. See [act usage](https://nektosact.com/usage/index.html).

Treat act as a rehearsal: event context, token permissions, caches, and hosted services can differ. It currently ignores concurrency, job permissions, and job timeouts, among other [unsupported features](https://nektosact.com/not_supported.html). A local success does not verify those controls.

## Control hosted runtime

- Use positive path filters for optional expensive workflows, including source, tests, dependency manifests/lockfiles, build configuration, shared scripts, and `.github/workflows/**`. Example fragment, adapted to actual project paths:

  ```yaml
  on:
    pull_request:
      branches: [main]
      paths:
        - 'src/**'
        - 'tests/**'
        - 'scripts/**'
        - 'package.json'
        - 'package-lock.json'
        - '.github/workflows/**'
  ```

  Branch and path filters must both match; PR branch filters target the base branch. A workflow skipped by path/branch filtering can leave required checks Pending and block merging. Keep required workflows triggered for every relevant PR; filter expensive jobs inside them and provide an always-run required gate that reports failures and handles intentional skips. Do not apply this optional fragment blindly to the required-check skeleton above. See [filter semantics and required-check warning](https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax#onpushpull_requestpull_request_targetpathspaths-ignore).
- Set strict, realistic job `timeout-minutes` values and tighter step timeouts for potentially hanging commands. Tune against observed durations.
- Cache package-manager downloads with a supported setup action or `actions/cache`. Include OS, relevant toolchain version, and lockfile hash in custom keys; still perform the locked dependency install after restoring. Avoid caching secrets. Measure actual runtime and cache overhead rather than assuming a fixed saving. See [GitHub dependency caching](https://docs.github.com/en/actions/reference/workflows-and-actions/dependency-caching).
- Cancel obsolete PR runs using a group scoped to workflow, event, and PR/ref, as in the skeleton. Ensure independent PRs/workflows cannot cancel one another. Deployment cancellation needs a separate decision. See [GitHub concurrency](https://docs.github.com/en/actions/how-tos/write-workflows/choose-when-workflows-run/control-workflow-concurrency).

## Verify before handoff

Run static checks and the relevant project scripts, then use act for supported jobs. Exercise event-dependent conditions with representative payloads, including relevant PR/base branches and missing optional fields. Verify path-filter cases (source, docs-only, lockfile, and workflow edits), fork permissions, cache misses/hits, timeouts, and cancellation on GitHub where local execution cannot establish behavior. Report unrun hosted checks explicitly under the linked validation guide.
