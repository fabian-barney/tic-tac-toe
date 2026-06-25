---
name: implement-task
description: Implement remaining Tic Tac Toe feature tasks sequentially with tests, CRAP gate, local AI review, fixes, and task status updates.
---

# Implement Task

Implement remaining feature tasks sequentially. Do not skip ahead. Do not
implement bootstrap tasks unless a missing bootstrap step blocks the current
feature task.

## Required Reads

Before editing, read:

- `spec.md`
- `AGENTS.md`
- every file in `docs/adr/`
- `tasks/status.md`
- every pending or in-progress feature task file

## Task Selection

Use `tasks/status.md` as the source of truth.

- Select the first feature task whose dependencies are `completed`.
- Mark it `in-progress` before editing.
- Finish or block that task before starting another task.
- Update both `tasks/status.md` and the task file's implementation evidence.

## Per-Task Loop

For each selected feature task:

1. Read the task and relevant `spec.md` sections.
2. State a short implementation plan for that task.
3. Implement the smallest coherent change that completes the task.
4. Add or update focused unit tests and component/interaction tests.
5. Run relevant tests during the implementation loop.
6. Run the configured validation gate.
7. Run a local AI review pass for the current task.
8. Fix every valid AI review finding.
9. Rerun affected tests and validation after fixes.
10. Record evidence before moving to the next task.

Use the existing project scripts. Do not add direct CRAP package commands to the
workflow unless the configured scripts are broken and you are diagnosing the
blocker.

Required validation command:

```text
npm run validate
```

Focused tests may be run before full validation, but full validation is required
before marking a feature task `completed`.

## Local AI Review

Review local files against `spec.md`, `AGENTS.md`, ADRs, and the active task.
Review the actual files, not a git diff.

If a separate reviewer agent or sub-agent is available, use it. If not, perform
a fresh pass with a clearly separated reviewer role.

Review focus:

- correctness
- missing edge cases
- insufficient tests
- CRAP or complexity risk
- accessibility
- divergence from `spec.md`
- task tracking completeness

Classify each finding as valid or invalid. Fix valid findings. Record invalid
findings with a short rationale.

## Completion Rule

A feature task is complete only when:

- relevant tests pass
- `npm run validate` passes
- CRAP gate evidence is available through the validation output
- valid AI review findings are fixed
- affected tests and validation pass again after fixes
- task evidence is recorded
- `tasks/status.md` is updated

If a gate cannot produce evidence, mark the task `blocked` or record the missing
evidence explicitly. Do not mark missing evidence as passed.

## Stop Condition

Stop when all feature tasks are `completed`, or when the next task is blocked by
a concrete blocker.

Report each feature task with files changed, tests run, validation result, CRAP
result, AI review findings, fixes made, remaining limitations, and final app run
command.
