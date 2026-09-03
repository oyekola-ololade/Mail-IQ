# MailIQ — Version Archive Table of Contents

This directory documents MailIQ's actual surviving architecture/build lineage. It does not rewrite history into a cleaner sequence than the evidence supports.

## Interpretation rules

1. **v5.0 is current architecture authority**, not proof of a currently deployed runtime.
2. Historical files can explain why a decision changed but cannot overrule newer authority.
3. v4.2, v4.3 and the seat-isolation patch are preserved as **referenced-but-not-located** entries; their missing originals are not reconstructed as if recovered.
4. Workflow counts from different generations are not interchangeable. Historical 35/36-workflow design/build sets and the later 38-export candidate pool represent different artifact generations.
5. Every version/generation has an architecture diagram or, when its original is missing, a clearly labelled evidence-bounded architecture envelope.
6. Historical versions do not receive fake demo/screenshot placeholders.

## Versions

| Version | README | Architecture | Role |
|---|---|---|---|
| v1.0 | [README](v1.0/README.md) | [Architecture](v1.0/ARCHITECTURE.md) | baseline product/system architecture |
| v1.1 | [README](v1.1/README.md) | [Architecture](v1.1/ARCHITECTURE.md) | workflow-heavy / mostly-n8n direction |
| v2.2 | [README](v2.2/README.md) | [Architecture](v2.2/ARCHITECTURE.md) | explicit two-layer 36-workflow build generation |
| v3.0 | [README](v3.0/README.md) | [Architecture](v3.0/ARCHITECTURE.md) | Railway/state/OAuth correction |
| v3.1 | [README](v3.1/README.md) | [Architecture](v3.1/ARCHITECTURE.md) | node-level workflow/backend expansion |
| v4.1 | [README](v4.1/README.md) | [Architecture](v4.1/ARCHITECTURE.md) | shared workflows + tenant/state isolation |
| v4.2 | [README](v4.2/README.md) | [Architecture envelope](v4.2/ARCHITECTURE.md) | referenced; standalone original not located |
| v4.3 | [README](v4.3/README.md) | [Architecture envelope](v4.3/ARCHITECTURE.md) | referenced; standalone original not located |
| Seat-isolation patch | [README](seat-isolation-patch/README.md) | [Architecture envelope](seat-isolation-patch/ARCHITECTURE.md) | referenced patch later folded into v5 |
| v5.0 | [README](v5.0/README.md) | [Architecture](v5.0/ARCHITECTURE.md) | current architecture authority |

## Cross-version decisions

- Node.js/API application boundary retained instead of making n8n the entire backend.
- OAuth/token state moved from dynamic workflow credentials toward PostgreSQL-backed authoritative state.
- Per-client workflow proliferation replaced by shared definitions with isolated tenant execution/context.
- Railway became the mature service-network direction; static/frontend direction moved toward Vercel in v5.
- PgBouncer session pooling used where n8n prepared statements require it.
- MinIO removed from the current default architecture.
- Reliability controls such as pruning, error workflows, monitoring, migrations and recovery became explicit architecture concerns.

Return to the [root Table of Contents](../TABLE_OF_CONTENTS.md).