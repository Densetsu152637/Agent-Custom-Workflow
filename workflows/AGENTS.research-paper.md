# Research paper documentation

Load for research undertaken to write or maintain a research paper/manuscript, or refactoring a research implementation with a maintained paper. Ordinary lookups, software comparisons, and papers used only as sources do not trigger these persistent artifacts.

## Retain and reuse research results

Apply the persistent-record requirements in this section only under the [paper documentation scope](AGENTS.research.md#scope-and-documentation).

- Whenever a paper-related research goal or prompt produces results, record them for future agents, including inconclusive or negative outcomes. Use the assigned project's existing research documents or evidence ledger; give each record a stable ID and link it from a discoverable index at a persistent path. Preserve the goal and exact prompt (redacting secrets), scope and assumptions, methods/settings, relevant dates and source or implementation revisions, results, supporting evidence, and limitations.
- Before new research, consult relevant prior records and compare findings using compatible criteria. Record changed scope, methods, or context and explain conflicting findings in a new entry; preserve prior records rather than overwriting their history.
- Add every source used in paper-related research to the repository's existing BibTeX bibliography. If none exists, create `paper/references.bibtex` under the repository root, creating `paper/` as needed. Reuse existing entries and stable citation keys; verify metadata against the source itself and leave unavailable fields out rather than inventing them. Reference citation keys in retained research records where appropriate.

## Update the paper after a refactor

- When refactoring a research implementation with a maintained research paper, update that paper to reflect the final implementation under [documentation alignment](../guides/coding-standards.md#documentation-alignment). Map the code changes to the affected paper content before editing; this rule does not require creating a paper for an ordinary software task.
- Update only the parts affected by the refactor, including directly dependent claims, equations, algorithm descriptions, implementation details, figures, tables, or cross-references where needed for consistency. Preserve unaffected content and structure; do not rewrite the whole paper or make unrelated editorial changes.
- Check each changed passage against the final code and available validation evidence, and report the affected paper sections and corresponding implementation changes. If the refactor invalidates reported results, identify them as needing revalidation and update measurements only from actual rerun evidence; do not invent results. Record inaccessible paper sources or unresolved discrepancies as documentation gaps.
