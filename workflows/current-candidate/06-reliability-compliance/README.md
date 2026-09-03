# 06 — Reliability / Compliance / Operations

**Subsystem status:** candidate workflows documented; public JSON publication/revalidation pending.

## Candidate workflows

- `SW-16 Health Monitor`
- `SW-17 Database Backup`
- `SW-18 Admin Alerts`
- `SW-21 Data Purge / GDPR`
- `SW-22 History Pruner`
- `SW-23 DLQ Reprocessor`

## System role

These workflows exist because operational correctness is part of the architecture, not a decorative layer around the happy path.

## Responsibilities

- detect degraded/failed system conditions;
- generate operator-visible alerts;
- preserve backup/recovery capability;
- enforce data purge/retention operations;
- prune execution/history data;
- recover or reprocess dead-lettered work under controlled rules.

## Verification needs

- health checks detect meaningful failures rather than only process uptime;
- backup artifact can actually be restored/tested;
- admin alert contains useful execution/context information;
- purge/prune operations are scoped and auditable;
- DLQ replay is idempotent and cannot duplicate already-applied side effects.