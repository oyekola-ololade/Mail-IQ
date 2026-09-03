# MailIQ — Repository Index

> **Current truth:** substantial multi-version email-intelligence SaaS engineering archive. v5.0 is the current architecture authority; the current runtime bundle is still being reconciled and revalidated. MailIQ is offline and is not presented as a live paying-customer SaaS.

## Start here

- [Main project README](README.md)
- [Version archive](versions/INDEX.md)
- [Sanitized 38-workflow current-candidate bundle](workflows/current-candidate/README.md)
- [Multi-workflow system map](docs/MULTI_WORKFLOW_SYSTEM_MAP.md)
- [Workflow catalog](docs/workflow-catalog.md)
- [Architecture](docs/architecture.md)
- [Database/state model](docs/database.md)
- [Integrations](docs/integrations.md)
- [Testing](docs/testing.md)
- [Security](docs/security.md)
- [Operations](docs/operations.md)
- [Reliability / rebuild record](docs/reliability-and-rebuild.md)
- [Evidence register](docs/evidence-register.md)
- [Changelog](CHANGELOG.md)

## Version lineage

Every version/generation has a README and an architecture diagram. For v4.2, v4.3 and the seat-isolation patch, the architecture page is deliberately labelled as a reconstructed/known envelope because the standalone original source was not recovered.

| Version / generation | Status | Primary architectural meaning | Record | Diagram |
|---|---|---|---|---|
| v1.0 | Historical | baseline architecture/product definition | [README](versions/v1.0/README.md) | [architecture](versions/v1.0/ARCHITECTURE.md) |
| v1.1 | Historical | mostly/all-n8n workflow direction | [README](versions/v1.1/README.md) | [architecture](versions/v1.1/ARCHITECTURE.md) |
| v2.2 | Historical | two-layer build; 36 workflow definitions; n8n credential assumptions; MinIO | [README](versions/v2.2/README.md) | [architecture](versions/v2.2/ARCHITECTURE.md) |
| v3.0 | Historical | Railway services; OAuth state in PostgreSQL; Python processor retained | [README](versions/v3.0/README.md) | [architecture](versions/v3.0/ARCHITECTURE.md) |
| v3.1 | Historical fallback | node-level workflow/backend expansion | [README](versions/v3.1/README.md) | [architecture](versions/v3.1/ARCHITECTURE.md) |
| v4.1 | Historical decision authority | shared workflows + PostgreSQL OAuth + tenant execution isolation | [README](versions/v4.1/README.md) | [architecture](versions/v4.1/ARCHITECTURE.md) |
| v4.2 | Referenced; original not located | changes later folded into v5 | [README](versions/v4.2/README.md) | [known envelope](versions/v4.2/ARCHITECTURE.md) |
| v4.3 | Referenced; original not located | changes later folded into v5 | [README](versions/v4.3/README.md) | [known envelope](versions/v4.3/ARCHITECTURE.md) |
| Seat-isolation patch | Referenced; original not located | tenant/seat state-isolation corrections later folded into v5 | [README](versions/seat-isolation-patch/README.md) | [patch architecture](versions/seat-isolation-patch/ARCHITECTURE.md) |
| v5.0 | **CURRENT architecture authority** | hardened state/deployment/operations architecture | [README](versions/v5.0/README.md) | [architecture](versions/v5.0/ARCHITECTURE.md) |

## Current multi-workflow visibility

The public repository now exposes the complete **38-export sanitized candidate pool** by subsystem:

```text
workflows/current-candidate/
├── 01-onboarding/                 6 workflows
├── 02-tier-processors/            4 workflows
├── 03-billing-account-state/      5 workflows
├── 04-notifications-delivery/     6 workflows
├── 05-provider-lifecycle/         5 workflows
├── 06-reliability-compliance/     6 workflows
└── 07-agent-tools/                6 workflows
```

These JSON files are **sanitized candidate evidence**, not 38 verified production workflows. Credential bindings and old environment-specific values are removed/replaced, but configured import/runtime verification remains a separate promotion gate.

Start at [`workflows/current-candidate/README.md`](workflows/current-candidate/README.md).

## Media rule

Historical versions receive architecture diagrams because architecture is part of the version record. They do **not** receive fake runtime demo/screenshot evidence.

Only the current version receives missing-media placeholders for evidence that must come from a real current run:

- [Current demo placeholder](evidence/current/demo/README.md)
- [Current screenshot placeholder](evidence/current/screenshots/README.md)

When real current evidence is produced, replace placeholder text with the real artifact and record the date/version/test context.
