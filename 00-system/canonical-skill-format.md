# Canonical Skill Format (Design Brief)

> Original design brief for the canonical skill format. This is the source
> instruction / specification for building the skill system; it has not yet been
> implemented in this repo.

You are the senior AI systems architect for the DSP Optimizer project.

We are building an agentic media-buying decision system that sits on top of DSPs, beginning with ExoClick.

The system is evolving around this loop:

```
DOMAIN EXPERTISE
→ explicit heuristics/rules
→ reusable skills
→ agent decisions
→ shadow-mode comparison against a human expert
→ outcomes
→ disagreement analysis
→ skill improvement
→ eventually guarded/autonomous execution
```

Your task is to DESIGN AND IMPLEMENT the canonical skill format for this system.

Do not merely write a document describing what a skill could look like.

Build the actual reusable skill specification, templates, validation rules, examples, and supporting repo structure so that every future skill follows the same contract.

## 1. Core design principle

A skill represents a bounded capability or body of decision logic that the agent can load when performing a specific task.

Examples:

- pacing diagnosis
- budget allocation
- bidding
- conversion-rate diagnosis
- zone quality analysis
- creative performance analysis
- anomaly detection
- temporal/daypart analysis
- scaling decisions
- objective interpretation
- ExoClick-specific optimization
- fraud/traffic-quality diagnosis

Skills must be:

- modular
- human-readable
- machine-readable
- versioned
- testable
- auditable
- composable
- platform-aware
- objective-aware
- capable of expressing exceptions and uncertainty
- tied to evaluation cases
- usable in shadow mode
- safe to improve over time without silently changing historical behavior

Do NOT create one giant "media buying" skill.

Skills should be small enough to reason about, evaluate, version, and improve independently.

## 2. Define the canonical skill contract

Create a formal canonical schema for every skill.

At minimum, every skill should support the following fields/concepts:

### IDENTITY

- skill_id
- name
- version
- status
- owner
- created_at
- updated_at
- description

### SCOPE

- capability
- applicable_platforms
- applicable_verticals
- applicable_objectives
- applicable_campaign_types
- exclusions
- prerequisites
- dependent_skills

### PURPOSE

- what question this skill answers
- what decisions it supports
- what it explicitly does NOT decide

### INPUT CONTRACT

- required inputs
- optional inputs
- input definitions
- units
- acceptable ranges
- required time windows
- required levels of granularity
- data freshness requirements
- missing-data handling

### CONTEXT

- business objective
- KPI hierarchy
- campaign constraints
- account/client constraints
- platform constraints
- inventory constraints

### SIGNALS / FEATURES

For every important signal:

- signal name
- definition
- why it matters
- calculation
- directionality
- thresholds if applicable
- minimum sample requirements
- interactions with other signals
- caveats

### HEURISTICS / RULES

Each rule must include:

- rule_id
- name
- condition
- evidence required
- interpretation
- recommended action
- expected effect
- confidence
- severity/priority
- exceptions
- conflicting-rule handling
- whether the rule is universal, platform-specific, vertical-specific, or client-specific

### DIAGNOSTIC LOGIC

The skill must distinguish:

- observation
- diagnosis
- recommendation

For example:

- Observation: CAC increased 25%.
- Diagnosis: CAC increased because CVR fell while CPC remained stable.
- Recommendation: Investigate zone/creative quality before changing bids.

Do not collapse these three stages.

### DECISION OUTPUT

Define the exact structured output the skill produces.

At minimum:

- diagnosis
- findings
- recommended_action
- action_parameters
- rationale
- confidence
- evidence
- alternative_explanations
- risks
- expected_outcome
- review_window
- escalation_required
- skills_used

### GUARDRAILS

- actions never allowed automatically
- actions requiring human approval
- maximum permitted changes
- insufficient-evidence behavior
- conflicting-signal behavior
- low-confidence behavior
- stop conditions

### EXCEPTIONS

Provide a formal way to encode:

- known exceptions
- edge cases
- situations where a normal rule should not fire
- client-specific overrides
- platform-specific overrides

### UNCERTAINTY

The system should never pretend all recommendations have equal certainty.

Define:

- confidence scale
- evidence sufficiency
- unresolved ambiguity
- assumptions
- unknowns

### TEMPORAL BEHAVIOR

Specify:

- how much history is required
- comparison windows
- when to wait instead of act
- cooling-off period after changes
- when a recommendation becomes stale
- how recent changes affect analysis

### EVALUATION

Every skill must link to:

- eval cases
- expected outputs
- shadow-mode cases
- regression tests
- known failure cases

### PROVENANCE

For each rule or major heuristic, support:

- source
- source_type
- expert
- transcript/research reference
- date captured
- confidence in source
- notes

