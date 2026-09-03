# MailIQ v4.1 — Architecture Diagram

[← v4.1 README](README.md) · [Version Index](../INDEX.md)

> **Status:** HISTORICAL UNIFIED ARCHITECTURE / IMPORTANT DECISION AUTHORITY.

```mermaid
flowchart TB
    Events["Provider / application events"] --> Shared["Shared n8n workflow definitions"]
    Shared --> Guard["Tenant / account ownership + execution-context guard"]
    Guard <--> PG[("PostgreSQL authoritative OAuth + tenant state")]
    Guard --> Process["Shared processing logic"]
    Process --> Provider["Provider API operations"]
    Process --> Delivery["Tenant-selected delivery"]
    Process --> Ops["Audit / monitoring / failure handling"]
    Delivery --> Channels["WhatsApp · Telegram · Slack · Discord"]
    Ops <--> PG
```

## What changed

v4.1 rejects per-client workflow proliferation as the primary tenancy mechanism. The mature direction becomes **shared workflow definitions + tenant-scoped execution/context + PostgreSQL-backed authoritative provider state**.

## Why this matters

The archive ties this generation to an audit cycle with 14 findings. v4.1 is therefore the key transition architecture explaining several decisions later retained by v5.
