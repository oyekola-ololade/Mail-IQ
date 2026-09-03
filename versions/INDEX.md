# MailIQ — Version Archive

This directory documents MailIQ's actual surviving architecture/build lineage. It does not rewrite history into a cleaner sequence than the evidence supports.

## Interpretation rules

1. **v5.0 is current architecture authority**, not proof of a currently deployed runtime.
2. Historical files can explain why a decision changed but cannot overrule newer authority.
3. v4.2, v4.3 and the seat-isolation patch are preserved as **referenced-but-not-located** entries; their missing originals are not reconstructed as if recovered.
4. Workflow counts from different generations are not interchangeable. The historical 35/36-workflow design/build sets and the later 38-export candidate pool represent different artifact generations.
5. A workflow is only called current/verified after source identification, sanitization, import/topology review and representative execution evidence.

## Versions

- [v1.0](v1.0/README.md) — baseline product/system architecture.
- [v1.1](v1.1/README.md) — mostly/all-n8n workflow direction.
- [v2.2](v2.2/README.md) — explicit two-layer build and 36-workflow definition generation.
- [v3.0](v3.0/README.md) — Railway/state/OAuth correction.
- [v3.1](v3.1/README.md) — node-level workflow/backend implementation expansion.
- [v4.1](v4.1/README.md) — unified/shared-workflow architecture after audit findings.
- [v4.2](v4.2/README.md) — referenced; standalone original not located.
- [v4.3](v4.3/README.md) — referenced; standalone original not located.
- [Seat-isolation patch](seat-isolation-patch/README.md) — referenced patch folded into v5.
- [v5.0](v5.0/README.md) — current architecture authority and current-candidate workflow reconciliation.

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