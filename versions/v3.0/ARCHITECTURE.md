# MailIQ v3.0 — Architecture Diagram

[← v3.0 README](README.md) · [Version Index](../INDEX.md)

> **Status:** HISTORICAL STATE / INFRASTRUCTURE CORRECTION.

```mermaid
flowchart TB
    UI["Product / user surface"] --> API["Application / API service"]
    API <--> PG[("PostgreSQL authoritative account + OAuth/token state")]
    API --> N8N["n8n orchestration"]
    N8N <--> PG
    N8N --> HTTP["HTTP Request provider adapters"]
    HTTP --> Gmail["Gmail API"]
    HTTP --> Graph["Microsoft Graph"]
    N8N --> Python["Retained Python processing service"]
    Python <--> PG
    N8N --> Delivery["Messaging / downstream delivery"]

    subgraph Railway["Railway-oriented service environment"]
      API
      PG
      N8N
      Python
    end
```

## Architectural correction

v3.0 moves provider OAuth/token state into PostgreSQL-backed authoritative state and uses provider APIs through workflow HTTP Request patterns rather than treating dynamic n8n credentials as the primary tenancy mechanism.

## Evidence boundary

This diagram represents the surviving v3.0 architectural direction. It does not claim a complete public v3.0 workflow bundle or a currently deployed Railway environment.
