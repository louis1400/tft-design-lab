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
