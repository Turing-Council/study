# Rules for AI coding agents

These rules apply to any agent working in this repository (Claude Code, Codex, Cursor, Copilot, …). Humans follow [`CONTRIBUTING.md`](CONTRIBUTING.md); everything there applies to agents too.

## Read before acting

- The plan is in [`docs/plan/`](docs/plan/README.md). Read the sections for the area you touch before changing it.
- Check [`docs/decisions/`](docs/decisions/) for ADRs that constrain the area.
- If the task conflicts with the plan or an ADR, or either is ambiguous, stop and ask. Don't guess. If the human decides, draft an ADR.

## Architecture rules (do not break)

- One service layer in `apps/api`, behind controllers and future MCP tools. No business logic in controllers or in `apps/web` route handlers.
- VineJS validators are the single schema source for request and response shapes.
- `packages/shared` is the only place web/API contracts live.
- User-generated and scraped text goes in fields named `*_untrusted`.
- Missing values are `null`; never store strings like `"None"`, `"No data"` or `"–"`.
- Never hand-edit generated files. Regenerate them with the `just` recipe.
- Sign-in tokens never reach the browser: `apps/web` is the backend-for-frontend.

## Hard limits

- Never push to `main`, force-push a shared branch, or merge a PR unless the human asks.
- Never commit secrets, tokens, `.env` files, real student data or exam PDFs. Use synthetic fixtures.
- Ask before touching: Keycloak realm config, S3/R2 policies, destructive migrations (drop or rename), `.github/workflows/` triggers or permissions, `infra/`.
- Never add a checkout of PR code to a `pull_request_target` workflow.
- A new dependency needs a reason in the PR; a new service or major dependency needs an ADR.

## How to work

- One issue = one agent run = one small PR (aim for < ~400 changed lines, excluding generated files and fixtures).
- Keep diffs minimal and on-task: no drive-by refactors, renames or reformatting.
- Bug fixes start with a failing regression test. Add or update tests with every behaviour change.
- Run lint, type checks and tests before claiming the work is done (once the scaffold lands: `just lint test`). Report failures honestly.
- Verify your own work, then have a second agent or a human review it before merge.
- Use Conventional Commit messages and PR titles (`feat(exams): …`, `fix(auth): …`). Fill in the PR template, including the AI-assistance line. Reference requirement IDs and close the issue (`Closes #N`).
