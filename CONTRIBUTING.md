# Contributing to Turing Study

Thanks for helping. This is a student project run by Turing Council, so the process is deliberately light: a few rules, enforced by GitHub where possible.

## Before you start

- **The plan is in [`docs/plan/`](docs/plan/README.md)**; decisions are in [`docs/decisions/`](docs/decisions/README.md).
- **Pick work** from the **Turing Study** project board, the [milestones](https://github.com/Turing-Council/study/milestones) or issues labelled `good first issue`. Assign yourself so nobody else picks it up. Max 2–3 open PRs per person.
- Using an AI coding agent? It must follow [`AGENTS.md`](AGENTS.md), and you are responsible for what it produces.

## Workflow

1. **Issue first** for anything non-trivial (Feature, Bug or Spike form). Typos and small doc fixes can go straight to a PR.
2. **Branch** from `main` as `type/short-slug`, e.g. `feat/past-paper-archive`, `fix/grading-rounding`.
3. **Open a PR** early (draft is fine) and fill in the template. One issue = one small PR.
4. **Squash merge.** The PR title becomes the commit on `main`, so it must follow [Conventional Commits](https://www.conventionalcommits.org/): `type(scope): summary`. CI checks it. Allowed types and scopes are in [`.github/workflows/pr-title.yml`](.github/workflows/pr-title.yml).
5. **Review.** Every PR is reviewed by someone other than its author (a human, or a second agent for routine changes). Secrets, the Keycloak realm, GDPR-relevant code and production infra always need a human review.

## Definition of done

- Lint, type checks, tests and the contract check pass locally and in CI.
- Requirement IDs referenced in the PR.
- Docs updated when behaviour changes; an ADR added when a decision is made.
- DB migrations are expand/contract, compatible with the previous release.
- Generated code regenerated, never hand-edited.
- 0 serious axe violations on touched routes; empty and error states designed.
- Under ~400 changed lines (excluding generated files and fixtures).

## When to write an ADR

Copy [`docs/decisions/000-template.md`](docs/decisions/000-template.md) when a choice is costly to reverse, adds a dependency or external service, or departs from the plan. Reserve the number when the spike issue opens, and add it to the table in [`docs/decisions/README.md`](docs/decisions/README.md).

## Local setup

The code scaffold doesn't exist yet (M0). Once it lands, `just up` starts the stack and `just --list` shows every task.

## Security, copyright and takedowns

Don't open a public issue. See [`SECURITY.md`](SECURITY.md).

## Conduct

Be decent. See [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md).
