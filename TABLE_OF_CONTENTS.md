# MailIQ — Table of Contents

> **Current truth:** substantial multi-version email-intelligence SaaS engineering archive. v5.0 is the current architecture authority; the current runtime bundle is still being reconciled and revalidated. MailIQ is offline and is not presented as a live paying-customer SaaS.

## Start here

- [Main project README](README.md)
- [Version archive](versions/TABLE_OF_CONTENTS.md)
- [Current 38-workflow candidate bundle](workflows/current-candidate/README.md)
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

| Version / generation | Status | README | Architecture |
|---|---|---|---|
| v1.0 | Historical baseline | [README](versions/v1.0/README.md) | [Diagram](versions/v1.0/ARCHITECTURE.md) |
| v1.1 | Historical workflow-heavy direction | [README](versions/v1.1/README.md) | [Diagram](versions/v1.1/ARCHITECTURE.md) |
| v2.2 | Historical 36-workflow build generation | [README](versions/v2.2/README.md) | [Diagram](versions/v2.2/ARCHITECTURE.md) |
| v3.0 | Historical state/infrastructure correction | [README](versions/v3.0/README.md) | [Diagram](versions/v3.0/ARCHITECTURE.md) |
| v3.1 | Historical node-level build expansion | [README](versions/v3.1/README.md) | [Diagram](versions/v3.1/ARCHITECTURE.md) |
| v4.1 | Historical shared-workflow/tenant-isolation authority | [README](versions/v4.1/README.md) | [Diagram](versions/v4.1/ARCHITECTURE.md) |
| v4.2 | Referenced; original not located | [README](versions/v4.2/README.md) | [Known architecture envelope](versions/v4.2/ARCHITECTURE.md) |
| v4.3 | Referenced; original not located | [README](versions/v4.3/README.md) | [Known architecture envelope](versions/v4.3/ARCHITECTURE.md) |
| Seat-isolation patch | Referenced patch; original not located | [README](versions/seat-isolation-patch/README.md) | [Patch architecture envelope](versions/seat-isolation-patch/ARCHITECTURE.md) |
| v5.0 | **Current architecture authority** | [README](versions/v5.0/README.md) | [Diagram](versions/v5.0/ARCHITECTURE.md) |

## Current workflow bundle

The public current-candidate bundle is organized as seven cooperating subsystems:

1. [`01-onboarding/`](workflows/current-candidate/01-onboarding/) — 6 workflows
2. [`02-tier-processors/`](workflows/current-candidate/02-tier-processors/) — 4 workflows
3. [`03-billing-account-state/`](workflows/current-candidate/03-billing-account-state/) — 5 workflows
4. [`04-notifications-delivery/`](workflows/current-candidate/04-notifications-delivery/) — 6 workflows
5. [`05-provider-lifecycle/`](workflows/current-candidate/05-provider-lifecycle/) — 5 workflows
6. [`06-reliability-compliance/`](workflows/current-candidate/06-reliability-compliance/) — 6 workflows
7. [`07-agent-tools/`](workflows/current-candidate/07-agent-tools/) — 6 workflows

Total: **38 sanitized candidate workflow exports** when publication is complete.

## Media

Only the current version receives missing-demo/screenshot placeholders. Historical versions still receive architecture diagrams and detailed documentation, but no fake runtime media.

- [Current demo placeholder](evidence/current/demo/README.md)
- [Current screenshots placeholder](evidence/current/screenshots/README.md)
