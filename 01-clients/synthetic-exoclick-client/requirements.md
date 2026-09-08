# Synthetic ExoClick Client — Requirements

## CLIENT IDENTITY

- Client name: Synthetic ExoClick Client
- Aliases / shorthand: Synthetic Client, Test Client
- Vertical: Performance acquisition / non-traditional digital advertiser
- Platform(s): ExoClick
- Campaign / initiative: Initial DSP Optimizer validation campaign

## OBJECTIVE HIERARCHY

- Primary objective: Acquire conversions efficiently while maintaining enough scale to learn.
- Primary KPI: CAC
- Target: $80 CAC
- Hard ceiling/floor: Treat sustained CAC above $80 as off-target; do not overreact to isolated low-volume spikes.
- Stretch target: $60 CAC
- Secondary KPIs: conversion volume, pacing, CVR, CPC, spend efficiency, concentration risk
- Conversion definition: Completed signup / acquisition event represented by the synthetic conversion flag.

## BUDGET & PACING

- Total budget: $10,000 test budget
- Flight dates: 30-day nominal test window
- Daily pacing expectation: Flexible; average roughly $333/day if fully spent, but the campaign may pause for analysis.
- Must spend in full?: No. Efficient learning is more important than forcing spend.
- Pause-and-analyze allowed?: Yes. The test may run for several days, pause, analyze, adjust, and resume.

## SCALE VS EFFICIENCY

- Priority: Hit or beat the $80 CAC target while discovering scalable pockets.
- Acceptable tradeoff: Some CAC deterioration may be acceptable if it unlocks meaningful incremental conversion volume, but recommendations must explicitly quantify the tradeoff.
- Minimum volume requirement: Do not treat tiny-spend or one-conversion pockets as scalable winners.

## TARGETING & INVENTORY

- GEOs: Multiple synthetic GEOs represented in the dataset.
- Devices: Mobile and desktop where available.
- Formats: Native and other ExoClick-compatible formats represented in the dataset.
- Allowed inventory: Broad enough to discover publisher/zone-level patterns during the test.
- Restricted inventory: None unless explicitly encoded in the synthetic data or later requirements.
- Retargeting / 1P data: Not assumed for the initial synthetic validation.

## CREATIVE

- Available assets: Multiple synthetic creatives/creative IDs.
- Constraints: No client-brand constraints are assumed in the synthetic test unless encoded.
- Testing expectations: Creative-level and creative-interaction analysis is required, but low-volume creative outliers must not be over-prioritized.

## MEASUREMENT

- Attribution: Use the synthetic conversion/revenue fields as source of truth.
- Tracking method: Log-level impression/click/conversion data generated for evaluation.
- Source of truth: Synthetic dataset plus separate ground-truth file.
- Known gaps: Synthetic data approximates real DSP behavior and may not represent every ExoClick delivery mechanic.

## OPTIMIZATION AUTHORITY

- Mode: Recommendation only for initial validation.
- Allowed actions: Recommend bid changes, budget shifts, zone/publisher actions, daypart changes, creative tests, targeting adjustments, and pauses.
- Approval-required actions: All actual execution.
- Bid guardrails: Do not recommend extreme bid changes without high-confidence evidence.
- Budget guardrails: Prefer incremental reallocations; do not move more budget into a segment than the evidence suggests it can absorb.

## REPORTING

- Review cadence: After meaningful spend accumulation and at explicit pause points.
- Required outputs: account health, material findings, cluster findings, noise to ignore, risks, opportunities, prioritized recommendations, confidence, expected impact.
- Stakeholder preferences: Concise but evidence-heavy; focus on what moves the needle rather than statistically interesting trivia.

## HISTORY & KNOWN LEARNINGS

- Prior tests: Initial synthetic validation; no real production history yet.
- Known winners: TBD by analysis.
- Known losers: TBD by analysis.
- Rejected strategies: Treating tiny-spend outliers as major findings; generic campaign-level optimization without client context.
- Other context: The system is specifically being tested on whether client requirements change the quality of analysis versus a generic no-context run.

## UNRESOLVED QUESTIONS

- Exact minimum spend/conversion threshold for declaring a segment proven should be learned during testing rather than hard-coded prematurely.
- Exact scale-vs-CAC tradeoff tolerance should be stress-tested across synthetic scenarios.
- Whether future production use will support autonomous execution remains TBD.

## FINAL DECISION FRAME

- Optimize primarily toward CAC ≤ $80.
- Treat $60 CAC as a stretch goal, not a mandatory cutoff.
- Do not force the full $10K spend if doing so destroys efficiency.
- Do not declare tiny-volume segments winners or losers.
- Prioritize findings that affect meaningful shares of spend/conversions.
- Search for narrow interaction clusters before making broad exclusions.
- Evaluate pacing and CAC together.
- Preserve test traffic when evidence is uncertain.
- All actions remain recommendations during validation.
- Score every important run against known synthetic ground truth.
