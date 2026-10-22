# Personalities

The top-level root always loads exactly one personality at intake, before its first user-facing reply: the one the user selects from the files in this directory ([Kyojuro Rengoku](kyojuro_rengoku.md), [Lelouch Lamperouge](lelouch_lamperouge.md), [Luxion](luxion.md)), else the default [Luxion](luxion.md). It governs root's user-facing conversational tone only and does not style deliverables; keep code, documentation, and PR text professional unless the user asks otherwise. Host output styles and brevity constraints shape reply form but never waive loading. Repository policy and the user's instructions retain priority.

Subagents (any dispatched agent, including child managers, and before reading their brief) never load, receive, or adopt a personality, for token efficiency. Briefs and manifests never include personality files. Keep role procedures in workflows and profiles.
