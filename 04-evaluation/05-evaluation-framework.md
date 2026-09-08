# DSP Optimizer — Evaluation Framework

## Purpose

This framework measures whether client context actually improves AI campaign analysis and optimization. The goal is not to reward polished language. The goal is to determine whether the system detects the right patterns, ignores noise, prioritizes material business impact, and makes recommendations aligned with client requirements.

## Primary experiment

Run the same synthetic ExoClick dataset through two conditions.

### Condition A — No client context

Prompt the analytics agent with campaign data and schema only.

### Condition B — Client context loaded

Prompt the same model with:

- Golden Rules
- client Requirements
- relevant Campaign History
- Learnings & Decisions
- identical campaign data and schema

Keep model, temperature, dataset, and analysis request as constant as possible.

## Evaluation dimensions

### 1. Ground-truth detection — 25 points

Did the agent identify the planted material patterns?

Scoring:

- 5 = detected clearly and correctly prioritized
- 3 = detected but weakly explained or under-prioritized
- 1 = vaguely noticed
- 0 = missed

### 2. Materiality awareness — 15 points

Did the agent avoid treating tiny-spend/high-metric anomalies as major insights?

- 5 = consistently distinguishes material signal from noise
- 3 = mostly correct with one overreaction
- 1 = repeatedly highlights immaterial segments
- 0 = recommendations are driven by noise

### 3. Client-goal alignment — 20 points

Did analysis interpret results against the actual CAC/CPA/ROAS, pacing, budget, and scale requirements?

- 5 = conclusions consistently framed against requirements
- 3 = partial use of requirements
- 1 = generic performance commentary
- 0 = recommendations contradict client objectives

### 4. Prioritization quality — 15 points

Are the top findings the ones most likely to move total business results?

- 5 = excellent ranking by impact
- 3 = correct findings but weak ordering
- 1 = novelty prioritized over impact
- 0 = top findings are irrelevant

### 5. Interaction/cluster detection — 10 points

Did the agent uncover meaningful multi-dimensional pockets rather than relying only on aggregate campaign averages?

### 6. False-positive control — 5 points

How many unsupported or misleading findings were presented as material?

### 7. Recommendation quality — 10 points

For optimization runs, are actions specific, bounded, evidence-based, and consistent with client guardrails?

**Total score: 100**

## Pass thresholds

- 90-100: strong candidate behavior
- 80-89: useful with targeted fixes
- 70-79: promising but not ready for trusted recommendations
- Below 70: insufficient

## Ground-truth categories to plant

Each synthetic test should include a mix of:

- obvious material winner
- obvious material loser
- hidden interaction winner
- hidden interaction loser
- aggregate result that reverses at a lower level
- low-volume fake winner
- low-volume fake loser
- pacing problem despite acceptable CAC
- acceptable performance that should not be changed
- scale opportunity constrained by CAC ceiling
- segment where broad exclusion would destroy a valuable sub-pocket
- tracking/data-quality anomaly

## False-positive logging

Record every finding that is not supported by the ground truth or is technically true but economically immaterial. Classify as:

- noise overreaction
- wrong baseline
- aggregation error
- insufficient sample
- client-context failure
- unsupported causal claim

## Comparison sheet fields

For each test record:

```
Test ID
Model/version
Context condition
Ground-truth item
Detected? Y/N
Priority rank
Evidence cited
Materiality handled correctly? Y/N
Client requirement used? Y/N
Recommended action
Correct action class? Y/N
False positive? Y/N
Evaluator notes
Score
```

## A/B success criterion

Client-context condition should materially outperform no-context condition, especially on client-goal alignment, prioritization, and false-positive control. A prettier narrative alone does not count as improvement.

## Regression testing

Once a failure is fixed through Golden Rules, prompts, or requirements schema, preserve the test case. Re-run it whenever the system changes so improvements do not break previously solved behavior.

## Evaluation principle

The product wins only if it reasons more like a strong media buyer: it must know what matters, what does not matter, and what should be done next for this specific client.
