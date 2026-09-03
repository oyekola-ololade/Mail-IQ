# MailIQ v4.1 — Unified Architecture & Workflow Record

**Version class:** HISTORICAL MAJOR ARCHITECTURE CORRECTION  
**Primary authority:** Unified Architecture v4.1  
**Importance:** response to 14 audit findings and direct predecessor to v5.

## Core architectural shift

v4.1 rejects the earlier pattern of proliferating workflow definitions per client and moves to **shared workflow definitions with tenant/client execution isolation**. It also reinforces PostgreSQL-backed OAuth/provider state and a clearer authoritative-state boundary.

## Key decisions

- shared workflow definitions replace per-client workflow replication;
- tenant/client context is isolated at execution/state level rather than by cloning whole workflow graphs;
- provider OAuth/token state remains database-backed;
- durable account/integration/subscription state becomes more explicit;
- the architecture is reorganized in response to audit findings rather than merely expanded cosmetically.

## Why this matters

This generation is where MailIQ's scaling model changes substantially. The system stops treating workflow duplication as the core tenancy mechanism and instead separates **workflow definition** from **tenant execution context**.

That decision is retained in v5 and is one of the strongest reasons older workflow-generation assumptions must not be treated as current.

## Workflow-system interpretation

A v4.1 workflow should be understood as part of a shared-definition system that reads/writes tenant-specific authoritative state. A complete provenance-mapped v4.1 JSON bundle is not currently represented as recovered in the public repository.

## Evidence status

| Area | Status |
|---|---|
| Unified Architecture v4.1 | SURVIVES / HISTORICAL |
| Audit-response decisions | SURVIVE / IMPORTANT |
| Shared workflow model | HISTORICAL DECISION RETAINED IN CURRENT DESIGN |
| Exact complete JSON bundle | NOT YET PROVEN/MAPPED |
| Demo/screenshots | no placeholders for historical versions |

## Supersession

Superseded by v5.0, but v4.1 remains a critical decision record because many v5 choices originate here.