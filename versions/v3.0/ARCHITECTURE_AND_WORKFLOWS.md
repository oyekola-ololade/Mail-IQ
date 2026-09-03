# MailIQ v3.0 — Architecture & Workflow Record

**Version class:** HISTORICAL FINAL-ARCHITECTURE GENERATION  
**Primary authority:** Final Architecture v3.0

## Architectural direction

v3.0 is a major correction generation. It moved the system toward Railway-hosted services, PostgreSQL-backed OAuth/provider state, direct provider API use through HTTP Request nodes, and retained a Python processing component.

## Major corrections from v2.2

- OAuth/provider credentials and token state move toward PostgreSQL rather than dynamic n8n credential proliferation.
- Railway becomes the service-hosting direction.
- provider integrations are handled more explicitly through API/HTTP boundaries.
- Python processing remains part of the system rather than forcing all logic into n8n.
- the architecture begins to establish clearer ownership of durable state.

## Workflow-system interpretation

MailIQ remains a multi-workflow system in v3.0, but the important change is **how workflows obtain provider state and how application/runtime responsibility is divided**.

The current archive does not justify publishing a later workflow export under v3.0 solely because its topology looks similar. Provenance must be explicit.

## State boundary

The v3.0 direction is significant because provider/OAuth state begins to move out of workflow-definition-local credential assumptions and toward a durable database-backed source of truth. This directly anticipates the stronger state-authority decisions in v4.1/v5.0.

## Evidence status

| Area | Status |
|---|---|
| Final Architecture v3.0 | SURVIVES / HISTORICAL |
| Railway service direction | HISTORICAL DESIGN EVIDENCE |
| PostgreSQL OAuth direction | HISTORICAL DESIGN EVIDENCE / FOUNDATION OF CURRENT MODEL |
| Complete v3.0 JSON bundle | NOT YET PROVEN/MAPPED |
| Current runtime evidence | NO |
| Demo/screenshots | no placeholders for historical versions |

## Supersession

Superseded by v3.1 implementation-detail expansion, then v4.1 architectural unification.