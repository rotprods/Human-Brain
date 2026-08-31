# Human-Brain — GOAL

Build from zero in Rust a measurable cognitive runtime that discovers the minimum computational mechanisms needed to outperform simpler baselines on persistent memory, associative recall, contextual reconstruction, generalization, replay-driven improvement, selective forgetting, adaptive reasoning and planning.

## Success is behavioral, not anatomical

A mechanism earns a place only if it produces a measurable capability improvement against a simpler baseline at acceptable cost, latency and complexity.

## Current high-value hypotheses

1. Brain-inspired memory/learning mechanisms can improve long-horizon cognition beyond KV/vector/naive graph baselines.
2. Heterogeneous LLMs can act as interchangeable cognitive processors if routing allocates compute adaptively instead of calling the strongest or all models every time.
3. Fast/deep processing may be engineered as adaptive compute modes (single fast model, cascade, speculative verifier, parallel ensemble, adversarial/debate) without claiming literal equivalence to human System 1/System 2.
4. Rust is the leading implementation candidate for the production runtime, but architecture details remain experimental until measured.

## Hard constraints

- CLEAN-ROOM FIRST.
- RUST FIRST for production core.
- Existing repos are evidence, never architecture authority.
- No complexity without measured need.
- No biological name without a computational claim.
- No architecture freeze before baselines and experiments.
- High traceability, low coupling.

## Initial measurable target

On controlled synthetic sequence/memory tasks, compare simple baselines with candidate brain-inspired mechanisms and measure recall, partial-cue reconstruction, interference, false associations, generalization, replay benefit, retention, cost, latency and reproducibility.

## Non-goals for the first stage

- whole-brain simulation;
- millions of simulated neurons;
- GPU/distributed infrastructure;
- fixed anatomical crate hierarchy;
- mandatory universal graph store;
- always-on multi-agent/model swarms;
- claiming human-equivalent cognition or consciousness.
