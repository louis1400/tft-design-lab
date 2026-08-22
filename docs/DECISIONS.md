# Architecture and Product Decisions

Record durable decisions here when they would otherwise be easy to forget or accidentally reverse.

---

## D-001 — Headless simulation is mandatory

**Status:** Accepted

**Decision:** The authoritative gameplay simulation must run without React, Canvas, DOM APIs, animations, or browser timing.

**Why:** The project must support fast batch simulation and deterministic testing as well as visual playback.

**Implication:** Presentation observes engine state; presentation never owns gameplay truth.

---

## D-002 — Deterministic seeded randomness

**Status:** Accepted

**Decision:** All gameplay randomness must go through a seeded RNG abstraction. Direct `Math.random()` usage in gameplay code is prohibited.

**Why:** Bugs, balance anomalies, and interesting combats need to be exactly reproducible.

**Implication:** Same initial state + same seed + same action sequence should produce the same result.

---

## D-003 — TypeScript-first browser-accessible direction

**Status:** Accepted for bootstrap; revisit only with evidence.

**Decision:** Start with a TypeScript-based codebase designed to support a browser UI and a Node/headless simulation path.

**Why:** This minimizes tooling friction for an agent-implemented project and makes eventual portfolio demos easy to access.

**Implication:** Avoid engine-specific architecture that would make headless simulation or web delivery difficult.

---

## D-004 — Scope is milestone-gated

**Status:** Accepted

**Decision:** Features from later milestones are not implemented early merely because they are interesting or convenient.

**Why:** The project should reach trustworthy working states quickly and avoid compounding unknowns.

**Implication:** New ideas go to `docs/IDEA_BACKLOG.md` unless the active milestone is explicitly amended.

---

## D-005 — TFT fidelity requires a frozen Reference Set Slice

**Status:** Accepted

**Decision:** This project is not merely a generic TFT-inspired autobattler. Before the lab is trusted for original set design, relevant systems must be calibrated against observable behavior from a fixed historical TFT patch using a limited Reference Set Slice.

**Why:** The designer already knows how TFT feels and needs evidence that the lab is modeling TFT rather than an accidental alternate autobattler. Without calibration, simulation results could be precise but irrelevant because the underlying rules are wrong.

**Implication:** Fidelity becomes a recurring validation track. We will reproduce representative real units, traits, items, board states, and later economy/game-flow scenarios; create golden/reference tests; compare timing, targeting, movement, formulas, event ordering, pacing, and outcome distributions; and explicitly document known mismatches.

**Boundary:** We are validating behavior, not reproducing Riot source code, production assets, backend systems, or every undocumented quirk regardless of design relevance.

**Gate:** Original set implementation must not depend on a subsystem with a known material TFT-fidelity mismatch unless that limitation is explicitly accepted and documented.
