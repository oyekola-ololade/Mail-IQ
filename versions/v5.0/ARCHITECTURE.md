# MailIQ v5.0 — Current Architecture Diagram

[← v5.0 README](README.md) · [Version Index](../INDEX.md) · [38-workflow candidate bundle](../../workflows/current-candidate/README.md)

> **Status:** CURRENT ARCHITECTURE AUTHORITY. This is the v5 system model. It is not a claim that the whole system is currently deployed or that all 38 candidate exports have passed current configured-runtime verification.

```mermaid
flowchart TB
    subgraph Edge["External edge"]
      Gmail["Gmail + Pub/Sub"]
      Outlook["Outlook + Microsoft Graph"]
      Billing["Paystack events"]
      Messaging["WhatsApp · Telegram · Slack · Discord"]
    end

    subgraph Product["Application / control plane"]
      Frontend["Frontend / dashboard"]
      API["Node.js API\nauth · OTP/JWT · application requests"]
      PG[("PostgreSQL\nauthoritative users · tenants · OAuth · subscriptions · usage · operational state")]
      Redis["Redis / Upstash\nbounded OTP · rate-limit · revoked-token concerns"]
    end

    subgraph N8N["n8n shared orchestration"]
      Onboard["01 Onboarding\n6 candidate workflows"]
      Tier["02 Tier processors\n4"]
      State["03 Billing / account state\n5"]
      Notify["04 Notifications / delivery\n6"]
      Provider["05 Provider lifecycle\n5"]
      Reliability["06 Reliability / compliance\n6"]
      Agent["07 Conversational agent / tools\n6"]
    end

    Frontend --> API
    API <--> PG
    API <--> Redis
    API --> Onboard
    Gmail --> Provider
    Outlook --> Provider
    Billing --> State
    Provider <--> PG
    Provider --> Tier
    Tier <--> PG
    Tier --> Notify
    State <--> PG
    State --> Notify
    Notify --> Messaging
    Reliability <--> PG
    Reliability --> Notify
    Agent <--> PG
    Agent --> Provider
    Agent --> Notify
    Onboard <--> PG
    Onboard --> Provider
    Onboard --> State
```

## v5 architectural principles

- **Shared workflow definitions**, not per-client workflow proliferation, are the mature tenancy direction.
- PostgreSQL owns authoritative tenant/account/provider-token/subscription state.
- n8n orchestrates workflows and third-party webhook processing rather than becoming the sole application backend.
- external provider webhooks can terminate directly at n8n where appropriate.
- Railway remains the mature service-network direction; static/frontend direction can use Vercel.
- PgBouncer session pooling is preferred where prepared statements make transaction pooling unsafe for n8n.
- MinIO is not part of the current default architecture.
- reliability workflows—health, backup, alerts, data purge, history pruning and DLQ recovery—are part of the architecture, not afterthoughts.

## Current workflow visibility

The sanitized public candidate pool is grouped under [`../../workflows/current-candidate/`](../../workflows/current-candidate/README.md). Sanitized does **not** mean runtime-verified.
