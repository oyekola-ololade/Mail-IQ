# MailIQ — Version Archive

This directory documents MailIQ's actual surviving architecture/build lineage. It does not rewrite history into a cleaner sequence than the evidence supports.

[← Main README](../README.md) · [Repository Index](../INDEX.md) · [38-workflow candidate bundle](../workflows/current-candidate/README.md)

## Interpretation rules

1. **v5.0 is current architecture authority**, not proof of a currently deployed runtime.
2. Historical files can explain why a decision changed but cannot overrule newer authority.
3. v4.2, v4.3 and the seat-isolation patch are preserved as **referenced-but-not-located** entries; their missing originals are not reconstructed as if recovered.
4. Workflow counts from different generations are not interchangeable. The historical 35/36-workflow design/build sets and the later 38-export candidate pool represent different artifact generations.
5. A workflow is only called current/verified after source identification, sanitization, import/topology review and representative execution evidence.
6. **Every version has an architecture page.** For missing-original versions, that page shows only the evidence-supported architectural envelope/lineage and labels unknown deltas explicitly.

## Versions

| Version | Status | README | Architecture diagram |
|---|---|---|---|
| v1.0 | Historical baseline | [open](v1.0/README.md) | [diagram](v1.0/ARCHITECTURE.md) |
| v1.1 | Historical workflow-heavy | [open](v1.1/README.md) | [diagram](v1.1/ARCHITECTURE.md) |
| v2.2 | Historical two-layer / 36-workflow generation | [open](v2.2/README.md) | [diagram](v2.2/ARCHITECTURE.md) |
| v3.0 | Historical state/infrastructure correction | [open](v3.0/README.md) | [diagram](v3.0/ARCHITECTURE.md) |
| v3.1 | Historical node-level build expansion | [open](v3.1/README.md) | [diagram](v3.1/ARCHITECTURE.md) |
| v4.1 | Historical unified/shared-workflow authority | [open](v4.1/README.md) | [diagram](v4.1/ARCHITECTURE.md) |
| v4.2 | Referenced; standalone original not located | [open](v4.2/README.md) | [known architecture envelope](v4.2/ARCHITECTURE.md) |
| v4.3 | Referenced; standalone original not located | [open](v4.3/README.md) | [known architecture envelope](v4.3/ARCHITECTURE.md) |
| Seat-isolation patch | Referenced patch; standalone original not located | [open](seat-isolation-patch/README.md) | [patch architecture](seat-isolation-patch/ARCHITECTURE.md) |
| v5.0 | **Current architecture authority** | [open](v5.0/README.md) | [diagram](v5.0/ARCHITECTURE.md) |

## Cross-version decisions

The most important changes across the lineage are:

- preserve a Node.js/API application boundary rather than making n8n the entire backend;
- move OAuth/token state from dynamic n8n credentials toward PostgreSQL-backed authoritative state;
- replace per-client workflow replication with shared workflow definitions and isolated tenant execution/context;
- converge mature service infrastructure around Railway while using Vercel for static/frontend direction;
- use PgBouncer session pooling where n8n prepared statements require it;
- remove MinIO from the current default architecture;
- let third-party webhooks terminate directly at n8n where appropriate;
- defer nonessential scale complexity until evidence/revenue requires it;
- treat pruning, error workflows, monitoring, migrations and recovery as architecture, not afterthoughts.

See the root [workflow catalog](../docs/workflow-catalog.md), [multi-workflow map](../docs/MULTI_WORKFLOW_SYSTEM_MAP.md) and [reliability record](../docs/reliability-and-rebuild.md) for cross-version detail.
