# MailIQ v2.2 — Architecture Diagram

[← v2.2 README](README.md) · [Version Index](../INDEX.md)

> **Status:** HISTORICAL COMPLETE-BUILD GENERATION. The surviving v2.2 specification is associated with **36 workflow definitions**, n8n credential-oriented provider access and MinIO.

```mermaid
flowchart TB
    subgraph Product["Application / product layer"]
      UI["User / admin surface"]
      App["Application logic"]
    end
    subgraph Automation["Automation layer — 36 workflow definitions"]
      Router["Workflow routing"]
      Process["Email processing / intelligence"]
      Notify["Notification workflows"]
      Ops["Supporting workflows"]
    end
    Creds["n8n credential-oriented provider access"]
    Providers["Gmail / Outlook / external APIs"]
    DB[("Database state")]
    MinIO[("MinIO object storage")]
    Channels["Messaging destinations"]

    UI --> App --> Router
    Router --> Process --> Notify --> Channels
    Router --> Ops
    Automation --> Creds --> Providers
    Automation <--> DB
    Automation <--> MinIO
```

## Why this version is distinct

The **36-workflow** count belongs to this generation. It must not be merged with the later 35-workflow design set or the later 38-export candidate pool.

## Later corrections

- provider OAuth/token authority moved toward PostgreSQL;
- per-client/dynamic workflow assumptions were replaced by shared workflow definitions + tenant-scoped execution;
- MinIO was removed from the current v5 default architecture.
