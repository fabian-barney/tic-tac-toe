# ADR 0001: Use CRAP Threshold 6

## Status

Accepted

## Context

The workshop demonstrates disciplined local quality gates without requiring git,
pull requests, CI, or external review infrastructure. Tic Tac Toe is small, so a
strict CRAP threshold is practical and useful for teaching branch reasoning,
focused tests, and simple implementation design.

## Decision

Use `@barney-media/crap-typescript-vitest` as the CRAP integration for Vitest.

Configure the adapter with:

```ts
withCrapTypescriptVitest(vitestConfig, {
  threshold: 6,
  format: "text",
  junit: false
});
```

The threshold is fixed at `6`. The output format is fixed as `text`.

## Consequences

- The CRAP gate runs as part of the Vitest non-watch validation path.
- Code that exceeds the threshold must be simplified, split, or better tested.
- The threshold must not be lowered to make implementation easier.
- The adapter must not be disabled to make validation pass.
- Production files must not be excluded just to hide failing methods.

## Alternatives Considered

- Threshold `8`: acceptable for some hard gates, but too lenient for a compact
  workshop exercise.
- CLI-only CRAP execution: useful generally, but the Vitest adapter better fits
  the local test loop because it combines tests, coverage, and CRAP evidence.
- No CRAP gate: rejected because the workshop explicitly teaches local quality
  gates and code/test improvement loops.
