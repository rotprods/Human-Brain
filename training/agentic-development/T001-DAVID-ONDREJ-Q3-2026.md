# T001 — David Ondrej Agentic Engineering, Q3 2026

Status: INGESTED / DISTILLED
Observed: 2026-08-31
Source class: user-supplied article + verified official `davidondrej/skills` artifacts

## 0. How to read this module

This module does not canonize another engineer's personal stack. It separates:

- **durable engineering principles** that transfer across tools;
- **adaptations** needed for Human-Brain and Roberto's operating constraints;
- **volatile snapshots** of Q3-2026 products/models/pricing;
- **ideas explicitly rejected as universal rules**.

The goal is to improve our operating system, not imitate a setup.

---

## 1. Core thesis extracted

At high agentic-development throughput, the scarce resource stops being typing speed or individual code generation. The bottlenecks move toward:

1. selecting the right work;
2. maintaining state across many workers;
3. assigning priority;
4. isolating concurrent changes;
5. choosing the right model/harness for the job;
6. preserving human judgment for taste/architecture;
7. validating outputs without review theater;
8. integrating safely;
9. persisting enough state that work survives sessions/machines;
10. measuring whether the agentic system actually improves delivery.

This means a mature setup resembles a scheduler/control plane more than a single chatbot.

---

## 2. Interface is replaceable; state is not

### Source idea
David uses a multi-harness interface (`bb`), cmux/Ghostty for workspace/terminal control, Herdr as an agent runtime/state surface, and Corral as a priority-oriented completion queue.

### Durable principle — ACCEPTED
**Agent state tracking becomes mandatory once concurrency exceeds one.**

Canonical states for our protocol:

```text
queued
running
blocked
awaiting_review
done
failed
cancelled
```

Canonical priorities:

```text
P0 critical
P1 high
P2 normal
P3 low/background
```

A manager must process high-priority blockers/completions before lower-value finished workers.

### Why it matters
Without explicit state, a multi-agent system becomes notification-driven: whichever terminal makes noise first steals attention. That is not scheduling.

### Adaptation
We do not depend on bb/Herdr/Corral. They are implementations of a portable contract:

`WorkerId + TaskId + State + Priority + Dependency + UpdatedAt + ResultPointer`

---

## 3. Manager agent > uncontrolled swarm

### Source idea
David predicts manager-agent → many worker-agents, but explicitly argues that launch rules, model choice, permissions and task conditions should be designed by the operator rather than delegated blindly to a vendor harness.

### Durable principle — ACCEPTED
The manager owns decomposition, worker/model selection, dependency ordering, integration and verification.

Subagents are not a default source of intelligence. They are an execution primitive whose overhead must be justified.

### Launch threshold
Delegate only when all are sufficiently true:

1. task can be briefed as a self-contained contract;
2. parallelism/diversity has real expected value;
3. files or mutable state can be isolated/partitioned;
4. expected gain > context/delegation/integration cost.

### Verified official skill alignment
David's official `launch-subagent` skill reinforces that workers start blind, require a complete brief, should not touch the same files in parallel, and the main agent remains integrator/reviewer.

---

## 4. Isolation and worktrees

### Source idea
Worktrees are unnecessary ceremony for small/single-agent work, but become increasingly necessary at 20–30 concurrent agents.

### Official skill details
The official worktree skill formalizes:
- one task = one worktree = one agent session;
- primary checkout as integration point;
- no auto-merge;
- worktree bootstrap must include ignored env/deps/db/ports/generated files;
- worktrees isolate working files, not all shared Git state.

### Durable principle — ADAPTED
Use isolation when concurrency/collision risk justifies it. Never let parallel agents freely mutate the same checkout.

### Do not overengineer
For a tiny one-agent task, branch/worktree orchestration can cost more than the task. The trigger is **collision risk and concurrency**, not ideology.

---

## 5. Human judgment before irreversible architecture

