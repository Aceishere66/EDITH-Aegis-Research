# Coding-Agent Engineering Workflow

## Principle

A coding agent is most useful when the surrounding engineering system is explicit.

The goal is not to hand over an entire project and hope for a correct result. The goal is to construct a bounded environment where an agent can make useful progress and where completion can be verified.

## 1. Define the task

Before implementation:

- state the problem
- identify the relevant subsystem
- define constraints
- define non-goals
- specify acceptance criteria
- identify required verification

## 2. Build context deliberately

Useful context can include:

- architecture documentation
- current repository status
- exact files or modules
- previous decisions
- test expectations
- known failures
- interfaces that must remain stable

More context is not automatically better. Irrelevant context can reduce precision.

## 3. Decompose

Large changes are split into stages that can be inspected independently.

```text
research
  ↓
decision
  ↓
small implementation slice
  ↓
verification
  ↓
next slice
```

## 4. Separate roles when useful

Different models can be assigned different roles:

- planner / analyst
- implementer
- reviewer / critic

A reviewer should receive enough evidence to challenge the implementation rather than simply repeat the implementer's reasoning.

## 5. Verification is part of the task

Completion claims should be backed by available evidence:

- build
- unit tests
- integration tests
- static checks
- diff review
- platform/hardware validation when required

An agent should state what it could not verify.

## 6. Structured handoff

Long-running work benefits from explicit state transfer:

- current objective
- current branch/commit
- completed work
- unresolved issues
- architectural constraints
- next exact action
- tests already run
- known risks

This makes work resumable across models or sessions without relying on conversational memory alone.

## Human responsibility

The human remains responsible for:

- selecting objectives
- approving architecture
- accepting trade-offs
- judging whether evidence is sufficient
- deciding when an agent's output is merged or rejected
