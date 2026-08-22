# AGENTS.md

This repository is a designer-led, agent-implemented autobattler design laboratory.

## Required reading before any code change

1. Read `docs/STATUS.md`.
2. Read the active milestone in `docs/milestones/`.
3. Read `docs/ARCHITECTURE.md`.
4. Read relevant entries in `docs/DECISIONS.md`.
5. Inspect existing implementation and tests before proposing changes.

## Operating rules

- The human designer owns product intent, game rules, balance values, and prioritization.
- Do not invent or rebalance gameplay values unless explicitly instructed.
- Do not implement future milestones early.
- Prefer the smallest change that satisfies the current task.
- Do not refactor unrelated systems while implementing a feature.
- Do not add dependencies unless necessary; explain any new dependency before adding it.
- Prefer simple, readable implementations over clever abstractions.
- If documentation and implementation disagree, stop and report the conflict before changing behavior.

## Architecture rules

- Gameplay simulation must be runnable without UI or rendering.
- UI observes game state; UI must not own authoritative gameplay state.
- Gameplay rules belong in the engine, not in React/components/rendering code.
- Randomness must flow through a seeded RNG abstraction.
- Same starting state + same seed must produce the same simulation result.
- Game content should be data-driven where practical.
- Bots must use the same public game actions available to human-controlled players.

## Testing rules

- Every gameplay feature requires automated tests.
- Every bug fix should first have a regression test when practical.
- Never delete, weaken, or skip a failing test merely to make the suite pass.
- Run relevant tests after changes.
- Run the full test suite before declaring a task complete.

## Task protocol

For non-trivial changes:

1. Inspect.
2. Explain the proposed implementation plan without editing code.
3. Identify files/systems likely to change and risks.
4. Wait for explicit instruction to implement when the human asked for planning only.
5. Implement the scoped task.
6. Run tests.
7. Summarize exactly what changed and any remaining concerns.
8. Update `docs/STATUS.md` only after the work is verified.

## Scope protection

Ideas that are not part of the current milestone belong in `docs/IDEA_BACKLOG.md`, not in implementation.

Do not implement abilities, traits, items, economy, shops, augments, bots, networking, polished art, or production-client features during Milestone 01 unless the milestone document is explicitly amended.
