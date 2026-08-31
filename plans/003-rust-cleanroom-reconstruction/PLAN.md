# PLAN-003 — Rust Clean-Room Reconstruction & Architecture Convergence

Status: CANONICAL NEXT PLAN
Owner: Human-Brain
Primary language: Rust
Branch: plan/003-rust-cleanroom-architecture

## 1. Mission

Reconstruct `Human-Brain` from first principles in Rust as a deterministic, multiscale, evidence-bound cognitive runtime inspired by scientifically defensible mechanisms of the human brain.

This plan explicitly supersedes any interpretation that existing Roberto/rotprods repositories, prior architectures, frameworks, codebases, naming conventions, or implementation choices are authoritative inputs to the new architecture.

The project is CLEAN-ROOM FIRST and RUST FIRST.

## 2. Hard architectural independence rule

Existing repositories are treated only as an external comparison corpus.

They MAY contribute:
- lessons learned;
- anti-patterns;
- failure evidence;
- benchmarks;
- useful tests or acceptance contracts;
- independently validated algorithms;
- reusable ideas whose value survives first-principles review;
- interoperability requirements.

They MUST NOT:
- define the architecture by inheritance;
- force TypeScript/Python patterns into the Rust kernel;
- determine module boundaries;
- determine the memory model;
- determine the graph model;
- determine concurrency semantics;
- determine persistence semantics;
- determine the scheduler;
- determine scientific abstractions;
- be copied merely because they already exist.

Canonical decision order:

1. scientific evidence and explicit project goal;
2. first-principles systems reasoning;
3. measurable runtime requirements;
4. determinism, correctness, safety, performance and evolvability;
5. architecture experiments and benchmarks;
6. only then comparison against existing repositories.

Existing repos are evidence, never authority.

## 3. Clean-room decision protocol

For every major architectural decision:

1. State the problem without referencing an existing repo.
2. Derive candidate solutions from requirements and scientific constraints.
3. Define invariants.
4. Define falsifiable engineering predictions.
5. Prototype/benchmark competing candidates where needed.
6. Select the provisional best architecture.
7. Only after provisional selection, inspect existing repositories and external frameworks.
8. Classify any discovered capability as `PORT`, `ADAPT`, `WRAP`, `REFERENCE`, or `REJECT`.
9. Re-open the decision only if new evidence materially beats the clean-room candidate.
10. Persist the rationale, graph impact and tests.

This ordering is mandatory to reduce anchoring and architecture-by-legacy.

## 4. Core architecture hypothesis to test, not blindly assume

The current candidate architecture consists of two execution planes:

### Deterministic Simulation Plane

Rust-only scientific core responsible for:
- logical BrainTime;
- deterministic RNG streams;
- causal event ordering;
- multirate scheduling;
- neural/population/assembly state;
- topology;
- plasticity;
- neuromodulation;
- homeostasis;
- memory dynamics;
- replay;
- consolidation;
- snapshots;
- state hashes;
- deterministic replay;
- scientific experiments.

Hard boundary: no direct wall clock, LLM provider, network I/O, MCP, filesystem side effect, external agent, or nondeterministic async scheduling inside the scientific hot path.

### Agency / Executive Plane

Peripheral asynchronous Rust services/adapters responsible for:
- LLMs;
- MCP;
- tools;
- agents/subagents;
- external APIs;
- user/world I/O;
- model routing;
- permissions;
- budgets;
- cancellation;
- remote services.

Cross-plane communication occurs only through typed, recordable ports/events.

This two-plane model remains a hypothesis until architecture experiments validate it.

## 5. Data architecture hypothesis

Do not force all information into one universal graph store.

Use a shared identity/provenance spine with specialized physical substrates:

1. Neural Topology Store — sparse, data-oriented, cache-efficient, CSR/CSC-like structures where appropriate.
2. Component State Store — SoA/ECS-like storage for homogeneous state and high-throughput systems.
3. Temporal Cognitive Graph — typed, temporal, versioned property graph for episodes, concepts, beliefs, goals, causal relations and schemas.
4. Immutable Event Ledger — durable causal/control/cognitive events, with selective neural traces.
5. Derived Index Fabric — ANN/vector/BM25/full-text/materialized projections; never the canonical truth.

Any of these choices may be replaced if experiments demonstrate a better design.

## 6. Scientific architecture constraint

Every biologically named component must carry an explicit abstraction class:

- `DIRECT_MODEL`
- `CONSTRAINED_ANALOGY`
- `FUNCTIONAL_ANALOGY`
- `ENGINEERING_ABSTRACTION`
- `EXPERIMENTAL`

Every such model must link:
- scientific evidence;
- assumptions;
- parameters and provenance;
- falsifiable predictions;
- validation experiment;
- known limitations.

No biological label is accepted as proof of biological equivalence.

## 7. Mechanism-first architecture

Software boundaries are derived from computational mechanisms rather than anatomy labels.

Example:

`HippocampalModel` may compose:
- sparse encoding;
- pattern separation;
- recurrent association;
- temporal binding;
- comparator/readout;
- replay;
- plasticity.

A brain region is a model composition, not automatically a crate, service or process.

## 8. Multiscale fidelity

Architecture must support multiple levels of detail:

- cognitive system;
- brain region / neural mass;
- population;
- assembly / engram;
- neuron;
- dendritic compartment.

The same runtime should eventually allow mixed-resolution experiments.

Adaptive refinement/coarsening is a future capability and must preserve declared invariants.

## 9. Rust-first implementation constraints

The kernel and performance-critical fabrics are written from zero in Rust.

