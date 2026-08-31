# Human-Brain — AGENTS.md

This repository is a research program and future Rust cognitive runtime. Agents must optimize for **correctness, measurable progress and minimum necessary complexity**, not maximum architecture.

## Read-first order

At the beginning of meaningful work, read:

1. `GOAL.md`
2. `STATE.md`
3. `DECISIONS.md`
4. `plans/README.md`
5. the active plan or experiment
6. only the relevant module under `training/agentic-development/`

Do **not** preload the whole training corpus. Human-Brain uses progressive disclosure: discover the relevant training node first, then load its source document only when the task triggers it.

## Core operating loop

```text
OBSERVE REALITY
→ DEFINE THE CONCRETE GAP
→ CHECK WHETHER A MATERIAL HUMAN DECISION IS MISSING
→ CHOOSE THE SMALLEST SUFFICIENT EXECUTION MODE
→ IMPLEMENT / EXPERIMENT
→ VALIDATE WITH REAL EVIDENCE
→ REVIEW PROPORTIONALLY TO RISK
→ RECONCILE STATE + DECISIONS + TRAINING IMPACT
```

## Human decision boundary

Agents are good implementers, searchers, debuggers and reviewers. They must not silently decide material product taste, irreversible architecture, risk posture, data ownership or user-facing behavior when multiple materially different choices remain and the answer cannot be resolved from canonical artifacts or evidence.

When a material decision is genuinely unresolved:
- surface only the highest-leverage unresolved decision;
- present concrete alternatives and a recommendation;
- persist the answer immediately when supplied;
- supersede stale docs rather than allowing contradictory decisions to coexist.

Do not ask unnecessary questions for routine implementation details that can be resolved from code, tests, connected sources or reversible experimentation.

## Agent state and priority

When more than one worker exists, every worker must expose a state:

`queued | running | blocked | awaiting_review | done | failed | cancelled`

and a priority:

`P0 | P1 | P2 | P3`

Higher-priority blockers and completed results are processed before lower-priority work. Do not allow a low-value completed worker to distract the manager from a P0/P1 result or blocker.

## Manager / worker contract

The manager agent owns:
- decomposition;
- worker selection;
- model/execution-mode choice;
- dependency ordering;
- integration;
- validation;
- final disposition.

Launch a worker/subagent only when:
1. the task is self-contained enough to brief completely;
2. parallelism creates real wall-clock or diversity value;
3. writable files/state can be isolated or partitioned;
4. expected value exceeds delegation/context overhead.

A worker starts blind. Its brief must contain objective, relevant paths/artifacts, constraints, validation and expected return shape. Workers must return concise findings/artifacts, not raw context dumps.

## Isolation rule

Never let parallel agents write the same working directory or uncontrolled shared mutable state.

Use one-task/one-worktree isolation when concurrency or collision risk justifies it. For tiny/single-agent work, worktrees are optional and may be needless overhead.

The primary checkout is an integration surface, not a multi-agent scratchpad.

## Goal-loop rule

Long autonomous loops are appropriate only when all are true:
- the work is substantially mechanical/iterative;
- a verifiable stop condition exists;
- the repository is sufficiently agent-ready.

A goal contract must state:
- Objective
- Read first
- Constraints
- Exact validation
- Checkpoints
- Stop condition
- Documentation expectation

Explicitly forbid reward hacking: never delete, skip, weaken or narrow tests/evals to make a goal appear achieved.

Exploratory architecture/research without a falsifiable stop condition is not a good goal-loop task.

## Review policy

Do not review recursively until an LLM invents problems.

Review depth is proportional to risk/change size. For material changes, prefer an independent reviewer/model family from the implementer when diversity has expected value.

Reviewer outputs are hypotheses until triaged against code, tests and evidence. Merge/dedupe findings, prioritize corroborated issues, discard style preferences/theoretical noise, and preserve genuine disagreement rather than forcing consensus.

Use `plans/002-gauntlet-loop-development/PLAN.md` for changes that warrant the full verification/remediation loop.

## Tests

Tests exist to protect behavior and invariants, not to maximize test count.

Add the minimum set that catches realistic regressions at the cheapest reliable layer. Prefer contract/integration/reality probes at critical boundaries where unit tests could pass while wiring is dead. Avoid test bloat and vanity coverage.

## ADRs / decisions

Use `docs/adr/` only for durable architectural decisions whose rationale cannot be reconstructed reliably from code. Record what was decided, why, alternatives/rejected approaches and project state at the time.

Do not create ADRs for routine implementation choices.

## Production/data access

Production access, if introduced, is read-only by default for agents. Reality-checking with real data is valuable; uncontrolled write access is not.

Any production mutation requires a separate explicit controlled workflow and authorization boundary.

## Integration lock

When multiple agents/branches exist, merge/push/deploy is a single-writer critical section. Only the integration owner may perform it while holding the logical push/integration lock.

The lock covers the sequence:

`reconcile → merge → validate → push → CI → deploy (if any) → health check`

No parallel agent may race this sequence.

## Heartbeats and scheduled work

Prefer events over polling. A heartbeat should gate slower checks from durable `last_run`/state metadata, do cheap work first, and stay silent when nothing changed.

Never claim a scheduled system works until at least one actual firing/delivery has been verified.

## Handoffs

A handoff records **state, not commands**.

Reference canonical artifacts instead of duplicating them. Preserve the why, rejected approaches, traps, blockers and exact pointers a fresh agent cannot cheaply rediscover. Treat handoff claims as context to verify, not truth above executable reality. Never include secrets.

## Repeated-work rule

- repeated one-step action → alias/snippet/preset;
- repeated multi-step workflow → candidate skill;
- create the skill only after repetition demonstrates value.

Skills must use progressive disclosure and narrow trigger descriptions.

## Volatile routing knowledge

Named models, subscriptions, prices, limits and preferred harnesses are volatile policy data, never permanent architectural law. Store them with observation date/source and re-benchmark before changing durable routing policy.

## Persistence rule

Material changes to goals, decisions, training rules or current state must be persisted before the interaction ends. Training is stored under `training/agentic-development/` and cross-store references are kept in `ARTIFACT_REGISTRY.yaml`.

Do not pretend SaaS resources are filesystem symlinks. Use stable logical aliases/URIs that resolve to exact GitHub paths, Drive IDs, Mem IDs and Airtable IDs.
