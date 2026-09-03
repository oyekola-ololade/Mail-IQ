# 01 — Onboarding / Plan Routing

**Subsystem status:** recovered later-generation workflows documented; public JSON publication/revalidation pending.

## Candidate workflows

- `Onboarding Router` — select the appropriate plan/onboarding path.
- `Free Onboarding` — Free-plan provisioning/state setup.
- `Basic Onboarding` — Basic-plan provisioning/state setup.
- `Standard Onboarding` — Standard-plan provisioning/state setup.
- `Premium Onboarding` — Premium-plan provisioning/state setup.
- `Business Onboarding` — Business-plan provisioning/state setup.

## State relationship

Onboarding is expected to establish or update authoritative account/tenant/integration state rather than merely return a successful workflow response.

## Historical reliability concern

Earlier MailIQ analysis found identifier-reference mismatches capable of allowing downstream continuation while authoritative state was incomplete. Any onboarding export promoted here must therefore verify identifier provenance and final account state explicitly.

## Publication gate

For each workflow add sanitized JSON plus input/state/output contract and current execution result before marking it verified.