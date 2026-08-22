# Roadmap

## North star

Build a designer-facing laboratory that is behaviorally close enough to Teamfight Tactics that design experiments performed inside it are meaningfully informative for TFT set design.

This is not a generic autobattler project. The engine should deliberately model observed, documented, and testable TFT behavior where that behavior matters to set design.

"Accurate" does not mean reproducing Riot's proprietary source code, assets, backend, or every undocumented implementation quirk. It means establishing and continuously testing a behavioral compatibility target against real TFT.

## Fidelity strategy

Fidelity is a recurring validation track, not a one-time milestone.

For each major system we will:

1. Document the TFT behavior we intend to model.
2. Implement the smallest compatible rule set.
3. Create deterministic reference tests / golden fixtures.
4. Compare the lab against observable TFT behavior from a fixed reference patch.
5. Record known mismatches explicitly.
6. Resolve mismatches that materially affect design conclusions before proceeding.

We will maintain a **Reference Set Slice**: a deliberately limited subset of one historical/frozen TFT patch containing enough real units, traits, items, boards, and interactions to test whether the lab actually feels and behaves like TFT.

Using a frozen patch avoids live hotfix drift and gives the project a stable calibration target.

## Phase 0 — Foundation (current)

- Repository memory and operating rules.
- Architecture boundaries.
- Deterministic/headless requirements.
- Codex planning workflow.

Exit condition: repository bootstrap plan approved and implementation foundation verified.

## Phase 1 — Basic deterministic combat

Build generic combat primitives only:

- board positions;
- target acquisition;
- deterministic movement;
- attack timing;
- damage;
- death/retargeting;
- combat end;
- replayable seeds;
- telemetry;
- headless batch execution.

Purpose: prove the simulation architecture before attempting TFT compatibility.

## Phase 2 — TFT combat compatibility layer

Replace or refine generic assumptions using an explicit TFT behavioral contract.

Candidate systems include:

- hex-board geometry and distance;
- movement/pathfinding behavior;
- targeting and deterministic tie rules where known;
- attack cadence/windup model;
- mana generation;
- spell casting and cast locks;
- physical/magic/true damage;
- armor and magic resistance;
- crit behavior where relevant;
- shields, healing, omnivamp where relevant;
- crowd control and immunity rules;
- range and targeting patterns;
- combat timing/overtime if required;
- event ordering and simultaneous effects.

Exit condition: core TFT-like combat rules are documented, tested, and sufficiently stable to implement reference content.

## Phase 3 — Reference Set Slice: combat calibration gate

Select one frozen TFT patch and reproduce a limited real slice of it.

Target slice:

- roughly 10–15 units spanning multiple costs/roles;
- 4–8 interacting traits;
- a representative selection of items;
- several known board configurations;
- enough spell/trait patterns to stress the engine.

Use actual public gameplay behavior and public numerical data as calibration references, but do not copy Riot source code or production assets.

Validate at multiple levels:

### Rule-level
Examples: damage formulas, mana timing, range, targeting, attack cadence, trait triggers.

### Scenario-level
Recreate controlled board states and compare event sequences, cast timings, pathing, targeting, survival patterns, and combat duration with observable TFT behavior.

### Distribution-level
Where deterministic one-to-one comparison is impossible, run repeated scenarios and compare qualitative/statistical outcome distributions rather than demanding identical individual battles.

### Feel-level
Human designer watches/plays representative combats and records mismatches such as movement, pacing, targeting, or spell timing that make the simulator feel unlike TFT.

Exit condition: all material mismatches are either fixed or explicitly documented as acceptable limitations. Original set design should not depend on a known inaccurate subsystem.

## Phase 4 — Designer Lab

Build tools for the designer rather than requiring code edits:

- board builder;
- unit/content editor;
- trait/item parameter editing;
- combat inspector;
- seed replay;
- telemetry views;
- quick A/B comparison.

The existing Reference Set Slice remains available as a regression suite.

## Phase 5 — Combat-scale simulation

- Hundreds/thousands of headless combats.
- Board-vs-board testing.
- Structured telemetry.
- Batch seed replay.
- Comparative balance experiments.

Every engine change must continue passing the reference-slice compatibility suite.

## Phase 6 — TFT economy and game-flow compatibility

Model the strategic layer needed for actual TFT set design, including as appropriate:

- gold;
- interest/streaks;
- shop generation;
- level and XP costs;
- shop odds;
- bench/board limits;
- shared unit pools;
- unit combining/star levels;
- selling;
- player HP and player damage;
- round/stage progression;
- item/loot delivery abstractions needed for testing;
- other set-independent rules required by the chosen reference patch.

Exact scope should be driven by what is necessary to evaluate set design rather than by desire to recreate the production client.

## Phase 7 — Reference Set Slice: full-game calibration gate

Extend the frozen reference slice far enough to play meaningful TFT-like game sequences.

Compare:

- economy pacing;
- leveling/rolling decisions;
- shop distributions;
- board-strength progression;
- upgrade frequency;
- combat pacing;
- representative composition curves;
- other observable systemic behavior.

Exit condition: the lab is credible enough that we trust it as a set-design environment, with known limitations documented.

## Phase 8 — Strategic bots

Build agents that operate through the same legal actions available to humans.

Bots should eventually support different strategies (tempo, reroll, economy, vertical, flex) and expose inspectable reasoning.

Bots are testing instruments, not substitutes for human playtesting.

## Phase 9 — Original TFT-style set alpha

Only after the relevant compatibility gates:

1. Set thesis.
2. Design pillars and anti-goals.
3. Set mechanic.
4. Trait topology.
5. Roster/role/cost skeleton.
6. Champion/unit kits.
7. Set-specific augments/items/mechanics as required.

The original set is designed *inside the calibrated lab* rather than against a generic autobattler approximation.

## Phase 10 — Human-playable set

- Full match flow against bots.
- Human playtests.
- Qualitative feedback capture.
- Compare human observations with simulation evidence.

## Phase 11 — Evidence-driven iteration

Repeated loop:

**hypothesis → implementation → simulation/reference checks → human playtest → diagnosis → iteration → re-test**

Maintain compatibility tests so changes to support original mechanics do not silently break TFT baseline behavior.

## Phase 12 — Portfolio case study

Present:

- why the lab was built;
- how TFT fidelity was defined and validated;
- the Reference Set Slice and known limitations;
- designer tooling;
- original set thesis/mechanics;
- simulation experiments;
- human playtests;
- failures and iterations;
- final conclusions.

The strongest portfolio claim is not "I cloned TFT." It is:

**"I built and validated a controlled TFT-compatible design laboratory, then used it to design and iterate an original set with evidence."**
