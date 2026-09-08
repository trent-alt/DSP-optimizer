# Synthetic ExoClick Client — Campaign History

## Purpose

Persistent record of campaign runs, material changes, analysis sessions, and outcomes for the synthetic validation client. This file should be updated after each meaningful test cycle so the system does not reason from scratch.

## Current status

- Stage: Pre-production synthetic validation
- Platform: ExoClick
- Test budget framework: $10,000 / nominal 30-day window
- Primary KPI: CAC
- Target: $80
- Stretch target: $60
- Execution mode: Recommendation only

## Baseline assumptions

- The campaign is intentionally designed to include both real signal and misleading noise.
- Some high-performing segments will be low-volume and should not be treated as scalable.
- Some broad segments may look weak while containing valuable lower-level clusters.
- Pacing may intentionally conflict with efficiency to test tradeoff reasoning.

## Run log template

For every analysis cycle append:

```
RUN ID:
Date/time:
Dataset/version:
Spend covered:
Conversions covered:
Context condition: No-context / Client-context
Model/version:
Prompt version:
Golden Rules version:
Requirements version:

ACCOUNT RESULT
Spend:
Conversions:
CAC:
Pacing:
Status vs target:

TOP MATERIAL FINDINGS
1.
2.
3.

LOW-VOLUME / NOISE FINDINGS TO IGNORE
1.
2.

RECOMMENDATIONS MADE
1.
2.
3.

CHANGES APPROVED / SIMULATED
1.
2.

OBSERVED OUTCOME
1.
2.

GROUND-TRUTH SCORE
Detection:
Materiality:
Client alignment:
Prioritization:
False positives:
Recommendation quality:
Total:

DURABLE LEARNINGS TO PERSIST
Only record findings that survived enough evidence to matter.
```

## Initial history

### Run 000 — Setup

- Synthetic client requirements created.
- Golden Rules created.
- Analytics and Optimization agent prompts created.
- Evaluation framework created.
- No production optimization actions have occurred.

### Run 001 — Planned A/B test

- Condition A: Analyze identical synthetic campaign data without client requirements.
- Condition B: Analyze identical data with Golden Rules + client Requirements loaded.
- Goal: Measure whether client context improves prioritization, materiality awareness, client-goal alignment, and recommendation quality.
- Status: Not yet scored in this document.

## History-writing rule

Do not append every small fluctuation. Record only runs, decisions, or outcomes that materially affect future reasoning.
