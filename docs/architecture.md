# MailIQ architecture

## Status and scope

This document represents the current architecture model recovered from the MailIQ v5 specification, the 35-workflow canonical set, earlier exports, and the logic audit. MailIQ is offline; the model explains system intent and inspected evidence, not a running production deployment.

## Four interacting planes

| Plane | Responsibilities | Primary state |
|---|---|---|
| Provider edge | Gmail/Outlook events, OAuth grants, watches, Graph subscriptions | Provider event IDs, cursors, expiry, subscription state |
| Tenant control | Identity, account ownership, configuration, provisioning, billing | Clients, team members, OAuth tokens, platform mappings, subscriptions |
| Intelligence runtime | Ingest, deduplicate, classify, score, extract, route, queue | Email log, tenant policy, AI output, message queue |
| Operations | Delivery results, usage, reconciliation, health, alerts, backup | Failed jobs, webhook events, reconciliation logs, usage ledger |

## Data and control flow

```mermaid
flowchart LR
    subgraph Edge["Provider edge"]
      GM["Gmail watch"]
      MS["Graph subscription"]
      OA["OAuth grant"]
    end

    subgraph Control["Control plane"]
      API["API + auth"]
      DB[("Tenant state")]
      F["Workflow factory"]
      PAY["Paystack events"]
    end

    subgraph Run["Runtime"]
      RX["Provider receivers"]
      DEDUPE["Event dedup"]
      AI["Email intelligence"]
      R["Tenant route"]
      Q[("Message queue")]
    end

    subgraph Ops["Delivery + operations"]
      CH["Channel providers"]
      REC["Health + reconciliation"]
      HUMAN["Operator authority"]
    end

    GM --> RX
    MS --> RX
    OA <--> API
    PAY --> API
    API <--> DB
    API --> F
    F --> R
    RX --> DEDUPE
    DB <--> DEDUPE
    DEDUPE --> AI
    DB <--> AI
    AI --> R
    R --> Q --> CH
    CH -->|delivery receipt / failure| REC
    REC -->|retry| Q
    REC -->|repair state| DB
    REC --> HUMAN
    HUMAN -->|approve / correct| API
```

## Why several arrows run both ways

- **OAuth:** the application initiates consent; providers return grants, expiry, revocation, and refresh results.
- **Subscriptions:** MailIQ creates watches/subscriptions; Gmail and Microsoft return lifecycle state and later event notifications.
- **Tenant state:** runtime reads ownership and policy, then writes processing, usage, and failure outcomes back.
- **Delivery:** MailIQ submits a signal; the channel provider returns success, failure, or retry information.
- **Reconciliation:** drift is detected after the main path and fed back into queue, billing, token, or tenant state.
- **Human authority:** an operator can resolve provider pairing, billing, credential, or repeated-failure states that should not be “fixed” autonomously.

## Canonical workflow topology

```mermaid
flowchart TB
    Lifecycle["Onboarding + subscription<br/>SW-01–SW-07"]
    Pairing["Channel pairing<br/>SW-08–SW-10"]
    Provider["Provider lifecycle<br/>SW-11–SW-15"]
    Ops["Operations<br/>SW-16–SW-19"]
    Templates["16 delivery templates<br/>T01–T16"]
    State[("Tenant + operational state")]

    Lifecycle <--> State
    Pairing <--> State
    Provider <--> State
    Ops <--> State
    State --> Templates
    Templates --> Ops
```

The canonical set contains 19 system workflows and 16 delivery templates. See [workflow-catalog.md](workflow-catalog.md) for every workflow and node count.

## Persistence rules recovered from v5

- OAuth and platform tokens are designed for encrypted-at-rest storage.
- Runtime executions should read token state directly from PostgreSQL; workflow static data must not become the token authority.
- Inserts for events and queue state should use conflict-aware idempotency, not a select-then-insert race.
- Records supporting either a client or a team member use an exactly-one-owner constraint.
- The unified message queue replaces separate pending/digest queues to reduce double-send risk.
- Webhook events also provide a reconciliation cursor through processed/unprocessed state.
- Refresh tokens are rotated; reuse of an already-used token is intended to revoke the chain and force login.

## Representative email-processing path

```mermaid
sequenceDiagram
    participant P as Gmail / Outlook
    participant R as Receiver
    participant D as Tenant state
    participant A as Intelligence
    participant Q as Queue
    participant C as Channel
    participant O as Operations

    P->>R: Change notification
    R->>D: Deduplicate + resolve owner
    D-->>R: Tenant policy + account state
    R->>A: Message + bounded context
    A->>D: Classification + usage record
    A->>Q: Structured signal
    Q->>C: Deliver to selected destination
    C-->>O: Receipt or failure
    O->>D: Reconcile delivery state
    O-->>Q: Retry when policy allows
```

## Infrastructure decisions

The current specification describes a Node.js API, PostgreSQL, n8n orchestration, and Redis/Upstash for bounded application concerns such as OTPs, rate limiting, and revoked-token entries. n8n queue mode is explicitly deferred until memory pressure or execution backlog justifies its additional infrastructure cost.

## Historical architecture image

![Historical MailIQ system architecture](../assets/historical-system-architecture-overview.png)

This image was retained from Drive as historical evidence. When it conflicts with this document or the v5 source, the v5 model and the repository evidence register take precedence.
