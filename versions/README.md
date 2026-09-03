# MailIQ — Version Archive

This folder documents MailIQ's surviving architecture/build lineage. It preserves the evidence as it exists rather than forcing every generation into one supposedly canonical implementation.

[← Main README](../README.md) · [38-workflow current candidate bundle](../workflows/current-candidate/README.md)

## Versions

| Version / generation | Status | Architectural meaning | Record | Diagram |
|---|---|---|---|---|
| v1.0 | Historical | baseline architecture/product definition | [README](v1.0/README.md) | [architecture](v1.0/ARCHITECTURE.md) |
| v1.1 | Historical | workflow-heavy / mostly-n8n direction | [README](v1.1/README.md) | [architecture](v1.1/ARCHITECTURE.md) |
| v2.2 | Historical | two-layer build; 36-workflow generation; credential-oriented provider access; MinIO | [README](v2.2/README.md) | [architecture](v2.2/ARCHITECTURE.md) |
| v3.0 | Historical | Railway/state/OAuth correction; provider token state moved into PostgreSQL | [README](v3.0/README.md) | [architecture](v3.0/ARCHITECTURE.md) |
| v3.1 | Historical fallback | node-level workflow/backend implementation expansion | [README](v3.1/README.md) | [architecture](v3.1/ARCHITECTURE.md) |
| v4.1 | Historical decision authority | shared workflows + tenant execution isolation + PostgreSQL-backed OAuth/state | [README](v4.1/README.md) | [architecture](v4.1/ARCHITECTURE.md) |
| v4.2 | Referenced; original not located | changes later folded into v5 | [README](v4.2/README.md) | [known architecture envelope](v4.2/ARCHITECTURE.md) |
| v4.3 | Referenced; original not located | changes later folded into v5 | [README](v4.3/README.md) | [known architecture envelope](v4.3/ARCHITECTURE.md) |
| Seat-isolation patch | Referenced patch; original not located | tenant/seat ownership/isolation correction folded into v5 | [README](seat-isolation-patch/README.md) | [architecture](seat-isolation-patch/ARCHITECTURE.md) |
| v5.0 | **Current architecture authority** | hardened control/state/deployment/operations architecture | [README](v5.0/README.md) | [architecture](v5.0/ARCHITECTURE.md) |

## Interpretation rules

1. v5.0 is current architecture authority, not proof of a currently deployed runtime.
2. Historical files explain decisions and evolution but do not overrule newer authority.
3. v4.2, v4.3 and the seat-isolation patch remain explicitly labelled as referenced-but-not-located where their standalone originals are missing.
4. Historical 35/36-workflow counts and the later 38-export candidate pool are different artifact generations and must not be collapsed into one total.
5. Architecture diagrams are included for every version. When an original architecture source is missing, the diagram shows only the evidence-supported envelope/lineage and labels unknown deltas.
6. Historical versions do not receive fake runtime screenshots or demos.
7. A workflow becomes `CURRENT VERIFIED` only after source identification, sanitization, topology/import review, data/state-contract inspection and representative configured execution.

## Cross-version decision arc

- application/API responsibility became more explicit instead of pushing the entire product into n8n;
- OAuth/provider state moved toward PostgreSQL-backed authoritative state;
- per-client workflow proliferation gave way to shared workflow definitions with tenant-scoped execution/context;
- mature service infrastructure converged around Railway while current static/frontend direction uses Vercel;
- PgBouncer session pooling is preferred where n8n prepared statements require it;
- MinIO was removed from the current default architecture;
- monitoring, pruning, error handling, recovery and migrations became explicit architecture concerns.
