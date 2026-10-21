# Run GitHub Actions locally

Load when considering or executing act rehearsal for supported jobs. Workflow authoring and hosted gates remain in [GitHub Actions](github-actions.md); local success does not establish hosted behavior. Tool-managed act runner containers alone do not require the [application container/Compose guide](container-usage.md); load it when managing application container or Compose services relevant to the rehearsal.

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

Provide only needed local secrets using act's secure prompt, such as `act pull_request -s MY_SECRET`; use ignored secret files only under [secret handling](environment-configuration.md#secret-handling). GitHub's automatic token and environment secrets are not supplied locally. See [act usage](https://nektosact.com/usage/index.html).

Treat act as a rehearsal: event context, token permissions, caches, and hosted services can differ. It currently ignores concurrency, job permissions, and job timeouts, among other [unsupported features](https://nektosact.com/not_supported.html). A local success does not verify those controls.
