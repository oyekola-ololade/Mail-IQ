# MailIQ — Seat-Isolation Patch Architecture

[← Patch README](README.md) · [Version Index](../INDEX.md)

> **Status:** REFERENCED PATCH — ORIGINAL PATCH TEXT NOT LOCATED. The visual focuses only on the purpose supported by the archive: making tenant/account/seat ownership explicit and preventing ambiguous or cross-tenant state use.

```mermaid
flowchart TB
    Event["Incoming request / provider event"] --> Resolve["Resolve authenticated account / tenant / seat"]
    Resolve --> Ownership{"Ownership valid?"}
    Ownership -->|No| Reject["Reject / quarantine / operator path"]
    Ownership -->|Yes| Context["Create tenant-scoped execution context"]
    Context <--> PG[("Authoritative account + seat + integration state")]
    Context --> Shared["Shared workflow definition"]
    Shared --> Action["Provider / delivery / account action"]
    Action --> Persist["Persist result under same owner context"]
    Persist --> PG
```

## Supported architectural purpose

- explicit tenant/account/seat ownership resolution;
- scoped execution context before shared workflow actions;
- state writes tied back to the same authoritative owner boundary.

Exact historical SQL, node edits and migration statements are not invented because the standalone patch source was not recovered.
