# Turing Study

A study platform for DTU students, run by [Turing Council](https://github.com/Turing-Council): course hubs, past-paper practice, student notes, and a thesis and project board.

> **Status:** M0 Foundations (Nov–Dec 2026). No application code yet. The first big PR is the one-time import of AntiRecurso (see [ADR-001](docs/decisions/001-one-time-import-of-antirecurso.md)).

## Four pillars

1. **Course hub**: one page per DTU course code with ECTS, exam slot and previous codes.
2. **Exam practice**: past papers with solutions, a question bank, practice modes, mock exams, spaced review and DTU grading.
3. **Notes**: upload, browse and download notes by course, with moderation and CC BY-SA.
4. **Thesis & project board**: ideas from professors, research groups, companies and students.

## Stack

pnpm monorepo: `apps/web` (Next.js) + `apps/api` (AdonisJS) + `packages/shared` + `packages/tokens`, Postgres, Cloudflare R2, Keycloak as the council identity broker. See [docs/plan](docs/plan/README.md) and [ADRs](docs/decisions/README.md).

## Contributing

Read [CONTRIBUTING.md](CONTRIBUTING.md). Using a coding agent? It follows [AGENTS.md](AGENTS.md). Work is tracked on the org's **Turing Study** GitHub Project and in [milestones](https://github.com/Turing-Council/study/milestones).

## Licence

GPL-3.0. Based on [AntiRecurso](https://github.com/Nucleo-Estudantes-Informatica-ISEP/antirecurso) by NEI-ISEP; see [NOTICE.md](NOTICE.md).
