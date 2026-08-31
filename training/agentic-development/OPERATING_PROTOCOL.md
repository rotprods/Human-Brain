# Agentic Development Operating Protocol v1

Generated from Human-Brain first-principles constraints + T001 training. This is a living protocol, not a permanent doctrine.

## 1. Default execution mode

Use the **smallest sufficient agentic topology**.

```text
single agent
  ↓ only if needed
manager + one worker
  ↓ only if needed
manager + isolated parallel workers
  ↓ only if needed
heterogeneous deep/critical ensemble
```

Escalation requires a reason: parallelizable work, uncertainty, risk, specialist need, or independent verification value.

## 2. Material-decision gate

Before implementation, ask:

> Is there a material product/architecture/risk decision that cannot be resolved from canonical artifacts, evidence, code or a reversible experiment?

- **No** → proceed.
- **Yes** → surface one highest-leverage decision with options + recommendation; persist the answer immediately.

Never use clarification as a substitute for reading/reasoning.

## 3. Worker contract

Each worker receives:

```text
Task ID
Priority
Objective
Read-first pointers
Writable scope
Constraints
Validation
Return shape
Stop/escalation condition
```

Workers expose state:

`queued | running | blocked | awaiting_review | done | failed | cancelled`

The manager integrates; workers do not independently merge canonical state.

## 4. Priority discipline

Priorities:

`P0 critical > P1 high > P2 normal > P3 low/background`

A newly completed P0/P1 result or blocker preempts handling of lower-priority completions.

Priority is tied to user/goal impact, unblock value and risk, not agent age or notification order.

## 5. Isolation

When more than one agent can mutate code/state concurrently:
- partition files/state, or
- use isolated worktrees/environments.

Never run parallel writers against the same checkout without a specific concurrency-safe mechanism.

Worktrees are triggered by collision risk, not required for trivial single-agent work.

## 6. Long autonomy / goal contract

Use persistent autonomous loops only for tasks with verifiable progress and stop conditions.

Required contract:

```text
Objective:
Read first:
Constraints:
Validate:
Checkpoints:
Document:
Stop when:
```

Hard rule:

> Do not delete, skip, weaken, narrow or rewrite tests/evals merely to satisfy the stop condition.

If progress stalls or a new material decision appears, stop and escalate rather than churning.

## 7. Review routing

Review effort = function(change size, blast radius, reversibility, security risk, scientific impact, uncertainty).

### Tiny/reversible
Targeted self-check + validation.

### Medium/material
Independent code/QA/questions review as relevant.

### High-risk/large
`/gauntlet-loop` with independent heterogeneous reviewers, conditional security/performance/science passes and evidence-based synthesis.

Never recursively demand fresh issues. A reviewer may return zero real findings.

## 8. Review synthesis

Independent reviewers do not see each other's first-pass conclusions.

Afterward:
1. merge findings;
2. dedupe;
3. rank corroborated evidence;
4. verify against executable reality;
5. reject style-only/theoretical noise;
6. preserve unresolved disagreement;
7. remediate blockers;
8. rerun relevant validation.

A finding is not fixed simply because a model said so.

## 9. Integration lock

Canonical merge/push/deploy is single-writer.

Lock scope:

`reconcile → merge → full relevant validation → push → CI → deploy → health check`

Workers may continue isolated research, but no competing writer enters integration until release.

## 10. Safety hooks

Before side effects, guard against:
- destructive filesystem scope escape;
- force rewrite of shared Git history;
- secret/password-manager scraping;
- uncontrolled production writes;
- unsafe deployment/infra mutation;
- provenance-free destructive automation.

Risk-based permissions override convenience. “YOLO mode” is never a universal policy.

## 11. Production reality

If production data access exists, provide read-only access by default for reality checks. Write capability requires a separate explicit controlled path.

Executable reality outranks plans/docs.

## 12. Tests

Add tests where they prevent meaningful regressions.

Do not maximize count. Prefer the cheapest layer that catches the failure:
- unit for local pure logic;
- property tests for invariants;
- contract/integration for wiring;
- reality probes for actual execution paths;
- regression tests for expensive bug classes.

## 13. Progressive disclosure

Do not preload every skill/training document.

Routing flow:

`task → relevant training node → module → optional source/reference`

Only expand context when required.

## 14. Skills/automation threshold

- one repeated command → alias/snippet;
- repeated multi-step workflow → skill candidate;
- recurring agent task → schedule/heartbeat only if event/time semantics justify it.

Do not create permanent infrastructure from one-off behavior.

## 15. Heartbeats

Prefer event-driven triggers.

If polling is necessary:
- cheap gate first;
- durable `last_run`/state;
- active hours if relevant;
- silence when nothing changed;
- no tight-loop LLM invocation;
- verify a real firing before declaring operational.

## 16. Handoff

Handoff content:
- current state;
- why decisions were made;
- rejected/dead-end approaches;
- blockers/dependencies;
- exact canonical pointers.

Reference; do not duplicate. Never include secrets. New agents must verify handoff claims against canonical artifacts/code.

## 17. ADR threshold

Create ADR only when:
- decision is durable;
- alternatives were materially different;
- rationale is not obvious from code;
- future agents would plausibly reverse it without context.

## 18. Volatile model/harness knowledge

Store specific models, providers, subscription limits and prices as dated observations with TTL/review date.

Never hardcode “best model” into permanent policy without benchmarks. Model selection is empirical routing data.

## 19. Queued/pre-sent work

The manager may queue likely next actions to reduce idle time, but every queued action must re-read predecessor state before execution. Queueing is scheduling, not stale pre-authorization.

## 20. Productivity

Optimize accepted outcomes, not activity.

Future metrics:
- verified lead time;
- accepted changes per unit time/compute;
- rework rate;
- escaped defects;
- blocked worker time;
- integration overhead;
- reviewer false positives;
- human interventions;
- cost/tokens per accepted outcome.

## 21. Protocol evolution

A training rule can be promoted/demoted only with explicit reason:

```text
ACCEPTED ↔ PROVISIONAL ↔ ADAPTED ↔ REJECTED ↔ DEFERRED
```

Volatile facts expire independently.

Every material protocol change must update the training graph and state pointers.
