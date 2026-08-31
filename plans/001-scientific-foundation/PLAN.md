# PLAN-001 — Scientific Foundation

Status: ACTIVE SUPPORT PLAN

## Purpose

Preserve and operationalize the advanced neuroscience/cognitive-science research without forcing research findings into software architecture prematurely.

## Rule

Science answers: **what mechanism or behavior may exist, under what evidence and uncertainty?**
Architecture separately answers: **what is the smallest computational model worth testing?**

## Outputs

For each relevant mechanism record only:

- claim;
- primary/strong source;
- confidence/uncertainty;
- competing interpretation where relevant;
- computational property hypothesized;
- minimum falsifiable experiment;
- result once implemented.

## Priority domains

1. associative and episodic memory;
2. pattern separation/completion;
3. replay and consolidation;
4. forgetting/interference/reconsolidation;
5. working memory and gating;
6. attention/salience;
7. prediction error and adaptive control;
8. action selection/planning;
9. multiscale neural dynamics only when required by a behavioral gap.

## Anti-overengineering constraint

No brain region, neurotransmitter, cell type or anatomical fact automatically creates a crate/module/service.

## Relationship to other plans

- `PLAN-001 --EVIDENCE_FEEDS--> PLAN-003`
- `PLAN-001 --SCIENCE_GATES--> EXPERIMENTS`
- `PLAN-002 --VALIDATES_CHANGES_TO--> PLAN-001`

## Exit condition

The research corpus is durable and queryable enough to support current experiments, without requiring complete formalization of all neuroscience before coding begins.