Initial workspace should stay deliberately small until boundaries are proven:

- `hb-core`
- `hb-sim`
- `hb-graph`
- `hb-neural`
- `hb-memory`
- `hb-cognition`
- `hb-models`
- `hb-science`
- `hb-agency`
- `hb-cli`

Crates are split further only after profiling, dependency analysis and ownership boundaries justify it.

Python is allowed for research notebooks/reference experiments/data preparation.
TypeScript is allowed for visualization/operator surfaces.
Neither may define the scientific kernel architecture.

## 10. Repository archaeology role

The ecosystem scan remains valuable but is moved after clean-room candidate generation.

For each external/internal repo or framework:

- mine symbols, algorithms, tests, workflows and failures;
- identify capability;
- measure maturity;
- inspect license;
- detect dead code and architecture drift;
- extract anti-patterns;
- compare with the independently derived Rust candidate.

The result is a `REUSE.graph`, not a dependency list.

## 11. Architecture-reality rule

Executable reality outranks documentation.

Truth order:

1. reproducible runtime probe;
2. reproducible integration/scientific experiment;
3. actual execution path;
4. code and schema;
5. generated graph/state;
6. architecture docs;
7. plans;
8. comments/docstrings.

A passing unit test on unwired/dead code is not proof of implementation.

## 12. Graph × impact rule

Every decision/change becomes graph nodes and edges.

Minimum node classes:
- Goal
- Requirement
- ScientificClaim
- Source
- Hypothesis
- Model
- Mechanism
- Algorithm
- Component
- Crate
- Symbol
- Test
- Benchmark
- Experiment
- Invariant
- Risk
- Decision
- Question
- Plan
- Task
- PR

Every proposed change must compute semantic blast radius through propagation-enabled relationships.

No merge while required impacted nodes remain dirty.

## 13. Workstreams

### WS-1 — Scientific reconstruction
Re-ingest and amplify the advanced brain research; decompose into claims, mechanisms, evidence, contradictions, parameters and experiments.

### WS-2 — Clean-room architecture derivation
Derive competing kernel/runtime/data architectures from first principles without consulting legacy code during initial candidate generation.

### WS-3 — Rust architecture spikes
Build throwaway benchmarks/prototypes for scheduler, state layout, topology, event model, graph representation, snapshots and replay.

### WS-4 — Ecosystem archaeology
Only after WS-2 candidate architecture exists, contrast all relevant existing repos and frameworks.

### WS-5 — Architecture gauntlet
Run code/system/science/security/performance/questions reviews against candidate architectures.

### WS-6 — Convergence
Produce Architecture vNext, ADRs, rejected alternatives, benchmark evidence, risk graph and final BrainSpec prerequisites.

## 14. Required architecture experiments before freeze

At minimum compare/test:

- fixed-step vs event-driven vs hybrid multirate scheduler;
- ECS/SoA vs alternative data-oriented state representations;
- CSR/CSC/sparse adjacency alternatives for neural topology;
- deterministic parallel reductions;
- event ledger granularity and storage cost;
- snapshot + replay strategy;
- ID/version/causality model;
- temporal cognitive graph representations;
- graph projection/index strategy;
- mutation buffering/barrier semantics;
- deterministic RNG partitioning;
- memory retrieval/index architecture;
- regional model composition API;
- Simulation Plane ↔ Agency Plane typed boundary.

Architecture decisions should be benchmark-backed wherever performance or scale matters.

## 15. Anti-anchoring gates

A decision FAILS review if its principal justification is:
- “we already have this in repo X”;
- “COS does it this way”;
- “AMI already implements it”;
- “Tengu already has this primitive”;
- “it is easier to port”; or
- “we designed it earlier”.

Required justification must instead reference goals, invariants, evidence, experiments, complexity, performance, safety or maintainability.

## 16. Preservation rule

Previous research, architectural proposals and repository findings are not deleted.

They are retained as:
- hypotheses;
- evidence;
- historical decisions;
- candidate patterns;
- anti-patterns;
- comparison baselines.

They do not become canonical architecture until revalidated by this plan.

## 17. Exit criteria

PLAN-003 closes only when:

- advanced neuroscience research is preserved and graphified;
- clean-room Rust architecture candidates have been derived independently;
- core architecture experiments have executable results;
- relevant rotprods repos have been mined after candidate derivation;
- repository-derived ideas have explicit PORT/ADAPT/WRAP/REFERENCE/REJECT decisions;
- all P0 architecture contradictions are resolved;
- deterministic Simulation/Agency boundary is validated;
- source-of-truth ownership is explicit;
- no major component exists solely because of legacy architecture;
- Architecture vNext has evidence-backed ADRs;
- BrainSpec can be defined without depending on legacy implementation details.

## 18. Immediate next actions

1. Bootstrap repository governance and persistent plans structure.
2. Persist the complete advanced neuroscience research as PLAN-001 corpus/evidence.
3. Persist Graph×Loop governance as PLAN-002 requirements.
4. Execute this PLAN-003 clean-room derivation.
5. Generate at least 2-3 competing Rust architecture candidates.
6. Benchmark critical primitives.
7. Only then run the deep ecosystem/repository comparison pass.
8. Reconcile findings into Architecture vNext.
9. Freeze BrainSpec only after architecture gauntlet passes.
10. Begin production Rust kernel implementation afterwards.

## 19. Canonical invariant

`Human-Brain` is rebuilt from zero in Rust.

Legacy code may teach us.
Legacy code may warn us.
Legacy code may supply test ideas.
Legacy code may even contain an algorithm worth reimplementing.

Legacy code does not get a vote merely because it already exists.
