# MailIQ — Current-Candidate Workflow System

**Status:** recovered later-generation candidate pool for v5 reconciliation. Not all groups have public JSON yet; not all recovered exports are fully revalidated.

## Subsystems

1. [`01-onboarding/`](01-onboarding/README.md) — onboarding router + Free/Basic/Standard/Premium/Business onboarding.
2. [`02-tier-processors/`](02-tier-processors/README.md) — Free/Basic/Standard/Premium processing paths.
3. [`03-billing-account-state/`](03-billing-account-state/README.md) — webhook routing, subscription lifecycle, billing reconciliation, usage and settings state.
4. [`04-notifications-delivery/`](04-notifications-delivery/README.md) — notification, digest, quiet-hours and communication integration workflows.
5. [`05-provider-lifecycle/`](05-provider-lifecycle/) — Gmail/Outlook receivers and token/subscription renewal workflows; public JSON already present.
6. [`06-reliability-compliance/`](06-reliability-compliance/README.md) — health, backup, admin alerts, purge, pruning and DLQ recovery.
7. [`07-agent-tools/`](07-agent-tools/README.md) — conversational agent + calendar/email/settings/draft-send/token tools.

See [`../../versions/v5.0/WORKFLOW_INDEX.md`](../../versions/v5.0/WORKFLOW_INDEX.md) for the 38-export inventory and system interaction map.

## Publication rule

A missing JSON in this public tree means **publication/verification pending**, not “the subsystem never existed.” Before an export is added here it must be mapped to the correct generation, sanitized, structurally reviewed and assigned an honest verification state.