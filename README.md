# DSP Optimizer — README

## Purpose

This workspace is the shared source of truth for testing and developing the DSP Optimizer before production infrastructure is finalized.

## Core operating model

Client requirements → Observe campaign data → Diagnose → Recommend/Optimize → Verify → Learn → Persist memory.

## Critical principle

No campaign analysis or optimization should occur without first loading the relevant client context and the universal Golden Rules.

## Folder structure

- `00-system/` — architecture, Golden Rules, and reusable requirement-extraction logic.
- `01-clients/` — one folder per client containing requirements, campaign history, learnings, decisions, and later session summaries.
- `02-analysis/` — reusable prompts and logic for understanding campaign performance.
- `03-optimization/` — reusable prompts and logic for recommending or executing changes.
- `04-evaluation/` — ground truth, test cases, scoring, and context-vs-no-context experiments.

## How to use this workspace

1. Run the Requirements Extraction Prompt for a new client.
2. Save the resulting structured requirements in that client's Requirements document.
3. Before analysis, load Golden Rules plus the client Requirements and relevant history/learnings.
4. Analyze the campaign before optimizing it.
5. Score important tests against known ground truth when available.
6. Persist material learnings and decisions back into the client folder.

## Initial validation goal

Use the same synthetic ExoClick dataset in two conditions: (A) generic analysis without client requirements and (B) analysis with client requirements loaded. Compare detection, prioritization, materiality awareness, client-goal alignment, false positives, and recommendation quality.

## Production note

Google Drive is the collaboration and prototyping layer, not necessarily the final runtime architecture. Structured requirements, rules, memory, and evaluation artifacts should later be represented in version-controlled files and/or a database while preserving the same logical separation.
