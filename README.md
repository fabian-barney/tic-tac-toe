# Tic Tac Toe Agentic Development Lab

This folder is the complete workshop starter. Open or extract the full
`tic-tac-toe` folder before starting the lab, including the hidden
`.github/skills` directory.

There is no required git repository, branch, pull request, CI pipeline, merge
step, or human gate in this interactive lab. Everything happens locally in this
folder.

## Prerequisites

You need:

- Node.js and npm available in your terminal.
- GitHub Copilot CLI, VS Code agent mode, or another skills-compatible coding
  agent that can read this folder.
- Enough local permissions to install npm dependencies.

The target stack is React, Vite, TypeScript, Vitest, React Testing Library, and
the CRAP Vitest adapter configured by the bootstrap skill.

## Workflow

Use three separate prompts.

### Prompt 1: Generate Tasks

```text
Use /spec-to-task to generate implementation-ready tasks from spec.md.
```

Expected result: a `tasks/` directory exists, including `tasks/status.md`, and
no application source code has been created yet.

### Prompt 2: Bootstrap React And Gates

```text
Use /bootstrap-react to implement the bootstrap tasks.
```

Expected result: the React/Vite/TypeScript project exists, local validation
scripts are configured, the Vitest CRAP adapter runs with threshold `6` and
text output, and a smoke test proves the gate path works.

### Prompt 3: Implement Feature Tasks

```text
Use /implement-task to implement all remaining Tic Tac Toe feature tasks sequentially.
```

Expected result: every feature task is implemented in order, with tests, CRAP
gate evidence, local AI review, valid review fixes, and updated task status.

## Task Tracking

Prompt 1 creates `tasks/status.md`. Prompt 2 and Prompt 3 must keep it updated.

Allowed task statuses:

- `pending`
- `in-progress`
- `completed`
- `blocked`

Do not move to the next implementation task until the current task has recorded
gate evidence and status.

## Evidence Checklist

At the end of Prompt 3, the coding agent should report:

- app start command
- validation commands and results
- tests run during each task loop
- CRAP result for each task loop
- local AI review findings per feature task
- fixes made from valid review findings
- remaining limitations or missing evidence

Do not treat a gate as passed without evidence.
