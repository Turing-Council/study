# Turing Study: plan overview

Condensed from the council's platform plan (v4, 21 Nov 2026). Requirements (`01-requirements.md`) and architecture (`02-architecture.md`) land here during M0 and the holidays.

## Scope (V1)

Four pillars: **course hub** (one page per DTU course code), **exam practice** (past-paper archive, question bank, six practice modes, mock exams, spaced review, DTU grading), **notes** (uploads with moderation, attestation, CC BY-SA) and a **thesis & project board**. Borrowed from dtu-compass: "Report a problem" with a private feedback inbox, moderation rules, honest numbers, privacy-safe analytics, version history. V2: MCP access for AI assistants and dtu-compass integration.

Content is the critical path: no ISEP question banks are reusable, so the build is paired with a question builder, student uploads and question sprints.

## Architecture

- `apps/web`: Next.js 16 + Tailwind 4 + shadcn/ui with brand-kit tokens; backend-for-frontend so tokens never reach the browser.
- `apps/api`: AdonisJS 7 (exam engine, uploads, rate limits, question import) plus a worker (catalogue sync, malware scan, pruning).
- Postgres 18, Cloudflare R2 (EU) for files and encrypted backups, Keycloak ≥ 26.8 shared by the council ([ADR-003](../decisions/003-keycloak-identity-broker.md)).
- Hosting: Dokploy behind a Cloudflare Tunnel; images built in GitHub Actions and pushed to GHCR. Hostnames on `turingcouncil.com`: `study.`, `id.`, `study-test.`, `stats.`.

### Not used yet, and when to add it

| Tool | Add when |
|---|---|
| Redis | Postgres-backed rate limits or sessions get slow |
| Meilisearch | `pg_trgm` search gets slow |
| pgvector | semantic search is wanted |
| Queue service | the worker cron isn't enough |
| Kubernetes | never |

## Roadmap

| Milestone | Dates | Exit criteria |
|---|---|---|
| M0 Foundations | 24 Nov – 20 Dec | Test env deploys on merge; sign-in with a DTU email through Keycloak; brand correct; tests green after the auth rewrite; required checks enforced |
| M1 Internal beta | 4 – 22 Jan | Council members use it on 2 courses; no P1 bug for 7 days; main journey under 2 min |
| M2 Closed pilot | Feb – Mar | 3–5 pilot courses; ≥ 100 weekly active students; moderation median under 48 h; restore drill green |
| M3 Public launch | mid-April | ≥ 15 courses with content; 0 serious axe violations on key routes |

## Process

See [CONTRIBUTING.md](../../CONTRIBUTING.md) and [AGENTS.md](../../AGENTS.md): one issue = one agent run = one small PR, required CI as the gate, every PR reviewed by someone other than its author.
