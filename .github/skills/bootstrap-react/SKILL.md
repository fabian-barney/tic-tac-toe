---
name: bootstrap-react
description: Bootstrap the Tic Tac Toe React/Vite/TypeScript project and local gates. Use for the workshop's second prompt after spec-to-task generated tasks.
---

# Bootstrap React

Implement only bootstrap tasks from `tasks/status.md`. Do not implement Tic Tac
Toe rules or final UI beyond the smallest placeholder needed to prove the app
and gates run.

## Required Reads

Before editing, read:

- `spec.md`
- `AGENTS.md`
- every file in `docs/adr/`
- `tasks/status.md`
- every bootstrap task file

## Bootstrap Scope

Create the React/Vite/TypeScript project in the current folder. The folder is
not empty, so do not depend on a generator that requires an empty directory. If
using a generator, scaffold into a temporary directory and copy only the needed
project files back. Manual creation of the standard Vite project files is also
acceptable.

Configure:

- React
- Vite
- TypeScript
- Vitest
- React Testing Library
- jsdom test environment
- coverage for non-watch test runs
- `@barney-media/crap-typescript-vitest`
- one smoke test that proves the test/coverage/CRAP-integrated path runs

## Required Scripts

Configure `package.json` scripts:

```json
{
  "dev": "vite",
  "build": "tsc -b && vite build",
  "typecheck": "tsc --noEmit",
  "test": "vitest",
  "test:run": "vitest run --coverage",
  "validate": "npm run typecheck && npm run test:run"
}
```

## Vitest CRAP Adapter

Configure Vitest with the CRAP adapter. The configuration must use the fixed ADR
settings:

```ts
import { withCrapTypescriptVitest } from "@barney-media/crap-typescript-vitest";

export default withCrapTypescriptVitest(
  defineConfig({
    plugins: [react()],
    test: {
      environment: "jsdom",
      setupFiles: ["src/test/setup.ts"],
      coverage: {
        reporter: ["text", "json"],
        reportsDirectory: "coverage"
      }
    }
  }),
  {
    threshold: 6,
    format: "text",
    junit: false
  }
);
```

Keep the threshold at `6`. Keep output format as `text`. Do not disable the
adapter to pass validation.

## Task Loop

For each bootstrap task:

1. Mark it `in-progress` in `tasks/status.md`.
2. Implement only that task's setup scope.
3. Run the relevant command for that task.
4. Record command output summary in the task file's implementation evidence.
5. Update `tasks/status.md`.

For the final bootstrap task, run:

```text
npm run validate
```

## Stop Condition

Stop when:

- dependencies are installed
- `npm run validate` runs
- the smoke test passes
- CRAP adapter output is visible as `text`, or the task records why no
  meaningful production functions are analyzable yet
- all bootstrap tasks are marked `completed` or one is marked `blocked` with a
  concrete blocker

Report completed setup tasks, commands run, validation result, CRAP adapter
evidence, missing evidence, and the local app run command.
