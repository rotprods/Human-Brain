# Human-Brain — DECISIONS

Only decisions that have survived current scrutiny are recorded here. Hypotheses remain hypotheses.

## D-001 — Clean-room architecture

**Decision:** Existing repositories do not define Human-Brain architecture.

**Reason:** Prevent legacy anchoring and accidental porting of TypeScript/Python/runtime assumptions into the Rust core.

**Status:** ACCEPTED PRINCIPLE.

## D-002 — Rust-first production core

**Decision:** Rust is the leading production-core language.

**Reason:** Strong fit for deterministic systems, explicit ownership, performance, concurrency control and long-lived low-level infrastructure.

**Status:** HIGH-CONFIDENCE; implementation details still experimental.

## D-003 — Minimum-sufficient complexity

**Decision:** New abstractions require an observed problem, simpler alternative analysis and measurable benefit.

**Status:** ACCEPTED PRINCIPLE.

## D-004 — ECP is a hypothesis, not recovered legacy

**Decision:** `Ensemble Cognitive Processing` is the proposed meaning of ECP for current research.

**Evidence:** `rotprods/ecp-framework` is empty and no prior canonical expansion was recovered.

**Status:** PROPOSED HYPOTHESIS; see `HB-HYP-001`.

## D-005 — Adaptive multi-model compute, not always-on swarm

**Decision:** If ECP survives experiments, model multiplicity must be adaptive. Fast/small/local models handle cheap low-risk work; stronger/deeper/parallel patterns are triggered by expected marginal value, uncertainty, risk or disagreement.

**Status:** HYPOTHESIS POLICY CONSTRAINT.

## D-006 — Routing constraints precede scalar scores

**Decision:** Privacy, context, modality, tools, availability and hard budgets filter candidates before any weighted utility score.

**Reason:** A cheap/fast model that cannot satisfy a hard requirement must never win by arithmetic.

**Status:** PROPOSED ECP DESIGN RULE.

## D-007 — /gauntlet-loop is a real outer verifier loop

**Decision:** `/gauntlet-loop` means iterative implementation → independent review → synthesis → remediation → revalidation → outer verification until verified or explicitly stopped.

**Evidence:** Context7 Ralph-loop semantics provide the nested-loop/verification pattern; ROTCLAW provides internal remediation+rereun evidence.

**Status:** ACCEPTED DEVELOPMENT PROTOCOL CANDIDATE.

## D-008 — Reviewer independence before synthesis

**Decision:** Expensive multi-model review, when triggered, starts with independent reviewer outputs before cross-critique/synthesis.

**Reason:** Reduce correlated anchoring and false consensus.

**Status:** ACCEPTED PROTOCOL RULE.

## D-009 — No raw graph maximalism

**Decision:** Persist only relationships that enable useful queries, validation, routing, impact analysis or decisions.

**Reason:** Maximum traceability does not require maximum coupling or representing every fact as a graph edge.

**Status:** ACCEPTED PRINCIPLE.
