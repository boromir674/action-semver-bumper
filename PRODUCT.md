# Product

## Semantic Version Bumper

Semantic Version Bumper is a focused GitHub Action for one job:
turn **(current version + bump operator)** into **new semantic version**.

## Problem It Solves

Teams need consistent version increments in CI/CD.
Manual bumping is repetitive and error-prone.
This action provides deterministic, automation-friendly SemVer bumping.

## Target Users

- Maintainers running release pipelines on GitHub Actions.
- Teams that want explicit, auditable bump behavior.
- Projects that need dev prerelease progression (`-dev`, `-dev1`, ...).

## Product Behavior

- Inputs: `sem_ver`, `bump_operator`.
- Output: `new_sem_ver`.
- Operators: `MAJOR`, `MINOR`, `PATCH`, `DEV_PRERELEASE` (case-insensitive).
- Dev prerelease rule:
  - stable -> patch+1 and `-dev`
  - existing dev prerelease -> increment dev counter only

## Product Principles

- Pure-function mindset: same input, same output.
- Single responsibility: no commit parsing, no release orchestration.
- Low integration friction: drop-in composite action.
- Tested Github Action 

## Non-Goals

- Deciding bump level from Conventional Commits.
- Managing changelog strategy.
- Acting as a full release manager.

## Success Criteria

- Predictable output across all supported bump operators.
- Clear test coverage through CI matrix scenarios.
- Documentation that makes behavior obvious to first-time users.
