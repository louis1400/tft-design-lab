# M01 — Basic Deterministic Combat

## Goal

Build the smallest trustworthy headless combat simulation that proves the project architecture works.

This milestone is intentionally boring. It exists to establish correctness, determinism, testability, and the engine/UI boundary before adding interesting game design.

## Player-visible concept

Two small teams of generic units are placed on a board. Units automatically acquire enemies, move into range, attack, take damage, die, and eventually one team wins.

No production visuals are required.

## In scope

### Unit state

Each unit needs, at minimum:
- stable identifier;
- team;
- position;
- current/max HP;
- attack damage;
- attack speed;
- attack range;
- alive/dead state;
- current target when applicable.

### Combat rules

Implement only enough rules for:
- valid enemy detection;
- deterministic target acquisition;
- deterministic tie-breaking;
- movement toward a target when out of range;
- stopping when in attack range;
- attacks according to attack speed;
- damage resolution;
- death at zero HP;
- dead units becoming unable to act or be targeted;
- combat termination when only one team has living units (or both have none, if possible).

### Time

Simulation time must be controlled by the engine and must not depend on browser render frames or wall-clock time.

### Randomness

Provide a seeded RNG abstraction even if M01 uses little or no randomness yet. Gameplay code must not call `Math.random()` directly.

### Headless execution

The combat simulation must be executable in a non-browser environment.

### Tests

Automated tests must cover fundamental rules and determinism.

## Explicitly out of scope

Do not implement:
- abilities;
- mana;
- spell casting;
- traits;
- items;
- crits unless absolutely required by a later amended spec;
- armor/MR complexity;
- crowd control;
- economy;
- shop;
- bench management;
- unit combining/star levels;
- augments;
- bots;
- networking;
- polished graphics;
- exact TFT champion data;
- exact undocumented TFT pathfinding/targeting quirks.

## Board representation

Choose a simple board representation that can support autobattler positioning and deterministic movement. It should not prematurely encode production-level TFT behavior.

If hexes materially increase bootstrap complexity, Codex should explain the tradeoff during planning rather than silently substituting a different representation. The final choice must be documented.

## Targeting principle

For M01, prefer a simple legible rule such as nearest valid enemy with deterministic tie-breaking. The exact rule must be documented and tested.

Do not attempt to reverse-engineer every TFT targeting exception.

## Movement principle

Movement should be deterministic and understandable. Correctness and inspectability are more important than perfect pathfinding sophistication in M01.

## Telemetry / inspectability

A combat run should expose enough structured information to determine at least:
- winner/result;
- combat duration or simulation steps;
- unit damage dealt;
- unit damage taken;
- survival/death;
- meaningful event sequence or equivalent debug trace.

The implementation can remain minimal.

## Acceptance criteria

M01 is complete only when all of the following are true:

- [ ] Two teams can be instantiated from data and placed on a board.
- [ ] Units identify valid enemy targets.
- [ ] Target selection has deterministic tie-breaking.
- [ ] Units move toward targets when out of range.
- [ ] Units stop moving when they can attack their target.
- [ ] Units attack according to a defined attack-speed/time model.
- [ ] Attacks deal damage.
- [ ] HP cannot remain below the engine's defined death boundary without the unit being dead.
- [ ] Units die when appropriate.
- [ ] Dead units cannot attack, move, or be selected as valid targets.
- [ ] Combat ends deterministically when a terminal team state is reached.
- [ ] The same initial state and seed produce the same outcome/event ordering.
- [ ] Gameplay code uses the seeded RNG abstraction rather than direct `Math.random()`.
- [ ] Combat can run headlessly without UI/rendering dependencies.
- [ ] Automated tests cover targeting, movement, attack timing, damage/death, combat end, and determinism.
- [ ] A simple batch runner can execute at least 1,000 small combats headlessly without correctness failures.
- [ ] The implementation remains within M01 scope.
- [ ] `docs/STATUS.md` is updated after verification.

## Suggested implementation sequence

This is guidance, not permission to skip the planning pass.

1. Repository/tooling bootstrap.
2. Core data types and simulation state.
3. Seeded RNG service.
4. Board/distance model.
5. Target acquisition.
6. Movement.
7. Attack timing and damage.
8. Death and retargeting.
9. Combat termination.
10. Structured telemetry/debug events.
11. Batch runner/performance sanity check.
12. Full M01 acceptance review.

## Definition of done

"It looks like combat" is not sufficient.

The milestone is done when the acceptance criteria are verified by tests and runnable headless behavior, with no known correctness issue being hand-waved into a later milestone.
