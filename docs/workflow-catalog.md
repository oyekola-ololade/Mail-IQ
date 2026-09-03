# MailIQ Workflow Catalog — Current vs Historical

## Why this catalog exists

MailIQ has multiple surviving workflow generations. Counts from different folders describe different artifact sets and **must not be added together or treated as one verified deployment**.

The repository therefore separates:

1. a **35-workflow documented system/template design set** from the older primary build generation; and
2. a **38-export recovered later-generation pool** associated with the later MailIQ workflow generation and v5 reconstruction work.

Neither count, by itself, proves a currently deployed production system.

## Generation A — documented 35-workflow design set

This set contains **35 workflows and 676 nodes**:

- 19 system workflows / 204 nodes
- 16 child delivery templates / 472 nodes

### System workflows

| ID | Workflow | Nodes | Responsibility |
|---|---|---:|---|
| SW-01 | Onboarding Factory | 24 | Provisions tenant-scoped workflow state from a reusable template. |
| SW-02 | Paystack Webhook Handler | 11 | Receives and normalizes billing events. |
| SW-03 | Subscription Lifecycle | 17 | Applies subscription state transitions. |
| SW-04 | Billing Reconciliation | 9 | Reconciles provider events with internal billing state. |
| SW-05 | Payment Retry / Reminder | 8 | Coordinates bounded payment follow-up. |
| SW-06 | Usage Meter | 17 | Records usage signals for billing and operations. |
| SW-07 | Usage Reconciliation | 8 | Checks usage records against processing state. |
| SW-08 | Telegram Chat ID Capture | 8 | Pairs a Telegram destination with tenant context. |
| SW-09 | Slack OAuth Callback | 8 | Completes Slack workspace authorization. |
| SW-10 | Discord Bot Join Handler | 8 | Captures Discord delivery context. |
| SW-11 | Gmail Pub/Sub Receiver | 10 | Receives Gmail change notifications. |
| SW-12 | Outlook Graph Receiver | 12 | Receives Microsoft Graph change notifications. |
| SW-13 | Token Refresher | 11 | Refreshes provider tokens before expiry. |
| SW-14 | Gmail Watch Renewer | 8 | Renews Gmail watch registrations. |
| SW-15 | Outlook Subscription Renewer | 9 | Renews Microsoft Graph subscriptions. |
| SW-16 | Health Monitor | 11 | Inspects workflow and integration health. |
| SW-17 | Database Backup | 9 | Coordinates scheduled persistence backups. |
| SW-18 | Admin Alerts | 5 | Routes operational exceptions to an administrator. |
| SW-19 | Settings API | 11 | Reads and writes tenant configuration. |

### Tenant delivery templates

| ID | Provider → destination | Nodes |
|---|---|---:|
| T01 | Gmail → WhatsApp | 30 |
| T02 | Gmail → Telegram Personal | 30 |
| T03 | Gmail → Telegram Group | 30 |
| T04 | Gmail → Telegram Channel | 30 |
| T05 | Gmail → Slack Channel | 30 |
| T06 | Gmail → Slack DM | 30 |
| T07 | Gmail → Discord Channel | 30 |
| T08 | Gmail → Discord DM | 30 |
| T09 | Outlook → WhatsApp | 29 |
| T10 | Outlook → Telegram Personal | 29 |
| T11 | Outlook → Telegram Group | 29 |
| T12 | Outlook → Telegram Channel | 29 |
| T13 | Outlook → Slack Channel | 29 |
| T14 | Outlook → Slack DM | 29 |
| T15 | Outlook → Discord Channel | 29 |
| T16 | Outlook → Discord DM | 29 |

This set is useful design/evolution evidence. It should not be described as the uniquely authoritative current v5 runtime bundle without a fresh release-selection review.

## Generation B — 38 recovered later-generation exports

The later MailIQ archive contains **38 JSON workflow exports** spanning:

- onboarding/router and plan-specific onboarding;
- Free/Basic/Standard/Premium tier processors;
- multi-webhook routing;
- subscription lifecycle and billing reconciliation;
- notification, digest, quiet-hours and usage functions;
- Telegram, Slack, Discord, Gmail and Outlook integration lifecycle handlers;
- token refresh and provider-renewal workflows;
- health, backup, admin-alert, settings, purge/history and DLQ operations;
- conversational-agent and tool workflows for calendar, email search, settings, draft/send and token refresh.

This later set is the **candidate canonical pool for v5 reconciliation**, not automatically a verified current bundle. Every workflow still needs to be checked against the v5 architecture authority, sanitized for public release, and rerun where runtime claims matter.

## Count boundary

The archive contains at least 76 JSON artifacts across generations. Those files are evidence of substantial multi-version engineering work, not evidence that 76 workflows were simultaneously deployed.

## Public exports

Only representative, sanitized or explicitly historical files should be published here until individual release review is complete.

Current public examples:

- `workflows/sanitized/SW-01_Onboarding_Factory_SANITIZED.json`
- `workflows/historical/MailIQ_n8n_import_fixed.json`

## Release rule

A workflow should move into a future `workflows/current/` bundle only after:

1. architecture-generation identity is known;
2. secrets and environment-specific identifiers are removed;
3. JSON parses and imports successfully;
4. data/state contracts match the selected v5 authority;
5. critical expressions and branch behavior are inspected;
6. configured runtime verification exists for any behavior claimed as working.
