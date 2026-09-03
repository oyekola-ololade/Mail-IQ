# MailIQ Multi-Workflow System Map

## Status

**Recovered later-generation architecture / static implementation evidence. Runtime revalidation pending.**

MailIQ is not one n8n workflow. The later build is a cooperating set of onboarding, email-processing, provider-lifecycle, billing, notification, operational and agent-tool workflows sharing authoritative PostgreSQL state.

## 1. Onboarding and tenant creation

```mermaid
flowchart TD
    Signup["Signup / onboarding request"] --> R["SW-01 Router"]
    R --> F["Free onboarding"]
    R --> B["Basic onboarding"]
    R --> S["Standard onboarding"]
    R --> P["Premium onboarding"]
    R --> BU["Business onboarding"]
    F --> DB[("Client + settings + subscription state")]
    B --> DB
    S --> DB
    P --> DB
    BU --> DB
    P --> OAuth["Provider OAuth / watches / platform mapping"]
    BU --> OAuth
```

The router and plan-specific onboarding workflows are separate because plan capabilities, provider setup and platform configuration differ.

## 2. Email-event processing

```mermaid
flowchart LR
    Gmail["Gmail Pub/Sub"] --> G["SW-11 Gmail Receiver"]
    Outlook["Microsoft Graph"] --> O["SW-12 Outlook Receiver"]
    G --> Resolve["Resolve client / deduplicate"]
    O --> Resolve
    Resolve --> Tier{"Client tier"}
    Tier --> Free["Free processor"]
    Tier --> Basic["Basic processor"]
    Tier --> Standard["Standard processor"]
    Tier --> Premium["Premium processor"]
    Free --> State[("Email + usage + settings state")]
    Basic --> State
    Standard --> State
    Premium --> State
    State --> Notify["Notification / digest path"]
```

A separate Business processor export was **not recovered** in the later 38-file set. Business onboarding exists. No missing processor is invented in this repository.

## 3. Billing and usage control

```mermaid
flowchart TD
    Ext["Paystack / platform webhooks"] --> Router["SW-02 Multi-Webhook Router"]
    Router --> Sub["SW-03 Subscription Lifecycle"]
    Sub <--> DB[("Subscriptions / clients")]
    Recon["SW-04 Billing Reconciliation"] --> Provider["Paystack status"]
    Provider --> Recon
    Recon -->|mismatch| Sub
    Meter["SW-06 Usage Meter"] <--> DB
    Meter --> Alert["limit / billing signal"]
```

Billing state is intended to gate processing rather than exist as a disconnected accounting afterthought.

## 4. Notifications and platform delivery

```mermaid
flowchart TD
    Event["Trial / deadline / payment / usage event"] --> N["SW-05 Notification Engine"]
    N --> Immediate["Immediate delivery"]
    N --> Digest["Digest queue"]
    Digest --> DD["SW-07 Digest Dispatcher"]
    DD --> Quiet{"Quiet hours?"}
    Quiet -->|yes| Queue[("pending_messages")]
    Quiet -->|no| Send["Configured platform"]
    Queue --> Flush["SW-08 Quiet Hours Flush"]
    Flush --> Send
    Send --> WA["WhatsApp"]
    Send --> TG["Telegram"]
    Send --> SL["Slack"]
    Send --> DC["Discord"]
```

Telegram and Slack have separate onboarding/mapping workflows; Discord has a bot-join mapping handler.

## 5. Provider lifecycle

```mermaid
flowchart LR
    Tokens[("Encrypted OAuth state")] --> TR["SW-13 Token Refresher"]
    TR --> Gmail["Google OAuth"]
    TR --> Outlook["Microsoft OAuth"]
    Gmail --> Tokens
    Outlook --> Tokens
    Tokens --> GW["SW-14 Gmail Watch Renewer"]
    Tokens --> OR["SW-15 Outlook Subscription Renewer"]
    GW --> GmailAPI["Gmail watch"]
    OR --> Graph["Microsoft Graph subscription"]
```

This family exists because push subscriptions and access tokens expire independently of email-processing logic.

## 6. Operations and recovery

```mermaid
flowchart TD
    Health["SW-16 Health Monitor"] --> DB[("Clients / workflow state")]
    DLQ["SW-23 DLQ Reprocessor"] --> Fail[("failed_jobs")]
    Purge["SW-21 Data Purge"] --> DB
    Prune["SW-22 History Pruner"] --> DB
    Settings["SW-19 Settings API"] <--> DB
    Health --> Alerts["SW-18 Admin Alerts"]
    DLQ --> Alerts
    Alerts --> Audit[("admin audit log")]
```

## 7. Conversational agent and tools

```mermaid
flowchart LR
    Msg["Inbound WhatsApp-style message"] --> Agent["SW-20 Conversational Agent"]
    Agent --> Cal["TW-01 Calendar"]
    Agent --> Search["TW-02 Email Search"]
    Agent --> Settings["TW-03 Settings"]
    Agent --> Draft["TW-04 Draft / Send"]
    Cal --> Token["TW-05 Token Refresh Handler"]
    Draft --> Token
    Search --> DB[("MailIQ state")]
    Settings --> DB
    Token --> DB
```

## Architecture principle

The core design is **shared workflows + per-client state**, not one complete n8n clone per customer. PostgreSQL is the intended authority for client, subscription, integration, OAuth, usage, notification and operational state.

That principle is also why historical identifier/state mismatches are serious: a workflow can visibly execute while authoritative state is wrong.