### LEARNING / CHANGE HISTORY

The skill must support:

- changelog
- why a rule changed
- what evidence caused the change
- which evals changed
- whether historical decisions should be re-evaluated

## 3. Create both human and machine representations

I want a skill to have two complementary representations.

**A. Human-readable Markdown**

Example: `skills/pacing/SKILL.md`

**B. Machine-readable YAML or JSON**

Example: `skills/pacing/skill.yaml`

Decide which machine-readable format is more appropriate and explain why.

The Markdown should be easy for Trent, the domain expert/non-engineer, to review and edit.

The structured file should be strict enough for the application to validate and load programmatically.

Avoid unnecessary duplication.

If possible, define one as authoritative and generate/validate the other.

## 4. Build a schema

Create a real schema for the machine-readable skill format.

Use an appropriate schema technology such as:

- JSON Schema
- or Pydantic/Zod equivalent if more appropriate for the existing stack.

The schema must validate:

- required fields
- IDs
- semantic versioning
- enums
- arrays
- nested rules
- thresholds
- output contracts
- guardrails
- eval references
- provenance

A malformed skill should fail validation clearly.

Include useful validation error messages.

## 5. Define skill types / classification

Create a taxonomy so skills do not become inconsistent.

At minimum consider:

- diagnostic skill
- decision skill
- calculation skill
- platform knowledge skill
- objective interpretation skill
- guardrail skill
- orchestration skill

Determine whether these should be explicit skill types.

Explain which types are allowed to recommend actions and which are informational only.

## 6. Define rule precedence

This is important.

The optimizer will eventually have:

- global rules
- platform rules
- vertical rules
- account/client rules
- campaign rules
- temporary overrides

Define deterministic precedence.

A reasonable starting concept is:

```
temporary explicit override
>
campaign-specific
>
client/account-specific
>
vertical-specific
>
platform-specific
>
global
```

But do not blindly accept this.

Think through conflicts and implement a clear precedence system.

The agent must be able to explain:

"Rule X was not applied because Rule Y had higher precedence."

## 7. Define skill composition

Skills will be loaded together.

For example, a campaign diagnosis might use:

```
objective interpretation
+
pacing
+
conversion diagnosis
+
zone analysis
+
ExoClick platform knowledge
```

Define how skills interact.

We need:

- dependencies
- required skills
- optional supporting skills
- incompatible skills
- priority
- conflict resolution
- shared context
- no circular dependencies

Create validation for dependency loops if practical.

## 8. Define the standard agent response contract

Create a common structured response object used by skills.

For example:

```json
{
  "skill_id": "",
  "skill_version": "",
  "timestamp": "",
  "objective": "",
  "observations": [],
  "diagnoses": [],
  "recommendations": [],
  "confidence": 0.0,
  "evidence": [],
  "assumptions": [],
  "unknowns": [],
  "guardrails_triggered": [],
  "escalation_required": false,
  "review_at": "",
  "metadata": {}
}
```

Improve this substantially.

It must support comparison against a human decision in shadow mode.

## 9. Shadow mode compatibility

Every skill needs to support future shadow-mode evaluation.

Design the schema so we can record:

- exact skill version used
- exact inputs available at decision time
- timestamp
- agent output
- rules fired
- rules considered but suppressed
- missing information
- confidence
- expected outcome

We must later be able to compare that against:

- human diagnosis
- human recommendation
- actual action
- actual outcome

Do not allow future information leakage.

The skill execution record must preserve what the agent knew at the moment of the decision.

## 10. Build example skills

After defining the format, implement at least THREE example skills.

Use:

1. pacing-diagnosis
2. conversion-rate-diagnosis
3. zone-quality-analysis

These examples should be realistic enough to prove that the schema works.

Do NOT pretend we already know every ExoClick threshold.

Where exact thresholds are unknown, explicitly use placeholders or configurable parameters and mark them as needing empirical validation.

Do not invent platform facts.

## 11. Build a domain expertise capture template

We also need to turn Trent's tacit expertise into skills.

Create a structured "expertise capture" template/process.

The input might be conversational and messy, such as:

"When I see spend fall unexpectedly, I first check whether bids changed. If they didn't, I look at available traffic and win rate. But I wouldn't react immediately if we just changed creative…"

The capture process should extract:

- observation
- rule
- conditions
- metrics
- decision
- exceptions
- confidence
- scope
- questions still unresolved

Create:

`knowledge/expertise-capture-template.md`

and if useful:

`knowledge/expertise-capture.schema.json`

The goal is that Trent can unload expertise naturally and the system can convert it into a candidate skill/rule.

Candidate rules must NOT silently become production rules.

Define statuses such as:

- draft
- expert-reviewed
- shadow-testing
- validated
- deprecated

