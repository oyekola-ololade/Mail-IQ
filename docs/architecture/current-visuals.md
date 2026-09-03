# MailIQ Current Visual Sources

These diagrams are maintained as text so GitHub can render them directly and future architecture changes can be reviewed as diffs.

## v5-era system boundary

```mermaid
flowchart LR
    U[User / Admin UI] --> API[Node.js API]
    API <--> DB[(PostgreSQL authoritative state)]
    API --> N8N[n8n shared orchestration]

    Gmail[Gmail + Pub/Sub] --> N8N
    Outlook[Outlook + Graph] --> N8N
    OAuth[OAuth / token lifecycle] <--> API
    Billing[Subscription + usage] <--> DB

    N8N --> AI[Classification / extraction / agent layer]
    N8N --> Delivery[WhatsApp / Telegram / Slack / Discord]
    N8N --> Ops[Health / alerts / backup / reconciliation / DLQ]
    Ops --> DB
    Ops --> N8N
```

**Boundary:** architecture authority, not proof that every component is currently running.

## Recovered later-generation workflow topology

```mermaid
flowchart TB
    Pool[38 recovered later-generation exports]

    Pool --> O[Onboarding + plan routing]
    Pool --> T[Tier processors]
    Pool --> P[Provider / webhook lifecycle]
    Pool --> B[Billing + account state]
    Pool --> C[Notifications + communication]
    Pool --> R[Reliability + compliance]
    Pool --> A[Conversational agent + tools]

    O --> O1[Router · Free · Basic · Standard · Premium · Business]
    T --> T1[Free · Basic · Standard · Premium]
    P --> P1[Gmail · Outlook · webhooks · token/renewal handlers]
    B --> B1[Subscription · reconciliation · usage · settings]
    C --> C1[Notify · digest · quiet hours · Telegram · Slack · Discord]
    R --> R1[Health · backup · admin · GDPR · history · DLQ]
    A --> A1[Calendar · email search · settings · draft/send · token refresh]
```

**Boundary:** candidate canonical pool for v5 reconciliation. It does not mean 38 final, enabled, production-verified workflows.

## Account-state lifecycle

```mermaid
stateDiagram-v2
    [*] --> Registered
    Registered --> IntegrationPending
    IntegrationPending --> OnboardingPending: provider connected
    OnboardingPending --> Active: provisioning + state verification succeed
    OnboardingPending --> RepairRequired: provisioning/state mismatch
    Active --> RenewalRequired: provider/subscription expiry approaches
    RenewalRequired --> Active: renewal succeeds
    RenewalRequired --> RepairRequired: renewal fails
    Active --> Suspended: billing/policy/manual control
    Suspended --> Active: resolved
    Active --> Cancelled
    RepairRequired --> Active: reconciliation/repair succeeds
    Cancelled --> [*]
```

The state diagram is a control model. Exact runtime transitions must be verified against the selected workflow generation before a relaunch.
