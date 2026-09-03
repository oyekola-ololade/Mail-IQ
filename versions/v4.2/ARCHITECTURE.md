# MailIQ v4.2 — Known Architecture Envelope

[← v4.2 README](README.md) · [Version Index](../INDEX.md)

> **Status:** REFERENCED VERSION — STANDALONE ORIGINAL NOT LOCATED. This is **not** a reconstructed original v4.2 specification. It shows only the architecture envelope supported by adjacent v4.1/v5 evidence and marks the v4.2 delta as unknown.

```mermaid
flowchart LR
    V41["v4.1 known authority\nshared workflows + PostgreSQL OAuth + tenant isolation"]
    V42["v4.2 referenced generation\nEXACT DELTA UNKNOWN"]
    V5["v5.0 current authority\nhardened state / deployment / operations"]
    V41 --> V42 --> V5

    subgraph Envelope["Architecture envelope known to persist through the transition"]
      Shared["Shared workflow definitions"]
      State[("PostgreSQL authoritative state")]
      Isolation["Tenant-scoped execution / ownership"]
      Shared <--> State
      Shared --> Isolation
    end

    V42 -. "exact standalone changes not recovered" .-> Envelope
```

## What this diagram does and does not say

It preserves v4.2's place in the real lineage without pretending the missing original was recovered. No workflow count, exact infrastructure change, SQL migration, node change or standalone decision is invented.