## 12. Repo structure

Implement a clean structure similar to:

```
skills/
  _schema/
  _templates/
  pacing-diagnosis/
    SKILL.md
    skill.yaml
    evals/
  conversion-rate-diagnosis/
  zone-quality-analysis/

knowledge/
  expertise-capture/
  principles/
  heuristics/

evals/
  fixtures/
  shadow/
  regression/

docs/
  canonical-skill-format.md
  skill-authoring-guide.md
```

Adjust if there is a better architecture.

## 13. Create authoring rules

Write concise rules for anyone creating a new skill.

For example:

- one skill = one bounded responsibility
- do not hide business logic in prose
- every recommendation must cite the evidence/signals that triggered it
- separate observation from diagnosis from action
- unknown is better than invented
- configurable threshold is better than false precision
- every production rule requires provenance
- every validated skill needs eval coverage
- breaking behavioral changes require version increment
- client overrides cannot silently mutate global logic

Expand and formalize these.

## 14. Versioning

Define semantic version behavior.

For example:

**PATCH:**

- wording or documentation
- no decision behavior changes

**MINOR:**

- new backward-compatible rules/signals
- new optional output

**MAJOR:**

- changes to meaning
- decision behavior breaks
- required input changes
- output contract breaks

Determine whether this model is appropriate.

Most importantly, historical shadow decisions must always retain the skill version that produced them.

## 15. Testing

Create automated tests for:

- valid skill
- missing required input
- malformed rule
- duplicate rule ID
- invalid version
- invalid confidence
- broken dependency
- invalid scope
- rule precedence
- guardrail behavior

Also create at least a few behavioral eval fixtures.

## 16. Document the whole thing

Create:

`docs/canonical-skill-format.md`

It should answer:

- What is a skill?
- Why do skills exist?
- What belongs in a skill?
- What does not belong in a skill?
- How are skills created?
- How are they reviewed?
- How do skills become validated?
- How are they loaded?
- How are conflicts resolved?
- How do skills participate in shadow mode?
- How do skills evolve?
- How do we prevent bad rules from contaminating the optimizer?

Write it for both:

- Trent, a domain expert/non-engineer
- Ryan, an engineer/data scientist

## 17. Important product principles

Preserve these principles:

1. We are encoding expertise, not merely prompts.
2. Rules must be inspectable.
3. The agent must be able to explain what rule fired and why.
4. Human expertise is initially the benchmark, not permanent ground truth.
5. Agent-human disagreements are valuable learning data.
6. Eventually the agent should be capable of identifying patterns the human missed.
7. Synthetic data is useful for development and testing but does not substitute for real-world calibration.
8. Platform-specific knowledge must remain separate from universal media-buying logic where possible.
9. Never invent certainty or thresholds.
10. Do not allow a newly captured heuristic to become autonomous production logic without review/evaluation.
11. Historical reproducibility matters. We must be able to replay a decision using the exact skill version and information available at that point in time.
12. Build for shadow mode first; autonomous execution comes later.

## 18. Execution style

Do not overengineer this into a giant framework.

Start with the smallest robust version that can support:

- authoring skills
- validating skills
- loading skills
- running them
- recording outputs
- evaluating them

Use existing project conventions where sensible.

Inspect the repository before making decisions.

Do not overwrite existing architecture blindly.

If a relevant structure already exists, extend it.

Keep dependencies minimal.

Prefer understandable code over clever abstractions.

## 19. Deliverables

By the end, I should have:

1. canonical skill specification
2. machine-readable schema
3. human-readable skill template
4. structured skill template
5. three example skills
6. expertise capture template
7. skill lifecycle/status system
8. versioning standard
9. precedence/conflict model
10. dependency/composition model
11. standard skill output contract
12. shadow-mode execution record
13. validation tooling
14. automated tests
15. behavioral eval examples
16. authoring guide
17. canonical-skill-format documentation
18. concise explanation of architectural decisions

## 20. Final review

Before considering this complete, test the format against these questions:

- Can Trent understand and critique a skill without reading code?
- Can Ryan change its implementation without changing its conceptual contract?
- Can the application validate malformed skills?
- Can two skills disagree deterministically?
- Can the system explain which rule won?
- Can we identify exactly which skill version caused a decision?
- Can we replay historical shadow-mode decisions?
- Can client/platform overrides coexist without corrupting universal rules?
- Can an uncertain rule remain explicitly uncertain?
- Can expertise be captured before it is trusted?
- Can we determine whether a skill is getting better over time?

If any answer is no, revise the design.

Then provide me:

- the resulting file tree
- the key architectural decisions
- what was actually implemented
- any assumptions you had to make
- the next 3 highest-priority steps
