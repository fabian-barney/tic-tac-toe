---
name: spec-to-task
description: Generate implementation-ready task files from spec.md for the Tic Tac Toe workshop. Use when asked to create tasks from the Tic Tac Toe specification.
---

# Spec To Task

Create task files only. Do not create application source code, package files,
tests, scripts, or configuration files.

## Required Reads

Before writing tasks, read:

- `spec.md`
- `AGENTS.md`
- every file in `docs/adr/`

## Output

Create:

- `tasks/status.md`
- one Markdown file per task in `tasks/`

Use these status values only:

- `pending`
- `in-progress`
- `completed`
- `blocked`

## Task Set

Create these ordered tasks unless `spec.md` has changed in a way that makes one
task clearly obsolete:

1. `001-bootstrap-react-vite.md`
2. `002-configure-local-quality-gates.md`
3. `003-game-domain-model.md`
4. `004-move-validation-and-state-transitions.md`
5. `005-winner-and-draw-detection.md`
6. `006-react-board-and-status-ui.md`
7. `007-reset-and-accessibility.md`
8. `008-quality-hardening.md`

Classify tasks `001` and `002` as `bootstrap`. Classify tasks `003` through
`008` as `feature`.

## Status Tracker Format

Create `tasks/status.md` with this table shape:

```markdown
# Task Status

| Task | Type | Title | Dependencies | Status | Gate evidence | Notes |
|---|---|---|---|---|---|---|
| 001 | bootstrap | Bootstrap React/Vite/TypeScript | none | pending | none |  |
```

Include every generated task in the table. Use concise dependency ids such as
`001`, `001, 002`, or `none`.

## Task File Format

Each task file must contain:

```markdown
# Task title

## Summary

## Scope

## Out Of Scope

## Dependencies

## Relevant Spec Sections

## Expected Files Or Components

## Constraints And Assumptions

## Acceptance Criteria

## Validation Evidence Required

## AI Review Focus

## Stop Condition

## Implementation Evidence
Status: pending

Commands run:

Gate results:

AI review:

Notes:
```

## Task Content Rules

- Bootstrap tasks may create framework, dependency, config, scripts, smoke
  tests, and validation setup.
- Feature tasks must not recreate the framework setup.
- Feature tasks must require tests during the implementation loop.
- Feature tasks must require the CRAP gate through the configured validation
  command.
- Feature tasks must require a local AI review pass before completion.
- No task may assume git, branches, commits, pull requests, CI, Human Gates, or
  Merge.

## Stop Condition

Stop after task files and `tasks/status.md` exist. Report the generated task
list and confirm that no application code was created.