### Source idea
`/ask-then-build` exists because agents can implement quickly but can silently make product/architecture choices with long-term consequences.

### Official skill behavior
It asks 3–6 non-obvious questions one at a time, records answers immediately, supersedes stale docs, then produces a tightly scoped implementation prompt.

### Durable principle — ADAPTED
Do not ask questions mechanically. First inspect code, connected sources and existing decisions. If a **material, non-resolvable** architectural/product/taste decision remains, surface one highest-leverage decision at a time with options + recommendation.

Persist the answer immediately.

### Anti-pattern
Using clarification as a substitute for reasoning is prohibited. Human review is for real choices, not routine reversible implementation details.

---

## 6. Goal loops as contracts, not infinite autonomy

### Official `goal-loop` finding
David defines a persistent loop:

`plan → act → test → review → iterate`

with lifecycle states and explicit stop conditions.

Recommended only when:
1. the work is substantially mechanical/long-running;
2. completion is objectively verifiable;
3. the repo is agent-ready.

### Goal contract — ACCEPTED
A long-running autonomous task needs:

- Objective
- Read first
- Constraints
- Exact validation command/eval
- Checkpoints
- Documentation expectation
- Stop condition

and explicit anti-reward-hacking:

> Do not delete, skip, weaken or narrow tests/evals to make the goal pass.

### Relationship to Human-Brain
Our `/gauntlet-loop` is the verification/remediation layer around meaningful goal/implementation loops. Goal loop pursues a contract; gauntlet proves the result deserves acceptance.

---

## 7. Review: diversity without review theater

### Source idea
David's `/total-review` launches two different high-end reviewers, then dedupes and ruthlessly removes overthinking.

### Official skill finding
The actual skill:
- runs two reviewers in parallel;
- waits for independent reports;
- merges/dedupes;
- gives extra weight to corroborated findings;
- explicitly says most review findings may be overthinking;
- asks for human approval before fixing.

### Durable principle — ACCEPTED
Review findings are hypotheses, not truth.

For material changes:
1. independent reviewer first passes;
2. preferably heterogeneous model families when economically justified;
3. merge/dedupe;
4. verify against code/tests/evidence;
5. discard style/theoretical noise;
6. retain genuine disagreement;
7. fix only real findings.

### Critical anti-pattern — ACCEPTED
**No recursive review loops that demand a fixed number of new issues.** Models can fabricate defects to satisfy the prompt.

Review depth must be proportional to risk, not ritual.

---

## 8. Repeated work becomes tooling

### Source idea
Single-step repetition → text replacement/alias/snippet.
Multi-step repetition → skill.

### Durable principle — ACCEPTED WITH THRESHOLD
Automate only after repetition demonstrates real value.

```text
repeated command
→ alias/snippet/preset

repeated multi-step workflow
→ skill candidate
```

Do not turn every one-off workflow into a permanent skill repository entry.

---

## 9. Progressive disclosure is a first-class context strategy

### Verified official skill-authoring principle
David's skill system uses progressive disclosure:
1. discovery loads tiny metadata;
2. matching activates `SKILL.md`;
3. references/scripts load only when required.

### Durable principle — ACCEPTED
Training and policy should behave the same way.

We should not stuff all learned engineering knowledge into every context window. Store a durable graph and resolve only the subgraph relevant to the current task.

This directly reduces:
- context dilution;
- stale instructions;
- contradictory policies;
- token waste;
- accidental over-application of niche rules.

---

## 10. Integration is a single-writer critical section

### Source idea
David describes a push lock for environments with many parallel agents: one OS-level lock across merge, verify, push, CI, deploy and health check.

### Durable principle — ACCEPTED
Parallel implementation is fine. Parallel final integration is dangerous.

Model the integration sequence as a lock-protected critical section:

```text
reconcile
→ merge
→ validate
→ push
→ CI
→ deploy (if applicable)
→ health check
→ release lock
```

No worker races integration while another integration is in progress.

