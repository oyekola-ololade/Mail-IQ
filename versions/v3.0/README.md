# MailIQ v3.0 — Historical State & Infrastructure Correction

[← Version Table of Contents](../TABLE_OF_CONTENTS.md) · [Architecture Diagram](ARCHITECTURE.md)

**Status:** HISTORICAL  
**Primary surviving authority:** Final Architecture v3.0

## Architectural direction

v3.0 is a major correction generation. The reconstructed archive records:

- Railway-only service direction for the main service environment;
- OAuth/provider token state moved into PostgreSQL;
- provider APIs consumed through workflow HTTP Request patterns rather than dynamic n8n credential creation as the primary tenancy mechanism;
- the Python processor retained.

## Architecture

[Open the v3.0 architecture diagram →](ARCHITECTURE.md)

The diagram shows the Railway-oriented service environment, PostgreSQL-backed OAuth state, n8n provider HTTP adapters and retained Python processing layer.

## Why this changed the system

The shift of OAuth/token state into PostgreSQL is one of MailIQ's most important architectural corrections. It establishes a clearer authoritative state boundary and reduces the risk created by proliferating per-user dynamic credentials inside the orchestration layer.

## Workflow relationship

Workflow orchestration remains central, but workflows increasingly consume state owned by the database/application architecture rather than becoming the authority for identity and integration state themselves.

## Infrastructure relationship

This generation is part of the convergence toward Railway-hosted services that continues into later architecture. v5 later separates static/frontend hosting toward Vercel while retaining mature service-network concerns around Railway.

## Evidence boundary

**Supported:** the stated v3.0 architectural corrections and surviving architecture authority.  
**Not supported:** a complete public v3.0 workflow bundle, current deployment, or production verification.

## Media

Historical version. Architecture is documented; demo/screenshot evidence is not fabricated.
