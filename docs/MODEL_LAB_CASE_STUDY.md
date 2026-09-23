# Model Lab Case Study — Role Selection

## Scope

This case study is derived from the private EDITH Aegis Model Lab selection work.

```text
Source repository: Aceishere66/EDITH-Aegis
Source commit: 54f47d1c6c53e2c57c0f3ee29f33fc0b61a77891
Selection date: 2026-09-12
Scope: local/self-hosted research models
```

## Final role assignment

| Research role | Selected model | Runtime route |
|---|---|---|
| `FAST_ANALYST` | `gpt-oss:20b` | `fast` |
| `DEEP_CODE_ANALYST` | `qwen3:14b` | `deep`, `analyst` |
| `RESEARCH_CRITIC` | `qwen3.6:27b-coding` | `critic` |
| `SECOND_OPINION` | `qwen3.8:27b` | `review` |

## Why the critic received a holdout

The initial critic benchmark left two finalists effectively tied:

| Model | Mean quality | Verdicts | FP | FN | Evidence precision | Evidence recall |
|---|---:|---:|---:|---:|---:|---:|
| `qwen3.6:27b-coding` | 97.02 | 7/7 | 0 | 0 | 1.00 | 0.95 |
| `gemma4:26b` | 96.79 | 7/7 | 0 | 0 | 1.00 | 0.95 |

A 0.23-point difference was treated as non-decisive.

A separate 12-case holdout was therefore frozen **before inference**, with an equal distribution of:

- 4 ACCEPT
- 4 REJECT
- 4 NEEDS_MORE_EVIDENCE

## Holdout integrity

The private benchmark froze case, fixture and ground-truth manifests with SHA-256 before model execution and checked the same hashes again after the run.

This prevents accidental case mutation after seeing results.

## Holdout result

| Metric | qwen3.6:27b-coding | gemma4:26b |
|---|---:|---:|
| Mean quality | **99.375** | 97.500 |
| Correct verdicts | **12/12** | **12/12** |
| False positives | **0** | **0** |
| False negatives | **0** | **0** |
| Evidence precision | **1.0000** | **1.0000** |
| Evidence recall | **0.9722** | 0.8889 |
| Instruction compliance | **12/12** | **12/12** |
| Mean latency | 19.41 s | **5.65 s** |

## Precommitted decision order

The selection priorities were:

1. zero false positives
2. zero false negatives
3. verdict correctness
4. mean quality ≥ 90
5. evidence precision = 100%
6. evidence recall approximately ≥ 95%
7. instruction compliance
8. quality/latency as tie-breakers after the safety/evidence gates

Under those criteria, `qwen3.6:27b-coding` was selected for the critic role.

## Scorer correction

The evaluation pipeline itself exposed a bug.

The original scorer used a plain substring search for forbidden claims. A correct critic sentence such as:

```text
SQL injection is not supported.
```

could be penalized simply because the forbidden phrase appeared in the response.

The scorer was corrected so critic roles were not penalized for **naming a claim they were explicitly rejecting**. Existing model outputs were rescored; inference was not rerun.

## Engineering lessons

- benchmark infrastructure needs tests too
- close aggregate scores should not be overinterpreted
- frozen holdouts reduce post-hoc selection bias
- precommitted decision gates make model selection auditable
- quality and latency can legitimately trade off differently by role
- a model can be excellent overall but still miss one role-specific acceptance gate
