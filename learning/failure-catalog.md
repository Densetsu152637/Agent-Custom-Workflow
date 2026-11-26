# Failure catalog

Selection and updates are governed by [maintenance guidance](README.md); entry structure is defined in the [entry template](../templates/failure-entry.md).

## Index

| ID | Pattern / applicability | Status | Entry locator | Last verified |
| -- | ----------------------- | ------ | ------------- | ------------- |
| FAIL-001 | Local checks differ from CI's (toolchain floor, linters, flags); pushes fail CI one gate at a time | verified | [FAIL-001](#fail-001-local-checks-do-not-match-ci) | 2026-11-26 |
| FAIL-002 | Resource-limited code (interpreters, parsers, validators, servers) undercharges or leaks work; reviews take many rounds | candidate | [FAIL-002](#fail-002-resource-accounting-gaps-found-one-class-per-review-round) | 2026-11-26 |
| FAIL-003 | Secrecy, taint or authority boundaries leak through side channels and replayed decisions | candidate | [FAIL-003](#fail-003-label-and-authority-leaks-through-indirect-paths) | 2026-11-26 |
| FAIL-004 | Branches stacked on an unmerged branch conflict everywhere after the base is squash-merged | verified | [FAIL-004](#fail-004-stacked-branches-after-a-squash-merge) | 2026-11-26 |

## Entries

### FAIL-001: Local checks do not match CI

```text
ID: FAIL-001; short title: local checks do not match CI; status: verified
Applies to: any repository whose CI runs gates the local check script does not: a minimum or
  pinned toolchain (MSRV, oldest supported runtime or compiler, LTS SDK), linters (markdown,
  YAML, shell), stricter flags (--locked, -D warnings, --all-targets), other operating systems.
  Symptom: a push passes locally and fails CI on one gate; the fix passes locally and fails the
  next gate.
Does not apply to / invalidation conditions: CI is not a merge gate; the local script already
  runs every CI job's exact command; the failing gate is an outage or flaky infrastructure.
Observed symptom and impact: in one multi-stage project the minimum-toolchain job failed three
  times (language features and type inference newer than the floor) and the docs linter twice
  (blank lines, spaces in code spans), each costing a full CI cycle; CI logs were unavailable
  until the slowest job finished, adding wait time.
Evidence: Ratio repository (github.com/Densetsu152637/Ratio) PRs #6, #8 and #10 CI runs;
  observation date 2026-11-26.
Cause: confirmed. The local check script covered formatting, lint and tests on the current
  toolchain only; the floor toolchain and the docs linter ran only in CI, and workers relied on
  reading code for compatibility because the floor toolchain was not installed.
Failed approaches and why they did not help: asking workers to stay compatible by inspection
  (inference and library differences are not visible by reading); fixing only the reported
  error and pushing again (the next gate then failed).
Smallest successful correction: at intake, read the CI workflow files and list every job's exact
  command; install any toolchain they need; give every implementer that list as its pre-push
  check, run with the same flags, plus the linters CI runs. Where two toolchains disagree (the
  floor rejects one form, the newer linter rejects the other), use an explicit form both accept,
  such as a type annotation. Reproduce a CI-only failure locally rather than waiting for logs.
Verification procedure and actual result/revision: after the floor toolchain was installed and
  its exact CI command added to every brief, the next four branches (Ratio stages 8, 9, C and
  11a) passed the minimum-toolchain job on their first push.
Recurrence/evidence links; last verified date; maintainer/owner: Ratio PRs #6, #8, #10 and #12;
  2026-11-26; workflow maintainer.
Supersedes / superseded by: none.
```

### FAIL-002: Resource-accounting gaps found one class per review round

```text
ID: FAIL-002; short title: resource-accounting gaps found one class per review round;
  status: candidate
Applies to: code that must bound work or memory for untrusted input: interpreters and VMs with
  step or heap budgets, parsers, schema validators, regex and template engines, request handlers
  with quotas, anything that must charge before work. Symptom: security reviews find a new
  denial-of-service or undercharge each round, each fix closing one site but not its class.
Does not apply to / invalidation conditions: code with no adversarial input or no resource limit;
  limits enforced entirely outside the code (for example OS cgroups) with no in-code accounting.
Observed symptom and impact: four data and interpreter stages needed three to six security review
  rounds each; one validator went exponential, then quadratic, then length-dependent, then
  leaked work through discarded error messages, across six rounds.
Evidence: Ratio stages 6, 7, 8, 9 and 11a reviews (PRs #8, #9, #12 and branch
  feat/wt-s11a-host); observation date 2026-11-26.
Cause: confirmed by the findings. Implementers charged per element or per visit while the real
  cost depended on hidden factors, and briefs named the rule but not its recurring failure
  classes:
  1. per-unit charges blind to string, key or element length (hash, compare, escape, copy);
  2. work inside a loop or a repeated visit that the budget never sees;
  3. failure, refusal or early-exit paths that skip the charge or the debit;
  4. work done for output that is then discarded (messages built in silent or speculative
     branches, rendering past a size cap);
  5. buffers, caches, queues and copies allocated before they are charged or bounded;
  6. recursion over input depth on the native stack (including destructors and debug builds);
  7. long loops with no cancellation or yield point;
  8. bounds that trust the component being bounded (its clock, its timer, its own report).
Failed approaches and why they did not help: fixing each reported site; a debug guard and
  property test comparing work with charge whose counters did not see uncounted work (string
  operations, formatting) and whose generator never produced the adversarial shape.
Smallest proposed correction: put the eight classes in every brief for resource-limited code as
  an acceptance checklist; route string compare, hash and escape through counted helpers so
  guards see real cost; generate property-test inputs that are long, prefix-sharing, wide, deep
  and share references; ask the first review round to sweep all eight classes.
Verification procedure: unverified. On the next resource-limited stage, brief the checklist up
  front and compare review rounds and findings per class with this entry.
Recurrence/evidence links; last verified date; maintainer/owner: as Evidence; 2026-11-26;
  workflow maintainer.
Supersedes / superseded by: none.
```

### FAIL-003: Label and authority leaks through indirect paths

```text
ID: FAIL-003; short title: label and authority leaks through indirect paths; status: candidate
Applies to: systems that track sensitivity or authority on values or requests: taint or secrecy
  labels, information-flow control, capability or permission scopes, sandbox boundaries, record
  and replay of user decisions. Symptom: reviews keep finding a value that loses its label, or a
  decision granted without being asked, through a path the main rule missed.
Does not apply to / invalidation conditions: systems with no labels or scopes; flows the
  specification explicitly excludes (for example documented implicit flows).
Observed symptom and impact: across six stages, reviews found sensitive values unlabelled through
  error tags, the field that selects a variant, misses returning a default, interior parts of
  composite keys and branch decisions; a replayed approval removed a label from a new live
  secret, and a recorded user answer could be forged from a crafted tape.
Evidence: Ratio stages 6, 8, 9, 10, 11a and C reviews; observation date 2026-11-26.
Cause: confirmed by the findings. Rules were applied to the obvious data path only, and several
  guards were keyed to lists of names, so new operations of the same kind passed. The recurring
  classes were:
  1. results whose labels miss what decided them (selectors, tags, compared keys, misses, the
     chosen branch, failure messages);
  2. labels kept on a container but lost from its parts, or kept only one level deep;
  3. side channels around the guard (settings, defaults, configuration, error payloads, approval
     or question text, logs);
  4. decisions answered from a recording, cache or tape instead of asked live (approvals, user
     answers, declassification);
  5. unkeyed digests or hashes over sensitive data written anywhere persistent;
  6. guards driven by name lists instead of declared traits, so unknown operations pass;
  7. trust in fields the other side asserts (a frame's kind, a caller's claimed scope).
Failed approaches and why they did not help: adding each leaked operation to the guard's list;
  tests that exercised only the operations already named.
Smallest proposed correction: brief the seven classes with every security-sensitive task; derive
  guards from declared attributes and fail closed on anything unknown; never answer a user
  decision from a recording; key every digest over sensitive data; have each side verify against
  its own record, not the other side's assertion.
Verification procedure: unverified. On the next security-boundary stage, brief the list and count
  leak findings per class against this entry.
Recurrence/evidence links; last verified date; maintainer/owner: as Evidence; 2026-11-26;
  workflow maintainer.
Supersedes / superseded by: none.
```

### FAIL-004: Stacked branches after a squash merge

```text
ID: FAIL-004; short title: stacked branches after a squash merge; status: verified
Applies to: repositories that squash-merge pull requests, with parallel work branched from an
  unmerged branch to start dependent work early. Symptom: after the base merges, merging the
  default branch into the stacked branch reports add/add or content conflicts on every file the
  base touched, although the content is the same.
Does not apply to / invalidation conditions: merge commits or rebase merges that keep the base's
  history; branches cut from the default branch.
Observed symptom and impact: every follow-on branch in a staged project hit many conflicts
  (19 files in one case) after its base was squash-merged, costing time and risking a wrong
  resolution that drops a later fix.
Evidence: Ratio stages 5, 6, 8, 11a and C merges; observation date 2026-11-26.
Cause: confirmed. Squash merging gives the default branch new commits with no ancestry link to
  the base branch's commits, so git sees both sides adding the same files.
Failed approaches and why they did not help: resolving file by file by reading both sides (slow
  and error-prone when the base received review fixes after the branch point).
Smallest successful correction: before merging, check that the default branch's tree equals the
  base branch's final head (git diff --quiet <default> <base-head>). If it does, resolve every
  conflict to the stacked branch's side, then apply git diff <base-at-branch-point> <base-head>
  for the base's later fixes, and verify that git diff --stat <default> <result> equals the
  stacked branch's own changes. Never rebase or force-push shared branches to avoid it. Prefer
  branching from the default branch when the dependency allows.
Verification procedure and actual result/revision: applied to Ratio stage 11a's merge of stage 10
  (19 conflicts); git diff --stat origin/main 7634a2a matched git diff --stat b390cea 6e87773
  exactly (41 files), and all checks passed.
Recurrence/evidence links; last verified date; maintainer/owner: as Evidence; 2026-11-26;
  workflow maintainer.
Supersedes / superseded by: none.
```
