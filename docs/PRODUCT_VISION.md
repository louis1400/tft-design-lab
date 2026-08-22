# Product Vision

## Purpose

Build a lightweight, trustworthy TFT design laboratory that lets a game designer create content, run deterministic combats and eventually full-game simulations, inspect telemetry, conduct human playtests, and iterate based on evidence.

The lab should be **behaviorally calibrated against real Teamfight Tactics** closely enough that experiments performed inside it are meaningfully informative for TFT set design. This is stronger than merely building a TFT-inspired autobattler.

This is an independent portfolio and design-research project. It is not affiliated with Riot Games and is not intended to reproduce Riot's production source code, assets, backend, or proprietary technology.

## Primary user

The primary user is the designer building and evaluating an original set inside TFT structural constraints.

## Fidelity target

The engine should model observed, documented, and testable TFT behavior wherever inaccuracies could materially distort a set-design conclusion.

We will not assume our approximation is correct merely because it "looks like an autobattler." Instead, the project will maintain a **Reference Set Slice** based on a frozen historical TFT patch. That slice will be used to calibrate and regression-test combat rules and, later, economy/game-flow behavior.

Accuracy will be evaluated through:

- rule-level numerical checks;
- deterministic reference scenarios where possible;
- event timing and ordering;
- movement/targeting/pathing observations;
- repeated outcome distributions where one-to-one comparison is not meaningful;
- human feel/pacing checks by someone familiar with TFT;
- an explicit list of known mismatches and limitations.

"TFT-compatible" does not mean claiming perfect reproduction of undocumented implementation details. It means knowing what is modeled, testing it against observable TFT, and not relying on known-inaccurate subsystems for design conclusions.

## Core portfolio claim

The project should demonstrate:

- understanding of TFT/autobattler combat and economy systems;
- ability to define and validate a behavioral model of an existing game;
- ability to formulate design hypotheses;
- ability to prototype mechanics;
- ability to create designer-facing tools;
- ability to gather quantitative and qualitative evidence;
- ability to diagnose problems and iterate;
- ability to distinguish simulation evidence from human-player experience.

## Product principles

1. **TFT fidelity before invention.** Before trusting the lab for original set work, calibrate the relevant systems against a real fixed TFT reference.
2. **Design questions first.** Build systems because they enable a meaningful design test.
3. **Trustworthiness over spectacle.** A simple simulator whose rules are understandable and reproducible is more valuable than polished visuals with uncertain behavior.
4. **Headless by default.** Important simulations must run without graphics.
5. **Human-readable systems.** Designer tools should make values, outcomes, and reasoning inspectable.
6. **Iteration speed matters.** Balance and content values should eventually be editable without rewriting engine code.
7. **Evidence, not false certainty.** Bot results and combat statistics are signals, not substitutes for human playtesting.
8. **Portfolio traceability.** Important hypotheses, fidelity findings, changes, failures, and lessons should be preserved for later case-study use.

## Long-term target experience

A designer should eventually be able to:

1. Load the frozen Reference Set Slice and reproduce representative TFT scenarios.
2. Inspect known fidelity mismatches and regression results.
3. Define or edit units, traits, abilities, items, and set mechanics.
4. Construct boards manually.
5. Watch a battle visually.
6. Replay a battle from a deterministic seed.
7. Run hundreds or thousands of combats headlessly.
8. Compare boards and balance changes using telemetry.
9. Play a complete economy-driven match against bots.
10. Inspect why bots made strategic decisions.
11. Run human playtests.
12. Record design conclusions and iterate.

## Explicit non-goals

Unless a later milestone changes these deliberately, this project is not trying to build:

- a production-ready TFT clone;
- Riot source code or proprietary backend behavior;
- Riot art, audio, maps, or exact production UI;
- multiplayer networking;
- account systems;
- matchmaking;
- anti-cheat;
- monetization;
- production-scale backend services;
- highly polished animation or visual effects;
- perfect reproduction of every undocumented TFT quirk regardless of design relevance;
- an engine-learning exercise for the human designer.

## Technology direction

Favor a browser-accessible TypeScript-based project with a headless simulation engine separated from the visual application. Specific tooling may be selected during repository bootstrap, but architecture must preserve this separation.

## Success condition

The project succeeds when it enables a credible portfolio case study showing both:

**TFT reference behavior → modeled rule → validation/calibration → known confidence/limitations**

and

**design hypothesis → implementation → simulation/playtest evidence → diagnosis → iteration → measured/observed outcome**

The quality and credibility of these reasoning loops matter more than graphical polish or feature count.
