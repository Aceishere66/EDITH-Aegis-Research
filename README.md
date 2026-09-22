# EDITH Aegis — AI Engineering Research

Curated public research edition of **EDITH Aegis**, focused on the project's LLM evaluation, coding-agent workflow and multi-model engineering methodology.

> The full Aegis project is private. This repository intentionally excludes security targets, vulnerability research data, credentials, private evidence, operational program material and implementation details that are not needed to demonstrate the AI/software-engineering work.

## Why this repository exists

The goal is to show an engineering approach to LLMs that goes beyond "ask a model to write code".

The working principle is:

> Models are tools with different strengths, costs and failure modes. Their output should be scoped, testable, reviewable and subordinate to explicit engineering decisions.

## Areas covered

- model evaluation for task-specific work
- model routing
- context engineering
- coding-agent task decomposition
- structured handoffs between models
- implementation/review separation
- build and test evidence
- human-controlled architecture decisions
- provenance and auditability of AI-generated artifacts
- deterministic code for policies and state transitions

## Multi-model workflow

```text
Human engineer
      │
      ├── requirements
      ├── architecture
      ├── constraints
      └── acceptance criteria
      │
      ▼
Planning / analysis model
      │
      ▼
Implementation agent
      │
      ▼
Build + tests + static checks
      │
      ▼
Independent review model/agent
      │
      ├── reject / request changes
      └── accept with evidence
      │
      ▼
Human validation
```

Not every task uses every stage. The workflow is selected according to risk and complexity.

## Model selection

Aegis development uses provider-neutral reasoning:

- cheap/fast models for routine classification or mechanical work
- stronger coding models for implementation
- reasoning-focused models for architecture or difficult analysis
- separate review when independent scrutiny is valuable

The objective is not to always use the most expensive model. It is to use the appropriate model for the task and verify the result.

## Engineering rules

Representative rules used in the private project include:

- inspect before editing
- define scope before implementation
- prefer the smallest testable vertical slice
- keep architecture and policy deterministic where possible
- do not fabricate benchmark/test results
- add or modify tests with behavior
- run focused verification before full-suite verification
- report what was changed and what remains unverified
- treat model output as advisory rather than authoritative

## Documentation

- [LLM evaluation methodology](docs/LLM_EVALUATION.md)
- [Coding-agent engineering workflow](docs/AGENTIC_WORKFLOW.md)
- [Structured handoff template](examples/STRUCTURED_HANDOFF.md)
- [Evaluation template](examples/MODEL_EVALUATION_TEMPLATE.md)
- [Public scope](docs/PUBLIC_SCOPE.md)

## Related

- Engineering portfolio: https://github.com/Aceishere66/engineering-portfolio
- EDITH Dev Studio engineering page: https://edithdevstudio.com/engineering
