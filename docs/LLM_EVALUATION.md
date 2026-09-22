# LLM Evaluation Methodology

## Objective

Model evaluation should answer a practical engineering question:

> Which model is the best fit for this specific class of task under the current constraints?

A single overall "smartest model" label is less useful than task-specific evidence.

## Example dimensions

Depending on the task, a comparison can consider:

- functional correctness
- instruction following
- code quality
- regression rate
- ability to use repository context
- architecture adherence
- test quality
- review quality
- latency
- token/compute cost
- recovery from incomplete context

## Controlled comparison

A useful evaluation keeps the task and evidence stable:

```text
same task
same repository state
same acceptance criteria
same allowed context
        │
        ├── Model A
        ├── Model B
        └── Model C
        │
        ▼
build / tests / review evidence
        │
        ▼
task-specific conclusion
```

## Avoiding subjective-only evaluation

Preference can be recorded, but should not replace observable evidence.

Examples of stronger evidence:

- test pass/fail
- compile result
- number of regressions introduced
- scope violations
- unsupported claims
- files changed unnecessarily
- whether acceptance criteria were actually satisfied

## Routing

The practical output of evaluation is a routing rule, not a leaderboard.

Example:

- routine mechanical edit → fast coding model
- architecture decision → reasoning-oriented model
- broad implementation → coding agent with repository context
- sensitive/high-risk change → implementation + independent review
- long research synthesis → research model with explicit sources

Routing is revised when evidence changes.
