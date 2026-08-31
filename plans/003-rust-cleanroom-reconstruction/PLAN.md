# PLAN-003 — First-Principles Minimal Rust Research Program

Status: CANONICAL NEXT PLAN CANDIDATE
Owner: Human-Brain
Primary implementation language: Rust
Branch: `plan/003-rust-cleanroom-architecture`

## 1. Mission

Reconstruct `Human-Brain` from zero in Rust by discovering the **minimum set of computational mechanisms** required to obtain useful brain-like cognitive properties.

The project does not start by reproducing brain anatomy, by porting previous repositories, or by pre-selecting a sophisticated software architecture.

The operating loop is:

```text
QUESTION
→ HYPOTHESIS
→ MINIMAL MODEL
→ EXPERIMENT
→ MEASURE
→ KEEP / KILL
→ NEXT NECESSARY COMPLEXITY
```

The optimization target is:

```text
maximum useful cognitive capability
──────────────────────────────────
minimum necessary system complexity
```

## 2. Primary research question

> What is the smallest scientifically defensible set of computational mechanisms whose combination materially improves continuous learning, associative recall, contextual memory, generalization, replay, adaptive forgetting and planning over simpler baselines?

This question outranks every previously proposed architecture.

## 3. Hard independence rule

Existing `rotprods` repositories, external frameworks, previous Human-Brain diagrams and earlier architectural proposals are **non-authoritative**.

They may later provide:
- lessons;
- anti-patterns;
- benchmark ideas;
- tests;
- algorithms worth independently reimplementing;
- interoperability requirements.

They may not determine:
- module boundaries;
- scheduler design;
- graph representation;
- memory representation;
- concurrency model;
- persistence model;
- scientific abstractions;
- crate structure.

Decision order:

1. project goal;
2. scientific evidence;
3. explicit invariants;
4. simplest viable mechanism;
5. experiment;
6. measurement;
7. only then comparison with existing code or frameworks.

Legacy code is evidence, not authority.

## 4. Nothing architectural is canon yet

The following remain hypotheses, not commitments:

| Candidate | Status |
|---|---|
| Rust as production core | HIGH-CONFIDENCE HYPOTHESIS |
| deterministic scientific runtime | HYPOTHESIS |
| separate Simulation / Agency planes | HYPOTHESIS |
| ECS | UNDECIDED |
| custom SoA | UNDECIDED |
| CSR/CSC neural topology | UNDECIDED |
| event sourcing | UNDECIDED |
| temporal property graph | UNDECIDED |
| actor model | UNDECIDED |
| fixed timestep | UNDECIDED |
| discrete-event simulation | UNDECIDED |
| hybrid multirate scheduler | UNDECIDED |
| GPU | DEFERRED |
| distributed runtime | DEFERRED |
| adaptive fidelity / LOD | DEFERRED |
| glial simulation | DEFERRED |
| full anatomical decomposition | DEFERRED |

No item moves to `ACCEPTED` without a demonstrated need or experiment.

## 5. Science does not dictate software boundaries

A biological structure is not automatically a crate, service, class or process.

For every brain mechanism we first ask:

```text
What computation appears to be occurring?
What observable property does it produce?
What is the smallest model capable of reproducing that property?
```

Example:

`hippocampal pattern separation` may initially require only a sparse encoding mechanism and an experiment demonstrating reduced interference between similar episodes.

It does **not** justify a large `hippocampus/` subsystem by itself.

## 6. Complexity budget

Every new abstraction must answer all seven questions:

1. What observed problem does it solve?
2. Why can the current system not solve that problem?
3. What is the simpler alternative?
4. What evidence favors this option?
5. What complexity does it add?
6. Can it be removed or replaced later?
7. How will we measure whether it was worth adding?

If these cannot be answered:

```text
DO NOT ADD IT
```

This applies equally to graphs, schedulers, services, crates, databases, agents, CI gates and neuroscience-inspired mechanisms.

## 7. Initial repository scope

Do not bootstrap a large architecture.

Initial production workspace target:

```text
crates/
├── hb-core/
└── hb-experiments/
```

Additional crates exist only after a real ownership or dependency boundary appears.

Initial candidate primitives are deliberately small:

```text
Entity
Relation
Event
Activation
Memory
```

plus `Clock` and deterministic `RNG` if an experiment requires them.

Even these primitives are replaceable.

## 8. First experimental system

Build a tiny synthetic world before attempting anatomical brain simulation.

The system observes partially overlapping sequences such as:

```text
A → B → C
A → B → D
X → B → C
A → Y → C
```

Evaluate whether a candidate mechanism can:

1. encode individual episodes;
2. reconstruct missing elements;
3. distinguish highly similar episodes;
4. strengthen useful associations;
5. generalize recurring structure;
6. resist irrelevant noise;
7. forget selectively;
8. replay previous experiences offline;
9. improve after replay rather than merely repeat stored data.

## 9. Required baselines

No brain-inspired mechanism is considered useful without beating appropriate simpler baselines.

Minimum comparison:

```text
B0 — key/value episodic store
B1 — similarity/vector retrieval
B2 — simple associative graph
B3 — candidate brain-inspired mechanism
```

Metrics must include where applicable:
- exact recall;
- partial-cue recall;
- interference;
- false association rate;
- generalization accuracy;
- retention after noise;
- improvement after replay;
- memory cost;
- compute cost;
- latency;
- determinism/reproducibility.

If B3 does not materially beat simpler baselines on its claimed property, the mechanism is rejected or redesigned.

## 10. Mechanisms enter one at a time

