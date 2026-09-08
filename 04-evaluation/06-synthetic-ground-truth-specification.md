# DSP Optimizer — Synthetic Ground Truth Specification

## Purpose

Define the intentionally planted truths, decoys, and expected reasoning behaviors used to evaluate the analytics and optimization agents.

## Ground-truth philosophy

The synthetic dataset should not merely look realistic. It should contain known patterns that test whether the system can distinguish meaningful business signal from distracting noise.

## Required planted truth types

### GT-01 Material high-spend underperformer

Create a segment that consumes a meaningful share of spend and runs materially above the $80 CAC target.

- Expected behavior: rank as a high-priority risk.
- Failure mode tested: ignoring business impact in favor of more novel patterns.

### GT-02 Material scalable winner

Create a segment with meaningful spend/conversion volume and CAC materially below target.

- Expected behavior: identify as a credible scale candidate, subject to capacity/pacing checks.

### GT-03 Low-volume fake winner

Create a segment with extremely low CAC or very high ROAS but negligible spend and very few conversions.

- Expected behavior: label exploratory/noise; do not recommend major budget reallocation.

### GT-04 Low-volume fake loser

Create a segment with terrible CAC but negligible spend.

- Expected behavior: acknowledge if relevant but do not elevate above material problems.

### GT-05 Hidden interaction winner

Create a broad zone/publisher that looks average or weak overall but contains a strong GEO × device × format × daypart or creative interaction.

- Expected behavior: discover the sub-pocket and avoid broad exclusion.

### GT-06 Hidden interaction loser

Create a generally healthy segment with one narrow interaction driving disproportionate inefficiency.

- Expected behavior: recommend a narrow intervention rather than suppressing the healthy parent segment.

### GT-07 Pacing conflict

Create account-level CAC at or below target while spend is materially behind expected pace.

- Expected behavior: identify a controlled scale problem, not simply declare performance healthy.

### GT-08 Efficiency conflict

Create spend on pace but CAC materially above target.

- Expected behavior: prioritize efficiency before further scale.

### GT-09 Scale ceiling

Create a strong segment that degrades as spend/bid intensity rises, such that unlimited scaling would breach the CAC target.

- Expected behavior: recommend bounded/incremental scale and verification.

### GT-10 Aggregate reversal

Construct a Simpson's-paradox-like case where an aggregate segment appears better/worse because it contains a different mix of GEO/device/format traffic.

- Expected behavior: avoid misleading aggregate conclusion and compare matched slices.

### GT-11 Creative-context dependency

Create a creative that performs poorly overall but strongly within a specific context or audience cluster.

- Expected behavior: avoid global creative rejection without interaction analysis.

### GT-12 Time/daypart pocket

Create a meaningful time window with materially different CAC and enough spend to matter.

- Expected behavior: identify only if volume is sufficient; quantify affected spend.

### GT-13 Tracking anomaly

Plant an impossible or suspicious metric relationship, abrupt conversion drop, duplicate-like behavior, or inconsistent attribution signal.

- Expected behavior: flag as data-quality risk before optimization.

### GT-14 Acceptable no-change segment

Create a material segment close to target with stable volume.

- Expected behavior: explicitly recommend no action or low priority rather than optimizing everything.

### GT-15 Concentration risk

Create acceptable overall performance dominated by one publisher/zone/creative.

- Expected behavior: recognize operational risk without necessarily cutting the winning source.

## Decoy design rules

- Include extreme metrics on tiny spend.
- Include mild statistically interesting differences with little business impact.
- Include segments that look bad on CTR but are strong on CAC.
- Include segments that look strong on CTR but weak on conversion economics.
- Include correlation patterns that should not be stated as causal.

## Ground-truth record schema

For every planted item maintain:

```
Ground truth ID
Dataset version
Pattern description
Dimensions involved
Expected direction
Minimum materiality
Relevant client requirement
Expected analytics conclusion
Expected optimization class
Actions that should NOT be recommended
Evidence fields needed
Scoring weight
```

## Evaluation rule

The evaluator should score the model against this ground truth without exposing the ground-truth file to the model during the run. The file is for benchmark generation and scoring only.

## Initial client-specific expectations

For the Synthetic ExoClick Client:

- $80 CAC is the primary target.
- $60 CAC is a stretch goal.
- $10K is a test budget, not a mandatory spend-at-all-costs commitment.
- pause-and-analyze behavior is acceptable.
- tiny-spend outliers must not dominate conclusions.
- meaningful interaction clusters are a core product hypothesis.
- recommendations remain human-approved during validation.
