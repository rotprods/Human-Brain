# Human-Brain — STATE

Status: PRE-KERNEL / RESEARCH PROGRAM
Active branch: `plan/003-rust-cleanroom-architecture`
Active draft PR: #1

## Verified facts

- `rotprods/Human-Brain` began essentially empty and is still pre-production-kernel.
- `rotprods/ecp-framework` exists as a private repository but is currently an empty Git repository: no commits and no branches were found.
- No prior canonical definition of `ECP` was recovered from available project context.
- `Ensemble Cognitive Processing` is therefore a new architecture hypothesis, not legacy canon.
- `/gauntlet-loop` is not an identified standard package. Human-Brain defines it as a real outer verification/remediation loop inspired by documented Ralph-loop semantics and internal ROTCLAW gauntlet evidence.

## Persisted control artifacts

- `GOAL.md`
- `plans/001-scientific-foundation/PLAN.md`
- `plans/002-gauntlet-loop-development/PLAN.md`
- `plans/003-rust-cleanroom-reconstruction/PLAN.md`
- `plans/README.md`
- `research/architecture-hypotheses/HB-HYP-001-ensemble-cognitive-processing.md`
- `graph/PROGRAM.graph.yaml`

## Current architecture posture

Accepted principles:
- clean-room first;
- Rust first for production core;
- measurable behavior over anatomical mimicry;
- no complexity without measured need;
- existing repositories are evidence, never authority;
- high traceability, low coupling.

Active hypotheses:
- deterministic seeded experiments;
- brain-inspired memory mechanisms can beat simple baselines;
- adaptive heterogeneous LLM routing can improve quality/cost/latency;
- fast/deep execution modes can emerge from adaptive compute policies;
- heterogeneous independent reviewers can improve gauntlet quality when justified.

Not accepted as canon:
- ECS;
- CSR/CSC;
- universal graph store;
- event sourcing;
- two-plane runtime;
- distributed execution;
- GPU;
- always-on model swarms;
- full anatomical decomposition.

## Next experimental work

1. Reconstruct the research subset needed for EXP-001.
2. Specify EXP-001 dataset, metrics and failure thresholds.
3. Implement B0/B1/B2 baselines in the smallest possible Rust harness.
4. Implement one candidate associative/plastic mechanism.
5. KEEP/KILL based on results.
6. Separately define EXP-ECP-001 comparing fixed, cascade, speculative and ensemble model routing.
7. Run meaningful implementation PRs through PLAN-002 `/gauntlet-loop`.

## Current blockers

- no Rust workspace yet;
- no executable experiment harness yet;
- advanced neuroscience corpus not yet persisted in full;
- no measured routing telemetry yet;
- no ECP implementation decision yet.
