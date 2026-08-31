# Agentic Development Training

This directory is the durable training layer for how agents work on Human-Brain and related engineering projects.

It is **not** a giant prompt to preload into every session.

## Learning model

```text
RAW TRAINING
→ SOURCE VERIFICATION
→ DISTILL PRINCIPLES
→ ACCEPT / ADAPT / REJECT / DEFER / MARK VOLATILE
→ CONNECT USEFUL GRAPH EDGES
→ UPDATE OPERATING PROTOCOL
→ APPLY TO REAL WORK
→ MEASURE OUTCOMES
→ REVISE
```

Training material does not become policy merely because it comes from a highly productive engineer, a popular repository, a vendor, or a previous Human-Brain decision.

## Status classes

- `ACCEPTED` — strong principle adopted into current protocol.
- `PROVISIONAL` — promising, but requires project evidence or experimentation.
- `ADAPTED` — useful idea changed to fit our constraints.
- `REJECTED` — explicitly not adopted.
- `DEFERRED` — potentially useful later, no present need.
- `VOLATILE` — time-sensitive facts such as model rankings, subscriptions, prices and limits.

## Progressive disclosure

Default context should contain only the small operating contract in `AGENTS.md`.

When a task matches a training topic:
1. resolve the relevant node in `TRAINING.graph.yaml`;
2. open the referenced training module;
3. load external source/reference only if needed;
4. execute;
5. persist any material policy change.

## Modules

- `T001-DAVID-ONDREJ-Q3-2026.md` — David Ondrej agentic engineering setup and verified skills, interpreted as principles rather than dogma.
- `OPERATING_PROTOCOL.md` — current cross-module protocol produced from accepted/adapted learning.
- `TRAINING.graph.yaml` — useful semantic graph of principles, risks, tools, workflows and sources.
- `ARTIFACT_REGISTRY.yaml` — logical cross-store aliases once external persistence targets exist.

## Rule

Training should make the engineering system **simpler, faster, safer and more correct**. If a training rule increases ceremony without measurable benefit, downgrade or remove it.
