# ADR-002: Next.js + Adonis as two services in one monorepo

- **Status:** Accepted
- **Date:** 2026-11-24
- **Related Issue / Requirement:** M0 import, monorepo setup

## Context

Upstream is a Next.js 16 web app (~14k lines, `/api/*` mostly a ~280-line token-keeping proxy) and an AdonisJS 7 API (~8k lines plus ~6.5k lines of tests holding the real logic).

## Decision

Keep both as services in one pnpm monorepo: `apps/web`, `apps/api`, `packages/shared` (generated typed client, enums, DTOs: the only place web/API contracts live) and `packages/tokens` (brand tokens). One lockfile, Node 24 LTS, one CI that runs only affected packages; CI regenerates the typed client and fails on drift.

## Alternatives Considered

- **B. Collapse into one Next.js app:** one service, but 3–5 dev-weeks porting logic and tests with no user value, and MCP/worker would live inside Next.
- **C. Rewrite on dtu-compass's stack (FastAPI + Next):** a full rewrite.

## Consequences

A real API boundary for MCP, the worker, dtu-compass integration and a possible mobile client. Two services to run and two frameworks to learn (both TypeScript); sign-in is handled in the web proxy and verified again in the API.

## Revisit Trigger

The team shrinks to 1–2 people **and** both MCP and mobile are dropped → option B.
