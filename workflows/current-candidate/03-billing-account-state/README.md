# 03 — Billing / Account State

**Subsystem status:** candidate workflows documented; public JSON publication/revalidation pending.

## Candidate workflows

- `SW-02 Multi-Webhook Router`
- `SW-03 Subscription Lifecycle`
- `SW-04 Billing Reconciliation`
- `SW-06 Usage Meter`
- `SW-19 Settings API`

## System role

This group coordinates state that should not be left implicit inside a single workflow execution:

- subscription/plan transitions;
- external billing reconciliation;
- usage accounting;
- settings/config access;
- shared webhook routing where applicable.

## Authoritative-state rule

PostgreSQL/application state is the authority for account/subscription/integration truth. A successful API/webhook step is not enough if the authoritative record is not correct.

## Verification needs

- subscription create/change/cancel paths;
- duplicate/replayed billing events;
- reconciliation after partial failure;
- usage increments without double counting;
- settings reads/writes scoped to the correct tenant;
- state mismatch surfaced to operations rather than silently marked successful.