# MailIQ — Repository Index

> **Current truth:** substantial multi-version email-intelligence SaaS engineering archive. v5.0 is the current architecture authority; the current runtime bundle is still being reconciled and revalidated. MailIQ is offline and is not presented as a live paying-customer SaaS.

## Start here

- [Main project README](README.md)
- [Version archive](versions/INDEX.md)
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

| Version / generation | Status | Primary architectural meaning | GitHub record |
|---|---|---|---|
| v1.0 | Historical | baseline architecture/product definition | [open](versions/v1.0/README.md) |
| v1.1 | Historical | mostly/all-n8n workflow direction | [open](versions/v1.1/README.md) |
| v2.2 | Historical | two-layer build; 36 workflow definitions; n8n credential assumptions; MinIO | [open](versions/v2.2/README.md) |
| v3.0 | Historical | Railway services; OAuth state in PostgreSQL; Python processor retained | [open](versions/v3.0/README.md) |
| v3.1 | Historical fallback | node-level workflow/backend expansion | [open](versions/v3.1/README.md) |
| v4.1 | Historical decision authority | shared workflows + PostgreSQL OAuth + tenant execution isolation | [open](versions/v4.1/README.md) |
| v4.2 | Referenced; original not located | changes later folded into v5 | [open](versions/v4.2/README.md) |
| v4.3 | Referenced; original not located | changes later folded into v5 | [open](versions/v4.3/README.md) |
| Seat-isolation patch | Referenced; original not located | tenant/seat state-isolation corrections later folded into v5 | [open](versions/seat-isolation-patch/README.md) |
| v5.0 | **CURRENT architecture authority** | hardened state/deployment/operations architecture | [open](versions/v5.0/README.md) |

## Current multi-workflow visibility

The public repository intentionally separates **version documentation** from **publishable workflow exports**.

Current-candidate workflow groups belong under:

```text
workflows/current-candidate/
├── 01-onboarding/
├── 02-tier-processors/
├── 03-billing-account-state/
├── 04-notifications-delivery/
├── 05-provider-lifecycle/
├── 06-reliability-compliance/
└── 07-agent-tools/
```

`05-provider-lifecycle/` already contains publishable candidate exports. Other groups should only receive JSON after source-generation identification, sanitization, import validation and truth-boundary review. Missing public JSON does **not** mean the subsystem never existed; the version/workflow records describe what survives in the private archive and what remains pending publication.

## Media rule

Only the current version receives missing-media placeholders. Historical versions do not get fake demo or screenshot folders.

- [Current demo placeholder](evidence/current/demo/README.md)
- [Current screenshot placeholder](evidence/current/screenshots/README.md)

When real current evidence is produced, replace the placeholder text with the real artifact and record the date/version/test context.