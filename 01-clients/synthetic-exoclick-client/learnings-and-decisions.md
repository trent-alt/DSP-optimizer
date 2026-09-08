# Synthetic ExoClick Client — Learnings & Decisions

## Purpose

Persistent memory for durable lessons, client preferences, system mistakes, and decisions that future analytics/optimization agents must respect.

## Current durable decisions

### 1. Client context is mandatory

- Decision: Campaign analysis should not run as a generic DSP analysis when client requirements are available.
- Reason: The same KPI result can imply different actions depending on target CAC, pacing, budget, and scale tolerance.
- Status: Active rule.

### 2. Materiality must be explicit

- Decision: High ROAS, low CAC, or high CVR on negligible spend is not enough to call a segment a winner.
- Reason: Prior real-world experience showed LLMs can hyper-focus on tiny pockets that will not move total performance.
- Status: Active Golden Rule.

### 3. Analyze before optimizing

- Decision: Separate campaign analysis from optimization recommendations.
- Reason: The system should first explain what is happening, then diagnose, then act.
- Status: Active architecture choice.

### 4. Narrow fixes before broad exclusions

- Decision: Check lower-level interactions before blocking a whole publisher/zone/campaign.
- Reason: Aggregate underperformance may hide a valuable sub-segment.
- Status: Active optimization principle.

### 5. Do not force spend

- Decision: The synthetic $10K test does not have to be spent continuously or by a fixed date.
- Reason: Pausing after meaningful data accumulation to analyze and adjust can increase learning efficiency.
- Status: Active client requirement.

### 6. Recommendation-only mode

- Decision: Initial validation should not automatically execute changes.
- Reason: The goal is to validate reasoning quality before granting action authority.
- Status: Active guardrail.

### 7. Ground-truth testing over subjective evaluation

- Decision: Synthetic data should contain intentionally planted truths and decoys.
- Reason: We need to score whether the model uncovers known patterns and ignores misleading noise.
- Status: Active evaluation principle.

## Known system failure modes to watch

- Overweighting extreme metrics on trivial spend.
- Recommending a campaign-wide action when the problem is isolated to a narrower cluster.
- Ignoring pacing because CAC is acceptable.
- Ignoring CAC because spend is behind pace.
- Treating correlation as causation.
- Comparing unlike segments to an inappropriate blended average.
- Recommending more budget to a small segment without evidence it can absorb scale.
- Repeating a prior rejected or failed recommendation because client memory was not loaded.
- Producing generic "optimize bids / test creative" language without specifying where, why, confidence, and expected impact.

## Learning-entry template

```
LEARNING ID:
Date:
Source run:
Observation:
Evidence threshold met?:
Why durable:
Applies to: Universal / Client only
Decision impact:
Confidence:
Supersedes prior learning?:
```

## Decision-entry template

```
DECISION ID:
Date:
Decision:
Reason:
Owner/approver:
Scope:
Revisit trigger:
```

## Memory hygiene rule

Persist only information that should materially change future reasoning. Temporary performance fluctuations belong in Campaign History, not durable memory.
