# HB-HYP-001 — Ensemble Cognitive Processing (ECP)

Status: PROPOSED / NOT ARCHITECTURE CANON

## Important provenance note

`rotprods/ecp-framework` is currently an empty private Git repository: no commits and no branches were found. No prior canonical expansion of the acronym was recovered. Therefore **Ensemble Cognitive Processing** is a new proposed meaning, not a recovered definition.

## Hypothesis

A cognitive runtime can improve quality/cost/latency trade-offs by treating heterogeneous LLMs as dynamically allocated cognitive processors rather than binding cognition to one model or invoking many models on every task.

This is an engineering analogy to fast/deep thought, not a claim that LLM routing reproduces literal human System 1/System 2 neurobiology.

## Core pipeline

```text
CognitiveRequest
  ↓
TaskProfiler
  ↓
HardConstraintFilter
  ↓
Model/Execution Candidate Set
  ↓
Multi-dimensional scoring
  ↓
ExecutionPattern selection
  ↓
Run
  ↓
Verifier/Evidence
  ↓
Outcome telemetry
  ↓
Update routing priors
```

## CognitiveRequest features

At minimum:
- task/domain;
- expected output type;
- modality;
- privacy/local-only constraint;
- tool requirements;
- context size;
- latency budget;
- cost budget;
- task stakes/risk;
- uncertainty estimate;
- need for diversity/independent verification.

## ModelProfile

Static and live fields should be separated.

Static candidates:
- provider and model identity;
- local/cloud;
- modality/tool support;
- context limits;
- reasoning controls;
- privacy characteristics;
- known specialization;
- input/output price when applicable.

Live candidates:
- availability;
- warm/cold state;
- queue/concurrency pressure;
- p50/p95 latency;
- recent error rate;
- rate-limit state;
- observed task-quality calibration;
- recent cost;
- health/cooldown state.

## Routing: constraints before score

Never reduce everything to a single score before checking hard requirements.

First eliminate models that violate privacy, modality, context, tool, availability or hard budget requirements.

Then evaluate surviving candidates with a score vector such as:

```text
expected_quality_gain
capability_match
historical_calibration
reliability
latency
cost/price
privacy/locality
context_fit
tool_fit
diversity_value
```

A scalar utility may be used only as a final policy decision, e.g. conceptually:

```text
U = expected_quality
    - λ_cost * expected_cost
    - λ_latency * expected_latency
    - λ_risk * failure_risk
    + λ_privacy * locality_value
    + λ_diversity * independence_value
```

Weights depend on the request policy, not global aesthetics.

## Key routing principle: marginal gain

A stronger/slower/costlier model should be invoked when its **expected marginal quality gain** justifies the added cost/latency/risk.

This matches the direction of learned LLM routing research better than static model tiers.

## Candidate thought modes

These are execution policies, not permanent modules.

### REFLEX
One fast/local/cheap processor when confidence and task risk permit.

### FAST
Fast primary + lightweight verifier or fallback.

### DELIBERATE
2–4 independent heterogeneous processors, then structured synthesis.

### DEEP
Cheap models generate candidate reasoning/plans; stronger models verify/correct promising candidates; tools/tests provide external evidence.

### CRITICAL
Independent multi-provider reasoning + adversarial reviewers + evidence/tool validation + explicit uncertainty. Reserved for high-stakes or high-uncertainty tasks.

## Execution patterns

Router chooses among:
- single model;
- fallback chain;
- cascade/escalation;
- speculative draft → strong verifier;
- parallel best-of-N;
- heterogeneous ensemble;
- debate/critique;
- specialist → judge;
- tool/test-driven verification.

Do not assume majority vote is sufficient.

## Anti-groupthink protocol

For expensive ensemble modes:
1. independent first-pass outputs without seeing peers;
2. extract claims/solutions/uncertainties;
3. cross-critique only after independence exists;
4. external evidence/tests when possible;
5. synthesize with provenance;
6. retain disagreement/uncertainty instead of forcing false consensus.

## Confidence policy

Do not trust model self-confidence as the primary signal.

Prefer:
- historical calibration by task type;
- agreement/disagreement structure;
- verifier score;
- deterministic test results;
- tool/evidence consistency;
- human feedback when present;
- regression outcomes.

## Learning router

Version 0 should be understandable and heuristic.

Every routed run records:
- request features;
- candidates;
- chosen execution graph;
- outputs/structured verdicts;
- quality evidence;
- latency;
- token/cost usage;
- failures;
- final accepted result.

Later routing can become a contextual bandit/learned policy only after sufficient real data exists.

## Hooks / agentic hardness

Potential hooks:
- `pre_route` — normalize request and hard constraints;
- `post_route` — inspect selected execution graph;
- `pre_model` / `post_model` — budgets, provenance, output contracts;
- `pre_tool` / `post_tool` — permissions and evidence capture;
- `pre_synthesis` — preserve independent outputs;
- `post_synthesis` — check unsupported collapse of disagreement;
- `pre_commit` — development policy;
- `post_test` — update evidence;
- `pre_gauntlet` / `post_gauntlet` — reviewer selection and final stop reason.

Hooks may observe, enrich, deny or require escalation, but hidden side effects are forbidden.

## Rust boundary

The cognitive router should be ours.

Multi-provider libraries/gateways such as Rust `genai`, LiteLLM concepts, Ollama adapters or OpenAI-compatible transports may sit below a provider trait, but none determines ECP policy.

Candidate minimal Rust interfaces:

```rust
trait ModelProvider { /* transport + normalized capabilities */ }
trait RoutingPolicy { /* request -> execution plan */ }
trait Verifier { /* evidence -> calibrated outcome */ }
```

No larger type hierarchy is justified yet.

## Evidence that motivates experiments

- RouteLLM: learned strong-vs-weak routing can reduce cost while preserving quality.
- LLMRouter (2026): routing can be modeled as a sequential decision process with encoders, scores, decisions and learning signals.
- FrugalGPT: cascades can materially change quality/cost trade-offs.
- Mixture-of-Agents: heterogeneous parallel agents can improve some benchmark outcomes.
- SpecReason: lightweight speculative reasoning plus stronger verification can accelerate reasoning while preserving/improving results.
- Multi-agent debate work shows potential benefits but also demonstrates that aggregation strategy and stopping matter.

## Falsification criteria

ECP is rejected or simplified if experiments show that:
- one fixed model dominates under realistic budgets;
- routing overhead exceeds quality/cost benefit;
- parallel agents mostly add correlated noise;
- verifier/judge errors dominate ensemble gains;
- adaptive escalation cannot be calibrated reliably.

## Relationship to plans

- `PLAN-001 --EVIDENCE_FEEDS--> HB-HYP-001`
- `PLAN-003 --EXPERIMENTS_ON--> HB-HYP-001`
- `PLAN-002 --MAY_USE--> HB-HYP-001` for heterogeneous gauntlet reviewers
- `HB-HYP-001 --MUST_NOT_PREEMPT--> minimal memory experiments`
