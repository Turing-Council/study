# ADR-001: One-time import of AntiRecurso

- **Status:** Accepted
- **Date:** 2026-11-24
- **Related Issue / Requirement:** M0 import

## Context

AntiRecurso (NEI-ISEP, GPL-3.0) already covers about two thirds of our MVP: an exam engine with six modes, resume and idempotent grading, notes on S3, comments and reports, admin, a backend-for-frontend that keeps tokens server-side, and ~350 tests. We need to rebrand, re-scope to DTU and refactor freely.

## Decision

Copy upstream `dev` **once** into this repo (web `a875ca9` → `apps/web`, API `94a873c` → `apps/api`), not a fork. The import commit records both SHAs; attribution lives in `NOTICE.md`, the README and the About page. No upstream remote and no merging afterwards: NEI fixes are reviewed and ported by hand, logged in `UPSTREAM.md` (monthly scan, security fixes first). At import we strip NEI/ISEP branding and imagery, ISEP question banks, NEI server docs, CODEOWNERS, NEI reusable workflows and Coolify compose files, and squash the upstream migrations into one baseline.

## Alternatives Considered

- **GitHub fork:** easy upstream merges, but every refactor becomes a merge conflict and branding stays constrained.
- **Earlier demo repos:** not used; they diverge from upstream `dev`.
- **Rewrite:** throws away the best-tested part for no user-visible value.

## Consequences

We can refactor freely. We must actively watch upstream for security fixes. The repo stays GPL-3.0.

## Revisit Trigger

NEI ships a major rewrite worth re-importing.
