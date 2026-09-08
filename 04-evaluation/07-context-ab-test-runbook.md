# DSP Optimizer — Context A/B Test Runbook

## Purpose

Provide a repeatable procedure for testing whether loading client requirements and memory materially improves campaign analysis and optimization quality.

## Test question

Does a context-aware agent produce more decision-useful output than the same model analyzing the same data without client context?

## Preconditions

Before running:

- freeze a synthetic dataset version
- freeze the ground-truth specification
- freeze the Analytics Agent Prompt version
- record model/version and settings
- ensure the evaluator can see ground truth but the test model cannot

## Condition A — Generic / no client context

Inputs:

- campaign/log-level data
- schema/data dictionary
- Analytics Agent Prompt

Do NOT provide:

- client Requirements
- Campaign History
- Learnings & Decisions
- client-specific decision frame

## Condition B — Context-aware

Inputs:

- identical data and schema
- identical Analytics Agent Prompt
- Golden Rules
- client Requirements
- Campaign History
- Learnings & Decisions

## Run procedure

1. Use the exact same dataset for A and B.
2. Use the same model and generation settings.
3. Run Condition A first and save the raw output unchanged.
4. Run Condition B in a fresh session and save the raw output unchanged.
5. Do not allow Condition B to see Condition A's answer.
6. Score both outputs independently against the Evaluation Framework and Ground Truth Specification.
7. Compare not only which truths were found, but how they were prioritized.
8. Log false positives and harmful recommendations separately.

## Required artifacts per run

- raw prompt/input package
- raw model output
- evaluator scorecard
- false-positive log
- missed-ground-truth log
- recommendation comparison
- durable learnings, if any

## Core comparison questions

- Did context change the account-level conclusion?
- Did context make the model interpret CAC correctly relative to target?
- Did context improve pacing interpretation?
- Did context reduce low-volume overreaction?
- Did context improve ranking by spend/conversion impact?
- Did context help preserve useful sub-pockets inside weak aggregates?
- Did context produce more executable recommendations?
- Did context prevent recommendations that conflict with client constraints?

## Minimum success criteria for the product hypothesis

The context-aware run should:

- score higher overall
- score materially higher on client-goal alignment
- have equal or fewer false positives
- rank material findings above tiny-volume anomalies
- avoid at least one mistake the no-context run makes because it lacks the client decision frame

## Suggested first benchmark scenarios

- **Scenario 1:** CAC below target but account under-pacing.
  Expected difference: generic agent celebrates efficiency; context-aware agent identifies controlled-scale need.
- **Scenario 2:** $3-spend segment has extraordinary ROAS.
  Expected difference: generic agent may elevate it; context-aware agent should label it immaterial/exploratory.
- **Scenario 3:** Zone looks weak overall but mobile native 11 PM–2 AM is strong with meaningful volume.
  Expected difference: context-aware agent should avoid broad zone exclusion and surface the interaction pocket.
- **Scenario 4:** High-spend segment runs at $92 CAC while target is $80.
  Expected difference: context-aware agent should rank it above more dramatic but low-volume anomalies.
- **Scenario 5:** Scaling a $55-CAC segment causes marginal CAC to rise above $80.
  Expected difference: optimization agent should recommend bounded scale, not unlimited reallocation.

## Scoring record

```
RUN ID:
Dataset version:
Model/version:
Condition:
Overall score:
Ground-truth detection:
Materiality awareness:
Client-goal alignment:
Prioritization:
Interaction detection:
False positives:
Recommendation quality:
Evaluator notes:
```

## Decision rules after each benchmark

If Condition B wins clearly:

- preserve the test
- treat as regression benchmark
- continue to harder scenarios

If A and B are similar:

- inspect whether requirements were too generic
- inspect whether the analytics prompt already encoded the missing client logic
- add a scenario where client-specific requirements genuinely change the correct decision

If Condition B is worse:

- identify whether excess context distracted the model
- simplify requirements/memory inputs
- remove stale or low-value memory
- rerun before expanding architecture

## Next-stage test

After analytics passes, repeat the same A/B structure for Optimization Agent outputs. Do not move to autonomous execution until recommendation quality and regression performance are consistently strong.
