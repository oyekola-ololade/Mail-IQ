# MailIQ v1.0 — Historical Baseline Architecture

[← Version Index](../INDEX.md) · [Architecture Diagram](ARCHITECTURE.md)

**Status:** HISTORICAL  
**Primary surviving authority:** Architecture Specification v1.0  
**Role in lineage:** baseline product/system definition.

## What this version represents

v1.0 is the earliest named architecture generation retained in the reconstructed archive. It establishes the original MailIQ product boundary before later workflow, tenancy, credential, state and infrastructure decisions were repeatedly revised.

## Architecture

[Open the v1.0 architecture diagram →](ARCHITECTURE.md)

The diagram is a historical explanatory model derived from the surviving v1.0 architecture record; it is not a recovered runtime screenshot.

## Architectural interpretation

Treat this version as the baseline from which later changes are measured, not as current implementation guidance. Later versions materially changed how application/backend responsibility, workflow orchestration, OAuth state, tenancy, deployment and operational controls were handled.

## Workflow interpretation

The surviving control record does not establish a current publishable v1.0 JSON bundle. Do not manufacture one from later workflow exports. Any historical workflow file subsequently mapped to v1.0 should be added only after provenance is verified.

## Decisions / changes relative to later generations

The importance of v1.0 is that later versions moved away from its early assumptions toward:

- more explicit n8n workflow decomposition;
- a clearer API/backend boundary;
- PostgreSQL-backed identity/OAuth state;
- shared workflow definitions rather than per-client replication;
- explicit reliability/operations controls.

## Evidence boundary

**Supported:** an early MailIQ architecture/product definition existed and is part of the project's genuine design lineage.  
**Not supported:** current runtime use, production readiness, a recovered complete v1.0 workflow bundle, or current infrastructure equivalence.

## Media

Historical version. It has architecture documentation, but there are **no fake demo/screenshot placeholders** for runtime evidence that does not exist.
