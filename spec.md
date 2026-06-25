# Tic Tac Toe Technical Specification

## Goal

Build a browser-based Tic Tac Toe game using React, Vite, and TypeScript.

The implementation must separate game rules from the React UI so that the core
game behavior can be tested without rendering components. The result should be
small, maintainable, and structured enough to support local quality gates.

## Functional Behavior

The application displays a 3 x 3 Tic Tac Toe board for two local players using
the same browser.

Required behavior:

- The board starts empty.
- Player `X` always takes the first turn.
- Players alternate between `X` and `O` after every valid move.
- A player makes a move by selecting an empty cell.
- Selecting an occupied cell must not change the board or current turn.
- Selecting a cell after the game has ended must not change the board.
- The game detects wins across all rows, columns, and diagonals.
- The game detects a draw when all cells are filled and no player has won.
- The UI shows whose turn it is while the game is in progress.
- The UI shows the winning player when the game is won.
- The UI shows a draw message when the game ends without a winner.
- A reset control starts a new empty game with `X` to move.

## Interfaces And Boundaries

The implementation must have two clear parts:

- Game core: pure TypeScript functions and types for board state, moves, turn
  handling, winner detection, draw detection, and reset behavior.
- React UI: components that render the board, status, and reset control, and
  call the game core to update state.

The React components must not duplicate game-rule logic that belongs in the
game core. Component tests may verify rendering and user interaction, but the
core rules must be covered by focused unit tests.

## Data And State Model

Use explicit domain concepts for the game state. The exact implementation names
may vary, but the model must represent:

- `Player`: either `X` or `O`.
- `Cell`: either empty or occupied by a player.
- `Board`: exactly nine cells.
- `GameStatus`: in progress, won, or draw.
- `GameState`: board, current player, status, and winner when applicable.

Board cell positions must be stable and deterministic. A zero-based index from
`0` to `8` is acceptable. If another representation is chosen, the mapping must
be simple, documented in code, and covered by tests.

## Rules And Invariants

The implementation must preserve these invariants:

- The board always contains exactly nine cells.
- Only `X`, `O`, or empty values may appear in cells.
- `X` makes the first move of every new game.
- A valid move writes the current player to exactly one empty cell.
- A valid non-terminal move switches the current player.
- Invalid moves do not change the game state.
- Once a win or draw is reached, further moves do not change the game state.
- Reset returns to a fresh empty board with `X` as current player.
- A game cannot be both won and drawn.
- A winner can only be `X` or `O`.

## Edge And Exceptional Cases

The implementation must handle these cases:

- First move in any valid cell.
- Attempted move on an occupied cell.
- Attempted move after a win.
- Attempted move after a draw.
- Win on each of the three rows.
- Win on each of the three columns.
- Win on each of the two diagonals.
- Draw after the ninth move when there is no winner.
- Reset after an in-progress game.
- Reset after a win.
- Reset after a draw.

If the game core exposes a function that accepts a cell index, indexes outside
the board must be handled safely. The function may reject the move by returning
the unchanged state or by returning a typed error/result, but it must not corrupt
state.

## UI Requirements

The browser UI must provide:

- A visible 3 x 3 board.
- One interactive control per board cell.
- Visible `X` and `O` marks.
- A status message for current turn, winner, or draw.
- A reset button.

Accessibility requirements:

- Cell controls must be keyboard reachable.
- Cell controls must have understandable accessible names.
- The status message must be available as text.
- The reset control must be a real button.

Visual styling should be simple, readable, and stable. Advanced animation and
decorative effects are out of scope.

## Validation Strategy

The implementation must provide local validation commands for:

- TypeScript type checking.
- Unit tests for the game core.
- Component or interaction tests for the React UI.
- Coverage as part of the non-watch test run.
- CRAP metric analysis through the Vitest adapter.

CRAP analysis must use `@barney-media/crap-typescript-vitest` integrated into
the Vitest configuration through `withCrapTypescriptVitest`.

Required CRAP configuration:

- `threshold: 6`
- `format: "text"`
- `junit: false`

The CRAP threshold must not be lowered, bypassed, or disabled to make the gate
pass. If the CRAP gate fails, improve the code structure and tests until the
gate passes.

The CRAP gate must be based on tool output, not guessed values. If CRAP tooling
cannot produce evidence for a task, the result must be reported as missing
evidence or not applicable, not as passed.

## Acceptance Criteria

The implementation is acceptable when:

- The app can be started locally in a browser.
- The initial board is empty and `X` is shown as the first player.
- Valid moves place the correct mark and alternate turns.
- Invalid moves do not alter state.
- All row, column, and diagonal wins are detected.
- Draw state is detected correctly.
- Reset works from in-progress, won, and draw states.
- Core game rules are covered by unit tests.
- UI interactions are covered by component or interaction tests.
- Type checking passes.
- Relevant tests pass.
- CRAP analysis passes for relevant functions or reports a justified
  not-applicable/missing-evidence status.

## Non-Goals

Do not implement:

- AI opponent.
- Online or local network multiplayer.
- Backend service.
- Persistence across browser refreshes.
- Authentication or user profiles.
- Score history.
- Advanced animations.
- Internationalization.
- Mutation testing.
- Version control, pull requests, merge workflow, or CI integration.
