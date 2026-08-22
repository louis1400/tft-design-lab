# Product Vision

## Purpose

Build a lightweight, trustworthy autobattler design laboratory that lets a game designer create TFT-like content, run deterministic combats and eventually full-game simulations, inspect telemetry, conduct human playtests, and iterate based on evidence.

This is an independent portfolio and design-research project. It is not affiliated with Riot Games and is not intended to reproduce Riot's production client, assets, backend, or proprietary technology.

## Primary user

The primary user is the designer building and evaluating an original set inside TFT-like structural constraints.

## Core portfolio claim

The project should demonstrate:

- understanding of autobattler combat and economy systems;
- ability to formulate design hypotheses;
- ability to prototype mechanics;
- ability to create designer-facing tools;
- ability to gather quantitative and qualitative evidence;
- ability to diagnose problems and iterate;
- ability to distinguish simulation evidence from human-player experience.

## Product principles

1. **Design questions first.** Build systems because they enable a meaningful design test.
2. **Trustworthiness over spectacle.** A simple simulator whose rules are understandable and reproducible is more valuable than polished visuals with uncertain behavior.
3. **Headless by default.** Important simulations must run without graphics.
4. **Human-readable systems.** Designer tools should make values, outcomes, and reasoning inspectable.
5. **Iteration speed matters.** Balance and content values should eventually be editable without rewriting engine code.
6. **Evidence, not false certainty.** Bot results and combat statistics are signals, not substitutes for human playtesting.
7. **Portfolio traceability.** Important hypotheses, changes, failures, and lessons should be preserved for later case-study use.

## Long-term target experience

A designer should eventually be able to:

1. Define or edit units, traits, abilities, items, and set mechanics.
2. Construct boards manually.
3. Watch a battle visually.
4. Replay a battle from a deterministic seed.
5. Run hundreds or thousands of combats headlessly.
6. Compare boards and balance changes using telemetry.
7. Play a complete economy-driven match against bots.
8. Inspect why bots made strategic decisions.
9. Run human playtests.
10. Record design conclusions and iterate.

## Explicit non-goals

Unless a later milestone changes these deliberately, this project is not trying to build:

- a production-ready TFT clone;
- Riot assets, champions, maps, or exact UI;
- multiplayer networking;
- account systems;
- matchmaking;
- anti-cheat;
- monetization;
- production-scale backend services;
- highly polished animation or visual effects;
- exact undocumented TFT implementation details;
- an engine-learning exercise for the human designer.

## Technology direction

Favor a browser-accessible TypeScript-based project with a headless simulation engine separated from the visual application. Specific tooling may be selected during repository bootstrap, but architecture must preserve this separation.

## Success condition

The project succeeds when it enables a credible portfolio case study showing a sequence such as:

**design hypothesis → implementation → simulation/playtest evidence → diagnosis → iteration → measured/observed outcome**

The quality of this reasoning loop matters more than graphical polish or feature count.
