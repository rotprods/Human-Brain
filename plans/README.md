# Human-Brain Plans

The current plan system is intentionally small. Plans are coupled only where a real dependency exists.

## Active plan graph

```text
PLAN-001 Scientific Foundation
        │ evidence
        ▼
PLAN-003 First-Principles Minimal Rust Research
        │ implementation/change
        ▼
PLAN-002 /gauntlet-loop Development Protocol
        │ verified evidence
        └──────────────► feeds back into PLAN-001 / PLAN-003
```

`HB-HYP-001 Ensemble Cognitive Processing` is **not** a fourth plan. It is an architecture hypothesis evaluated under PLAN-003 and may be used by PLAN-002 for heterogeneous reviewers only when justified.

## PLAN-001

Question: What scientifically defensible mechanisms/behaviors are relevant to the current experiment?

Output: evidence and falsifiable computational claims.

## PLAN-002

Question: Is the current change actually correct, safe, tested and complete?

Output: verified or explicitly unverified PR state through `/gauntlet-loop`.

## PLAN-003

Question: What is the smallest Rust mechanism that can prove or disprove the next important cognitive hypothesis?

Output: baselines, experiments, KEEP/KILL decisions and only necessary new complexity.

## Cross-plan invariants

- PLAN-001 cannot force software boundaries.
- PLAN-002 cannot turn every review into mandatory expensive multi-model work.
- PLAN-003 cannot bypass evidence or verification because an experiment is exploratory.
- Architecture hypotheses never silently become plans/canon.
- Existing repos can inform decisions only after the question is explicit.

## Current next sequence

1. Preserve/reconstruct the science relevant to EXP-001.
2. Define EXP-001 metrics and B0/B1/B2 baselines.
3. Build the minimal Rust harness.
4. Test one candidate mechanism.
5. Run `/gauntlet-loop` on meaningful implementation PRs.
6. Evaluate `HB-HYP-001` separately: fixed model vs cascade vs speculative vs parallel/ensemble routing.
