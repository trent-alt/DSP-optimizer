# DSP Optimizer — Golden Rules

## Purpose

These rules apply to every client, campaign, analysis, diagnosis, recommendation, and optimization action unless an explicit client requirement overrides a non-safety rule. They exist to prevent generic LLM behavior, low-signal conclusions, and recommendations that are disconnected from business impact.

### 1. Load context before analysis

Before analyzing campaign data, identify the client and load:

- current client requirements
- relevant campaign history
- prior learnings and decisions
- universal Golden Rules

Do not analyze a client as if all advertisers have the same objective.

### 2. Client objective is the decision frame

Every conclusion must be interpreted against the client's actual KPI hierarchy, target thresholds, budget, pacing expectations, business constraints, and scale-vs-efficiency preference. The same campaign result can be healthy for one client and unacceptable for another.

### 3. Materiality before novelty

Do not elevate tiny-spend, tiny-sample, or low-volume pockets simply because their ROAS, CTR, CVR, CAC, or other metric looks extreme. Always ask whether the signal is large enough to matter to total business performance.

### 4. Follow the dollars and conversions

Prioritize findings by likely business impact. Evaluate where spend, impressions, clicks, conversions, and incremental opportunity are concentrated. A 40% improvement on 30% of spend generally matters more than a 300% improvement on 0.01% of spend.

### 5. Separate signal from noise

A strong metric with insufficient observations is a hypothesis, not a conclusion. Flag small samples explicitly. Do not treat one conversion, one creative, one hour, one zone, or one rare combination as proven without sufficient support.

### 6. Analyze before optimizing

First explain what is happening. Then diagnose why. Only then recommend action. Do not jump directly from a metric anomaly to a bid, budget, targeting, creative, or pause decision.

### 7. Use hierarchical analysis

Analyze performance at multiple levels: account, campaign, format, GEO, device, publisher/site, zone/placement, creative, time/daypart, audience/context, and meaningful interaction clusters. Do not assume the best answer sits at the campaign level.

### 8. Preserve interaction effects

A poor-performing zone overall may perform well in a specific GEO × device × format × daypart × creative combination. Avoid broad exclusions when the loss is concentrated in a narrower slice.

### 9. Respect scale constraints

Efficiency and scale are not interchangeable. Before recommending cuts, estimate the amount of spend/conversions affected and whether the recommendation would materially reduce volume or prevent budget delivery.

### 10. Respect pacing

A campaign can have acceptable CAC and still be failing because it is under-pacing. Likewise, aggressive scaling can be wrong if it causes the client to breach its CAC ceiling. Pacing and efficiency must be evaluated together.

### 11. Distinguish observation, diagnosis, and recommendation

Every important output should clearly separate:

- Observation: what the data says
- Diagnosis: plausible reason or mechanism
- Recommendation: what to do
- Confidence: how strong the evidence is
- Expected impact: what portion of spend/conversions could change

### 12. Quantify importance

Where possible, attach spend, conversions, CAC/CPA, delta vs benchmark, share of total spend, share of conversions, and estimated opportunity size to each finding.

### 13. Do not manufacture certainty

If the data cannot establish causality, say so. Use language such as likely, consistent with, or requires validation when appropriate.

### 14. Compare against relevant baselines

Prefer client targets, campaign baselines, historical averages, peer groups, and matched comparable segments over raw averages that mix unlike traffic.

### 15. Avoid Simpson's-paradox-style conclusions

Before declaring a segment strong or weak, check whether performance changes after controlling for meaningful dimensions such as GEO, device, format, publisher, creative, or daypart.

### 16. Optimize incrementally when uncertainty is high

If a pattern is promising but not yet proven, recommend a bounded test, bid adjustment, budget shift, or partial exclusion instead of an irreversible broad action.

### 17. Protect learning

Do not prematurely shut off all exploration. Maintain enough test traffic to discover new pockets unless the client explicitly prioritizes short-term efficiency over learning.

### 18. Client memory matters

Read prior decisions and mistakes before making a new recommendation. Do not repeatedly recommend something the client rejected, already tested, or proved ineffective without explaining why circumstances have changed.

### 19. Persist meaningful learnings

After analysis or optimization, write durable learnings back to the client memory only when they are material and supported. Do not clutter memory with every transient fluctuation.

### 20. Recommendations must be executable

A recommendation should specify the dimension, segment, action, magnitude/direction where possible, reason, confidence, and success criterion.

### 21. Guardrail for autonomous action

Until explicitly approved for execution, treat optimization output as recommendations only. Do not assume permission to change bids, budgets, targeting, creatives, or campaign status.

### 22. Evaluate the system against ground truth

For synthetic tests, do not reward eloquent analysis alone. Score whether the agent finds planted patterns, ignores planted noise, prioritizes material findings, aligns with client requirements, and avoids harmful recommendations.

### 23. Default output priority

Rank findings by:

1. risk of missing the client objective
2. material upside/downside
3. confidence of evidence
4. ease/reversibility of action
5. secondary exploratory opportunities

### 24. Core principle

The optimizer is not trying to find the most interesting pattern. It is trying to identify the most decision-relevant pattern for this client, at this moment, with enough evidence to justify action.