Candidate sequence, subject to experimental results:

```text
association
→ sparse activation / competition
→ plasticity
→ episodic linking
→ replay
→ consolidation
→ adaptive forgetting
→ working state
→ prediction error
→ action selection
```

A later mechanism is not implemented simply because it appears in the brain.

It enters only when the current system exhibits a measurable limitation that the mechanism plausibly addresses.

## 11. Scientific evidence contract

For every biologically inspired mechanism record only what is necessary:

```text
claim
source
confidence / uncertainty
software abstraction
assumptions
predicted behavior
experiment
result
```

Classification:

```text
DIRECT_MODEL
CONSTRAINED_ANALOGY
FUNCTIONAL_ANALOGY
ENGINEERING_ABSTRACTION
EXPERIMENTAL
```

No biological terminology is allowed to imply equivalence by naming alone.

## 12. Determinism policy

Determinism is currently a strong candidate requirement because it enables:
- reproducible experiments;
- causal debugging;
- regression testing;
- reliable comparison between models.

But we do not pre-commit to one scheduler architecture.

We first define the invariant:

```text
same model + same seed + same input trace
→ same scientifically relevant result
```

Then compare the simplest scheduling designs capable of satisfying it.

## 13. Architecture spikes are disposable

When a decision cannot be made cheaply from reasoning, build the smallest benchmark or prototype that answers the question.

Examples only when needed:
- AoS vs SoA;
- custom store vs ECS;
- adjacency list vs CSR;
- fixed-step vs event-driven;
- snapshot-only vs selective event log;
- single-thread vs deterministic parallel reduction.

Spikes are not production code by default.

A successful spike yields a decision and test evidence, not an obligation to preserve its implementation.

## 14. Repository archaeology is demand-driven

Do **not** deeply analyze all ~100 repositories before building the minimal model.

Inspect existing repositories only when a concrete question exists.

Examples:

```text
Question: how should replay persistence work?
→ inspect relevant internal/external persistence implementations.

Question: how should deterministic scheduling scale?
→ inspect simulation engines and relevant Rust runtimes.
```

This prevents archaeology paralysis and anchoring.

A broad automated ecosystem scan may be useful later, but it is not a prerequisite for the first scientific experiments.

## 15. Minimal governance

Initial durable project control requires only:

```text
GOAL.md
STATE.md
PLAN.md / plans/
DECISIONS.md
Git history + PRs
```

Do not create seven ledgers, seven graphs or dozens of CI gates before they solve an observed coordination problem.

The four review perspectives remain mandatory conceptually:

```text
/code-review
/security-review
/QA-review
/questions-review
```

Initially they are review protocols, not separate software systems.

## 16. Traceability without coupling

Canonical principle:

> Everything important must be traceable; not everything should be connected or coupled.

Use a graph only when a relationship enables a useful query, validation, impact analysis or decision.

Do not graph data merely because it can be represented as nodes and edges.

Target:

```text
high traceability
low coupling
```

## 17. Stop / kill rules

Stop a line of implementation when:
- it does not beat the relevant baseline;
- its claimed property cannot be measured;
- complexity grows faster than demonstrated capability;
- a simpler mechanism produces equivalent behavior;
- reproducibility becomes impossible without a justified reason;
- biological naming is doing more work than the algorithm;
- infrastructure is being built for hypothetical future scale rather than current experiments.

Rejected work remains research evidence, not failure to be hidden.

## 18. Phase sequence

### Phase A — preserve the science
Persist the advanced neuroscience investigation as evidence/research without translating every finding into architecture.

### Phase B — minimal Rust harness
Create the smallest Rust experiment harness capable of deterministic seeded runs and quantitative metrics.

### Phase C — baselines
Implement B0/B1/B2 as small reference baselines.

### Phase D — first mechanism
Implement one candidate associative/plastic memory mechanism.

### Phase E — falsification
Run the benchmark suite and decide KEEP / KILL / REDESIGN.

### Phase F — next bottleneck
Observe the strongest remaining failure and only then select the next biological/computational mechanism to investigate.

Repeat Phases D–F.

## 19. Immediate next actions

1. Keep this PR draft until review completes.
2. Persist the advanced neuroscience research corpus separately without declaring architecture from it.
3. Define a one-page `GOAL.md` with measurable cognitive properties.
4. Define the first experiment and metric suite before creating a large crate hierarchy.
5. Create only `hb-core` and `hb-experiments` when code begins.
6. Implement B0/B1/B2.
7. Implement one minimal candidate brain-inspired associative memory.
8. Benchmark.
9. Keep, kill or redesign based on results.
10. Add the next piece of complexity only when an observed limitation justifies it.

## 20. Canonical invariants

```text
NO COMPLEXITY WITHOUT A MEASURED NEED
NO BIOLOGICAL NAME WITHOUT A COMPUTATIONAL CLAIM
NO CLAIM WITHOUT A TESTABLE PREDICTION
NO NEW ABSTRACTION WITHOUT A SIMPLER ALTERNATIVE CONSIDERED
NO LEGACY ARCHITECTURE BY INHERITANCE
NO REPO ARCHAEOLOGY WITHOUT A QUESTION
NO SCALE INFRASTRUCTURE BEFORE SCALE EVIDENCE
NO ARCHITECTURE FREEZE BEFORE BASELINES
NO FEATURE WITHOUT MEASUREMENT
```

And above all:

```text
BUILD THE SMALLEST THING THAT CAN PROVE OR DISPROVE THE NEXT IMPORTANT IDEA.
```
