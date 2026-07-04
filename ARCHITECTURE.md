# Architecture

## Overview

This repository ships a **composite GitHub Action** that bumps a Semantic Version.
Core runtime lives in `action.yml` using bash steps.

## Runtime Flow

1. Validate `sem_ver` format (`X.Y.Z` with optional prerelease suffix).
2. Validate `bump_operator` against supported values.
3. Normalize operator to uppercase (case-insensitive behavior).
4. Apply bump logic:
   - `MAJOR` -> `major+1`, reset `minor` and `patch`.
   - `MINOR` -> `minor+1`, reset `patch`.
   - `PATCH` -> `patch+1`.
   - `DEV_PRERELEASE` ->
     - if already `devN`, increment only dev counter;
     - otherwise increment patch and append `-dev`.
5. Publish `new_sem_ver` through `$GITHUB_OUTPUT`.

## CI/CD Design

- Entry pipeline: `.github/workflows/cicd.yml`.
- Test execution is reusable: `.github/workflows/_test.yml`.
- Test strategy: JSON matrix of GIVEN/WHEN/THEN cases.
- Quality gate job aggregates upstream job outcomes.
- Tag pushes trigger deploy signaling and then GitHub Release.

## Deployment Signaling

- `.github/workflows/_signal_deploy.yml` checks whether a tag belongs to `main` or `release`.
- It emits:
  - `AUTOMATED_DEPLOY` (boolean)
  - `ENVIRONMENT_NAME` (`PROD_DEPLOYMENT` or `TEST_DEPLOYMENT`)

## Architectural Intent

- Keep logic deterministic and side-effect free.
- Keep interface minimal: 2 inputs, 1 output.
- Keep tests behavior-oriented and easy to extend.
