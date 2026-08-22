# Architecture

## Objective

Keep the simulation trustworthy, testable, deterministic, and independent from presentation so the project can support both visual playtesting and large headless simulation runs.

## High-level structure

Target structure, subject to small implementation adjustments during bootstrap:

```text
apps/
  lab/              # browser UI / visual playground

packages/
  engine/           # authoritative gameplay simulation
  content/          # data definitions for units and later game content
  analytics/        # telemetry and simulation analysis
  bots/             # strategic agents; later milestone

tests/              # integration/e2e tests when appropriate

docs/
```

Do not create packages merely to satisfy this diagram. Create them when the active milestone needs them.

## Authority boundaries

### Engine

The engine owns authoritative gameplay state and rules.

Examples:
- unit HP;
- positions;
- target selection;
- movement legality;
- attack timing;
- damage resolution;
- death;
- combat end conditions;
- seeded randomness.

The engine must run in a Node/headless environment without DOM, Canvas, React, browser timing, or animation APIs.

### UI

The UI is a client of the engine.

It may:
- create legal starting configurations;
- send supported commands/actions;
- observe snapshots/events;
- animate or visualize engine outcomes;
- display telemetry.

It must not contain authoritative gameplay rules.

### Content

Content describes game pieces and designer-controlled values. Where practical, changing a unit's HP, AD, range, or later ability parameters should not require modification of simulation algorithms.

### Analytics

Analytics consumes simulation outputs. It must not affect simulation results.

### Bots

Bots eventually decide which public actions to take. They may inspect only information intentionally exposed to players/agents. They must not directly mutate hidden engine state or create impossible boards/resources.

## Determinism

Determinism is a core feature, not an optimization.

Given:
- identical initial state;
- identical rules/content version;
- identical seed;
- identical sequence of player actions;

the simulation must produce the same outcome and event ordering.

Rules:
- no direct `Math.random()` in gameplay code;
- randomness goes through a seeded RNG abstraction;
- avoid dependence on wall-clock time;
- avoid dependence on render frame rate;
- define deterministic tie-breaking where ordering would otherwise be ambiguous.

## Simulation time

Combat logic should use simulation time controlled by the engine rather than browser frame time. The specific tick/event implementation may be chosen during bootstrap, but it must support running faster than real time and without rendering.

## Event visibility

Prefer producing inspectable gameplay events or equivalent structured telemetry for meaningful events such as:
- target acquired;
- movement;
- attack started/resolved;
- damage dealt;
- unit died;
- combat ended.

Do not over-engineer an event system during early milestones. The requirement is inspectability, not a sophisticated event bus.

## State mutation

Authoritative state changes should pass through engine rules. UI and future bot code must not mutate engine state directly.

## Testing strategy

Tests should focus on behavioral contracts, including:
- deterministic replay;
- targeting rules;
- movement rules;
- attack timing;
- damage/death;
- combat termination;
- invariants (e.g. dead units cannot act).

Prefer small deterministic fixtures over huge snapshot tests.

## Performance direction

Milestone 01 should prioritize correctness and clarity. The architecture must permit headless batch simulation, but premature optimization is prohibited. Profile before optimizing.

## Dependency policy

Keep dependencies modest. Libraries are acceptable when they clearly reduce project complexity or provide commodity infrastructure (testing, build tooling, UI framework). Core gameplay semantics should remain understandable from project code.

## Change policy

If a proposed change violates one of these boundaries, record an explicit architecture decision in `docs/DECISIONS.md` before implementation.