---

## 11. Guardrails must sit before tools

### Source idea
Global pre-tool guardrails prevent catastrophic disk deletion, Git-history overwrite, password-manager access and other destructive operations.

### Durable principle — ACCEPTED
Safety controls should intercept actions **before** side effects, not merely audit after.

Candidate deny/escalate categories:
- destructive filesystem operations outside scoped workspace;
- forced Git-history rewrite without explicit authorization;
- credential/password-manager scraping;
- uncontrolled production writes;
- secret exfiltration;
- deployment/infrastructure mutation outside current contract.

### Explicit rejection
The article's enthusiasm for YOLO harness modes is **not** adopted as a universal permission model. Permissions are risk-based.

---

## 12. Persistent/cloud agents: provider-neutral lesson

### Source idea
Local-only multi-agent execution does not scale indefinitely; long runs benefit from isolated durable environments. David recommends a self-host VPS + SSH + Herdr to reduce vendor lock-in.

### Durable principle — PROVISIONAL/PORTABLE
Long/parallel jobs may deserve remote persistent execution when local resource contention or session fragility becomes a measured bottleneck.

What we adopt:
- durable session state;
- isolated environments;
- reconnectability;
- reproducible bootstrap;
- provider portability;
- secrets scoped to environment.

What we do not canonize:
- Hostinger;
- any specific VPS size;
- Herdr as mandatory runtime.

---

## 13. Scheduling and heartbeats

### Official `agent-self-scheduling` findings
- distinguish built-in scheduler vs externally owned clock;
- one-shot runs are amnesiac unless resumed/persisted;
- prefer machine-readable output;
- event-driven notification is preferable to polling where available;
- one fast heartbeat can gate many slower checks by `last_run` state;
- stay silent when nothing is due;
- verify at least one real firing before claiming success.

### Durable principle — ACCEPTED
A heartbeat is a cheap scheduler/gate, not an excuse to invoke an LLM constantly.

Never put expensive reasoning on a tight timer without evidence that it is needed.

---

## 14. Handoffs preserve irrecoverable context, not copies

### Official `handoff` principles
1. state, not instructions;
2. reference, don't duplicate;
3. capture the why and dead ends;
4. verify claims against reality;
5. redact secrets;
6. ruthless compactness.

### Durable principle — ACCEPTED
A fresh agent should recover state by following pointers to canonical artifacts, not by reading a giant stale conversation dump.

Highest-value handoff content:
- current state;
- key decisions + why;
- failed/rejected approaches;
- blockers/dependencies;
- exact file/PR/issue pointers.

---

## 15. Tests: right-size, don't maximize count

### Source idea
David observes that coding agents tend to generate excessive unit/integration/database tests even where they add little value.

### Durable principle — ADAPTED
Do not follow the literal heuristic “tell the model not to add tests.” Instead require the smallest test set that protects real behavior and risk.

Prefer:
- cheap unit tests for local deterministic logic;
- contract/integration tests for wiring and boundaries;
- reality probes when passing unit tests could hide dead production paths;
- regression test for every expensive bug class worth preventing.

Reject vanity coverage/test-count targets unless they map to a real quality objective.

---

## 16. Read-only production data for reality checks

### Source idea
No production access prevents agents from checking whether assumptions match reality; write access creates unacceptable irreversible risk.

### Durable principle — ACCEPTED AS DEFAULT
When production data access exists, use read-only credentials/roles by default.

Production mutation must be a separately authorized workflow.

This supports:
- actual feature usage checks;
- real schema/data-shape verification;
- bug reproduction;
- hypothesis falsification;
without giving general agents mutation capability.

---

## 17. ADRs capture why, not code-visible what

### Source idea
Core architectural decisions deserve short ADRs because future agents can read code to see what exists but not necessarily why alternatives were rejected.

### Durable principle — ACCEPTED WITH MINIMALISM
Create ADRs only for durable decisions with non-obvious rationale. Include decision, context, alternatives and why.

