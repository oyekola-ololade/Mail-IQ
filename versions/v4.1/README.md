# MailIQ v4.1 — Historical Unified Architecture

[← Version Index](../INDEX.md) · [Architecture Diagram](ARCHITECTURE.md)

**Status:** HISTORICAL — superseded by v5, but important decision authority  
**Primary surviving authority:** Unified Architecture v4.1

## Why v4.1 matters

v4.1 responds to a substantial audit cycle and is the generation where MailIQ's tenancy/workflow model changes in a way that strongly influences v5.

## Architecture

[Open the v4.1 architecture diagram →](ARCHITECTURE.md)

The diagram visualizes the key correction: shared n8n workflow definitions operating with tenant-scoped execution/ownership against PostgreSQL-backed authoritative provider state.

## Major architectural direction

- shared workflow definitions rather than per-client workflow proliferation;
- PostgreSQL-backed OAuth/provider state;
- tenant execution/context isolation;
- explicit response to **14 audit findings** recorded in the archive;
- stronger state-provenance and ownership boundaries.

## Rejected pattern

The architecture rejects using duplicated/generated workflow definitions per customer as the primary tenancy mechanism. Shared workflow definitions with tenant-scoped execution/context become the mature direction.

## Relationship to v5

v5 supersedes v4.1 as current architecture authority, but v4.1 remains important because it preserves the transition rationale behind the shared-workflow and state-isolation decisions.

## Workflow publication rule

Historical v4.1 workflow exports, if mapped confidently, belong under a historical/provenance path. They should not be mixed into `workflows/current-candidate/` without reconciliation against v5 decisions.

## Evidence boundary

**Supported:** unified architecture, audit-driven change rationale, shared workflow direction and PostgreSQL-backed tenancy/OAuth decisions.  
**Not supported:** current runtime verification or a complete public v4.1 workflow bundle.

## Media

Historical version. Architecture is documented; demo/screenshot evidence is not fabricated.
