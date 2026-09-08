# Shadow Record Format

> Format for a single shadow-mode decision record: what was known at the moment
> of a decision, what the human and the agent each concluded, where they
> disagreed, what was actually done, and what happened afterward.

## DECISION ID

Timestamp

## OBJECTIVE

Target CAC / spend / conversion target / constraints

## AVAILABLE INFORMATION AT THAT MOMENT

- Campaign metrics
- Zone metrics
- Creative metrics
- Hourly trends
- Historical context

## HUMAN

- Diagnosis
- Recommendation
- Expected outcome
- Confidence
- Reasoning

## AGENT

- Diagnosis
- Recommendation
- Expected outcome
- Confidence
- Rules/skills invoked

## DISAGREEMENT

- Same diagnosis?
- Same action?
- Magnitude difference?
- Timing difference?

## ACTUAL ACTION

What was really done

## OUTCOME

- 1h
- 6h
- 24h
- 3d

## VERDICT

- Human better
- Agent better
- Equivalent
- Indeterminate

## LEARNING

- New rule?
- Exception?
- Skill change?
- No change?
