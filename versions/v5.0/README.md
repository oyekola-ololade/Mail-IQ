# MailIQ v5.0 — Current Architecture Authority

[← Version Index](../INDEX.md) · [Architecture Diagram](ARCHITECTURE.md) · [38-Workflow Candidate Bundle](../../workflows/current-candidate/README.md)

**Status:** CURRENT ARCHITECTURE AUTHORITY · runtime bundle still under reconciliation / revalidation

## Current position

v5.0 is the architecture and system-decision authority for MailIQ. It does **not** mean every surviving workflow export has been proven to be a current v5 runtime artifact, and it does not mean the system is currently deployed.

MailIQ is currently presented as an **offline/pre-production multi-version SaaS engineering system** while workflow-generation mapping, state/reliability checks and sanitization are completed.

## Architecture

[Open the v5.0 architecture diagram →](ARCHITECTURE.md)

The diagram includes the application/control plane, PostgreSQL authoritative state, provider edge, delivery edge, and the seven current-candidate workflow subsystems containing the recovered 38 sanitized exports.

## Core architecture decisions

- Node.js/API boundary retained for application auth, OTP/JWT, dashboard/backend requests and application-facing logic.
- n8n retained for orchestration and third-party webhook processing.
- OAuth/provider token state belongs in PostgreSQL-backed authoritative state rather than dynamic per-user n8n credentials as the primary tenancy mechanism.
- shared workflow definitions + isolated tenant/client execution replace per-client workflow proliferation.
- mature service-network direction remains Railway; static/frontend direction moves toward Vercel.
- PgBouncer session pooling is the safer n8n configuration where prepared statements are involved.
- MinIO is removed from the current default design; platform backup plus optional `pg_dump`/rclone-style backup is preferred.
- external provider webhooks terminate directly at n8n where appropriate.
- queue mode, attachment storage and other scale complexity remain deferred until actual evidence/revenue requires them.
- execution pruning, error workflow, edge/rate limiting, monitoring and migrations are explicit architecture concerns.

## Current-candidate workflow pool

A later archive contains **38 workflow exports**. Sanitized public copies are grouped under [`../../workflows/current-candidate/`](../../workflows/current-candidate/README.md).

They are the candidate canonical pool for v5 reconciliation, not automatically 38 verified current runtime definitions.

See [WORKFLOW_INDEX.md](WORKFLOW_INDEX.md) for the subsystem map.

## Required promotion gate

Before a workflow can be described as `CURRENT VERIFIED` it needs:

1. source/generation identification;
2. secret, identifier and environment sanitization for public release;
3. valid JSON/import/topology checks;
4. data/state-contract review;
5. expression/branch inspection;
6. configured representative execution;
7. failure/retry/state-provenance evidence appropriate to its role.

## Historical reliability issue class

Previous inspection found identifier/state-reference mismatches capable of producing a dangerous pattern:

`workflow action succeeds → identifier captured → authoritative state update uses wrong reference → downstream steps continue → account can appear active while underlying state is incomplete`.

This class of defect is one reason v5 remains under hardening rather than being labelled production-ready.

## Current media

Unlike historical versions, the current version has explicit runtime-evidence locations:

- [Demo status / placeholder](../../evidence/current/demo/README.md)
- [Screenshot status / placeholder](../../evidence/current/screenshots/README.md)
- current architecture SVG and other system visuals live under `../../assets/`.

A placeholder must only be replaced by real v5/current evidence, never by an old-version screenshot relabelled as current.
