# MailIQ v4.3 — Known Architecture Envelope

[← v4.3 README](README.md) · [Version Index](../INDEX.md)

> **Status:** REFERENCED VERSION — STANDALONE ORIGINAL NOT LOCATED. The diagram records only evidence-supported continuity and the location of the unknown v4.3 delta.

```mermaid
flowchart LR
    V41["v4.1\nshared-workflow / PostgreSQL state correction"] --> V42["v4.2\nreferenced · delta unknown"]
    V42 --> V43["v4.3\nreferenced · delta unknown"]
    V43 --> Seat["Seat-isolation correction\nreferenced patch"]
    Seat --> V5["v5.0\ncurrent architecture authority"]

    subgraph Known["Known mature architecture direction"]
      Shared["Shared n8n definitions"]
      PG[("PostgreSQL OAuth / tenant state")]
      Ownership["Tenant / seat ownership boundaries"]
      Ops["Hardening / operational controls"]
      Shared <--> PG
      Shared --> Ownership
      Ownership --> Ops
    end

    V43 -. "exact standalone v4.3 changes unavailable" .-> Known
```

## Evidence discipline

The lineage position is supported; the standalone v4.3 workflow inventory and exact changes are not. This page exists so the version still has a visual architecture record without fabricating the missing source.
