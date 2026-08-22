# TFT Design Lab

An independent game-design research project for designing, simulating, playtesting, and iterating on a TFT-like autobattler set.

The goal is **not** to reproduce the production TFT client. The goal is to build the smallest trustworthy laboratory needed to test autobattler design hypotheses.

## Project philosophy

- Design first; implementation serves design.
- Headless simulation is a first-class requirement.
- Gameplay rules are deterministic when given the same seed and starting state.
- Game content is data-driven wherever practical.
- Every gameplay system needs automated tests.
- Scope is controlled through milestone gates.
- Important decisions and observations are written down instead of remembered.

## Start here

Humans and coding agents should read these in order:

1. `AGENTS.md`
2. `docs/STATUS.md`
3. `docs/PRODUCT_VISION.md`
4. `docs/ARCHITECTURE.md`
5. The current milestone in `docs/milestones/`
6. Relevant entries in `docs/DECISIONS.md`

## Current phase

Milestone 01 — Basic deterministic combat.

See `docs/STATUS.md` for the exact current task.
