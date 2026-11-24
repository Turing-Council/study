# ADR-003: Keycloak as the council identity broker

- **Status:** Accepted
- **Date:** 2026-11-24
- **Related Issue / Requirement:** M0 Keycloak sign-in

## Context

Upstream uses ZITADEL. We need DTU sign-in (Entra ID over OIDC, or WAYF over SAML), a fallback restricted to DTU emails until DTU IT approves an app registration, and later MCP login (client metadata documents, resource indicators, dynamic registration). The council wants one login across Turing Study, dtu-compass, the website and the Discord bot.

## Decision

Keycloak **≥ 26.8** (pinned) at `id.turingcouncil.com`, one council realm, realm configuration as OpenTofu code in `infra/keycloak/` from M0. Clients: `study-web` (confidential, code flow + PKCE) and `study-api` (audience only). Until DTU approves, self-registration with email verification is restricted to `dtu.dk` / `student.dtu.dk` addresses in the registration flow. Use DTU's single-tenant Entra issuer, key users on `oid`, and enable "trust email" only after a linking spike. Store `sub`, email and name; never the student number.

## Alternatives Considered

- **ZITADEL (upstream):** already wired, but behind on CIMD and resource indicators; integration code is reworked anyway.
- **Logto:** most AI-first; unclear self-hosted CIMD and SAML support. Documented fallback.
- **authentik / Authelia / Ory / Better Auth:** missing features, too many services, or a library rather than a council-wide server.

## Consequences

~1.25–1.5 GB RAM and a heavy admin console (kept behind Cloudflare Access). Auth tests are rewritten against a Keycloak test realm or mock OIDC issuer. MCP flags are experimental and must be re-tested on every upgrade.

## Revisit Trigger

Keycloak's CIMD or resource-indicator flags are removed or break, or its RAM becomes a problem → re-test Logto.
