# PLAN-002 — Real /gauntlet-loop Development Protocol

Status: ACTIVE GOVERNANCE PLAN

## Exact meaning used in Human-Brain

`/gauntlet-loop` is an outer verification/remediation loop around an inner implementation/tool loop.

It is **not** a standard package named `gauntlet-loop`. Context7 found the closest documented pattern in Ralph Loop: an outer loop repeatedly runs an agent/tool loop, verifies completion, injects feedback into the next iteration, and stops on verified completion or explicit iteration/token/cost/abort limits.

Human-Brain extends that pattern with heterogeneous independent reviewers, evidence, tests and hard merge conditions.

## Real flow

```text
PR CONTRACT
   ↓
IMPLEMENT / INNER TOOL LOOP
   ↓
BUILD + TARGETED TESTS
   ↓
RISK CLASSIFICATION
   ↓
INDEPENDENT REVIEW FAN-OUT
   ├─ code
   ├─ security          [when triggered]
   ├─ QA
   ├─ questions
   ├─ performance       [when triggered]
   └─ science           [when biologically/scientifically relevant]
   ↓
ADVERSARIAL SYNTHESIS
   ↓
FINDINGS → PRIORITY → PATCH
   ↓
TARGETED REVALIDATION
   ↓
FULL RELEVANT VALIDATION
   ↓
OUTER VERIFIER
   ├─ VERIFIED → READY
   ├─ BLOCKERS → next loop with feedback
   ├─ STALLED → escalate/rethink architecture
   └─ BUDGET/MAX/ABORT → STOP unverified
```

## Reviewer independence

Reviewers receive the artifact and contract independently before seeing each other's conclusions. This reduces correlated anchoring and groupthink. Synthesis happens only after independent findings exist.

Different models/providers are preferred when the expected value of diversity justifies the cost; the cognitive router hypothesis in `HB-HYP-001` may later automate this.

## Adaptive reviewer selection

Do not run every expensive reviewer on every trivial change.

Always required:
- code/correctness review;
- QA/acceptance review;
- questions/assumption review.

Conditionally required:
- security for auth, tool execution, parsing, network, persistence, unsafe/FFI, dependencies, permissions or data boundaries;
- performance for hot paths, scale-sensitive structures or regressions;
- scientific review for brain-inspired models, equations, parameters or claims.

## Stop conditions

Verified only when all required conditions are true for the current PR:

```text
required_tests_failed        = 0
critical_findings            = 0
major_blocking_findings      = 0
security_high_or_critical    = 0
qa_acceptance_failures       = 0
must_answer_questions        = 0
determinism_failures         = 0  [when required]
science_validation_failures  = 0  [when required]
performance_budget_breach    = 0  [when required]
unresolved_review_conflicts  = 0
```

Non-success stops:
- iteration budget reached;
- token/cost budget reached;
- explicit abort;
- convergence stall.

## Convergence stall

A loop is stalled when remediation no longer produces meaningful state improvement, for example:
- the same blocking finding returns unchanged across two rounds;
- fixes oscillate between contradictory reviewer requirements;
- no measurable gate delta improves;
- the implementation repeatedly fails the same invariant.

Stall response: stop patch churn, reopen the underlying assumption/architecture and escalate reasoning depth/model strength if justified.

## Evidence from the existing ecosystem

ROTCLAW already exercised a real iterative gauntlet to 10/10 gates; it surfaced context-budget overflow and a self-referential recovery manifest that broke determinism, then fixed and reran them. Human-Brain treats this as evidence for remediation+rereun, not as architecture authority.

## Minimal persistence per loop

Do not build a giant governance platform initially. Persist only:
- current PR contract;
- findings with severity/evidence;
- validation results;
- loop number and stop reason;
- final disposition.

## Relationship to other plans

- `PLAN-002 --VALIDATES--> PLAN-001`
- `PLAN-002 --GOVERNS_IMPLEMENTATION_OF--> PLAN-003`
- `PLAN-002 --USES_WHEN_JUSTIFIED--> HB-HYP-001 cognitive ensemble routing`
