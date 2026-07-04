# Contributing

Thanks for contributing to Semantic Version Bumper.

This project follows a simple rule: **do one thing, and do it well**.
Contributions should preserve this focus.

## What to Contribute

- Bug fixes in SemVer bumping behavior.
- Test-case additions for real scenarios.
- Docs improvements that clarify behavior and boundaries.
- CI/CD improvements that increase reliability.

## Scope Guardrails

- In scope: deterministic version bumping from valid inputs.
- Out of scope: parsing commit history, release policy engines, changelog generation.

## Development Flow

1. Fork and create a feature branch.
2. Keep changes small and focused.
3. Update docs when behavior changes.
4. Add or adjust test cases in `.github/workflows/cicd.yml` matrix.
5. Open a PR with clear before/after behavior.

## Testing

- The action is validated through matrix-based workflow tests in `.github/workflows/_test.yml`.
- Each test defines `sem_ver`, `bump_operator`, and `expected_semver`.
- PRs should preserve existing cases and add new ones for edge conditions.

## Style

- Prefer clarity over cleverness.
- Keep bash logic explicit and deterministic.
- Keep operator handling case-insensitive.
- Keep docs aligned with `README.md` and `CHANGELOG.md`.

## Release Notes

If your PR changes behavior, include a short "why" and "impact" note.
This helps keep release notes meaningful and user-centered.