Do not create ADR bureaucracy for routine implementation.

---

## 18. Model/harness selection must be empirical and volatile

### Source idea
David assigns different models to planning, bugs, frontend and default work, and recommends dedicating time to personally testing new major models instead of trusting social-media opinion.

### Durable principle — ACCEPTED
Model routing priors should come from our own task-level evidence.

### Volatile data — DO NOT CANONIZE
Specific claims about:
- Fable 5;
- GPT-5.6 Sol;
- Grok 4.6/4.7;
- Kimi K3;
- OpenCode Go;
- Cursor/Claude/OpenAI plan prices and limits;
- API-vs-subscription economics;
are Q3-2026 observations/opinions and must carry timestamps/TTL.

Re-benchmark when conditions materially change.

This integrates naturally with `HB-HYP-001 Ensemble Cognitive Processing`.

---

## 19. Pre-sending / queued intentions

### Source idea
David queues predictable next messages to reduce idle time.

### Durable principle — ADAPTED
The manager may queue likely successor actions, but each successor must re-read predecessor result/state before executing.

A queued intention is not permission to operate on stale assumptions.

---

## 20. Productivity is multi-dimensional

### Source idea
David's `agentic-productivity` combines commits, agent sessions and user prompts because each alone is a bad metric.

### Durable principle — ACCEPTED, EXTENDED
Do not optimize for raw commits, tokens, agent count or prompts.

Preferred future metrics:
- accepted PR/change throughput;
- lead time to verified outcome;
- rework rate;
- defects escaped;
- reviewer false-positive rate;
- agent blocked time;
- manager integration time;
- compute/cost per accepted outcome;
- human intervention per successful task;
- fraction of autonomous work that survives review unchanged.

---

## 21. Voice/input speed is an operator optimization, not architecture

Dictation can increase prompt throughput for some users, but it does not change the correctness model of the engineering system. Treat as optional operator-interface optimization.

---

## 22. Decision matrix

### ACCEPTED
- explicit worker state tracking;
- priority-aware manager scheduling;
- manager/worker separation;
- selective subagent delegation;
- parallel isolation;
- human control of material taste/architecture decisions;
- goal contracts with verifiable stop conditions;
- anti-reward-hacking clauses;
- heterogeneous independent review when material;
- dedupe/triage of review findings;
- no recursive issue-mining reviews;
- progressive disclosure;
- repeated workflow → automation after proven repetition;
- single-writer integration/push lock;
- pre-tool destructive-operation guardrails;
- event-driven/gated heartbeats;
- state-centric handoffs;
- read-only production access by default;
- ADRs for durable non-obvious decisions;
- empirical model evaluation;
- productivity measurement beyond raw activity.

### ADAPTED
- worktrees: threshold-triggered, not universal;
- ask-then-build: only for material unresolved decisions, not routine clarification;
- tests: right-sized by risk, not “don't test”;
- cloud agents: provider-neutral durable execution only when bottleneck justifies it;
- pre-sending: queued intent must revalidate state.

### REJECTED AS GLOBAL RULE
- always YOLO / always bypass permissions;
- automatically trust reviewer findings;
- recursively review until no new issues can be invented;
- auto-merge/push every agent output;
- unrestricted production write access;
- always use worktrees even for trivial work;
- install every available skill.

### VOLATILE SNAPSHOT
- model rankings;
- subscription prices/limits;
- specific vendor recommendations;
- exact “best model for task X” mappings.

---

## 23. Effect on our protocol

The strongest change is conceptual:

```text
single smart agent
        ↓
managed cognitive workforce
        ↓
state + priority + isolation + routing + evidence + integration lock
```

But we explicitly preserve our anti-overengineering rule:

> Add the control-plane mechanism only when current concurrency/risk demonstrates the need.

Human-Brain remains pre-kernel. This training changes **how we develop it**, not the scientific architecture by fiat.
