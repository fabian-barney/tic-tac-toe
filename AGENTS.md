# Agent Instructions

This workshop starter uses local files and local validation only. Do not assume
git, branches, commits, pull requests, CI, Human Gates, or Merge.

Before creating tasks or implementing code:

- Read `spec.md`.
- Read all ADRs in `docs/adr/`.
- If `tasks/status.md` exists, read it before choosing work.

Implementation rules:

- Keep game-rule logic in framework-independent TypeScript modules.
- Keep React components thin and focused on rendering and user interaction.
- Use tests to prove behavior, including edge and exceptional cases.
- Run relevant tests during every implementation loop.
- Keep `tasks/status.md` current.
- Update the implementation evidence section in the active task file.

CRAP gate rules:

- Use the Vitest adapter `@barney-media/crap-typescript-vitest`.
- Keep the CRAP threshold at `6`.
- Keep CRAP output format as `text`.
- Do not lower the threshold.
- Do not disable the adapter.
- Do not exclude production source files just to pass the gate.
- If CRAP fails, improve code structure and tests until the gate passes.

Task status values are limited to:

- `pending`
- `in-progress`
- `completed`
- `blocked`
