# MailIQ — Multi-Tenant Email Intelligence Prototype

> **Evidence status:** Substantial multi-tenant prototype, previously trialled and currently offline.

MailIQ explores how Gmail and Outlook messages can be transformed into structured, actionable intelligence and routed to communication channels such as WhatsApp, Telegram, Slack, and Discord.

This repository contains real workflow, architecture, database, integration, and operations evidence. It also contains design documentation for controls that are incomplete or not verified end to end. MailIQ is not presented as a currently live or production-ready SaaS, and no paying customers are claimed.

---

## Current truth boundary

| Question | Current answer |
|---|---|
| Does substantial implementation evidence exist? | Yes |
| Was the product previously trialled? | Yes |
| Is it currently online? | No |
| Are paying customers claimed? | No |
| Is automatic provisioning verified end to end? | No |
| Are all reliability and security controls verified in operation? | No |
| Is this a production-readiness claim? | No |

## Intended email-intelligence flow

    Gmail / Outlook
           │
           ▼
      Email ingestion
           │
           ▼
      AI processing
           │
           ├── Classification
           ├── Urgency scoring
           ├── Key-detail extraction
           ├── Deadline detection
           └── Action recommendation
           │
           ▼
      Structured result
           │
           ▼
      Channel routing
           │
           ├── WhatsApp
           ├── Telegram
           ├── Slack
           └── Discord

The core product idea is to reduce inbox monitoring by turning incoming messages into structured decisions and notifications.

## Implemented and documented evidence

The project evidence covers substantial work in these areas:

- Gmail and Outlook ingestion designs and workflow exports
- Structured AI classification and urgency scoring
- Multi-channel delivery patterns
- Multi-tenant data and workflow architecture
- OAuth, subscription, and account-lifecycle design
- Database models and operational documentation
- Workflow-template and provisioning logic
- Error-handling, monitoring, and reconciliation designs

These items do not all have the same verification status. A documented control is not automatically an operating control, and an exported workflow is not production-tested until it is configured, executed with realistic test data, and checked for intended output and failure behaviour.

## Capability areas under review

### Email intelligence

The prototype and design evidence cover:

- 12-category email classification
- 1–10 urgency scoring
- Key-information extraction
- Deadline and date detection
- Recommended-action generation
- Structured AI output
- Token-saving SKIP logic
- Trust-based sender scoring
- User-defined classification overrides

### Multi-tenant workflow design

MailIQ uses a factory-style architecture intended to combine reusable templates with customer-specific context across email providers, delivery channels, preferences, and AI behaviour.

Automatic customer provisioning is not currently claimed as verified end to end. The repository should be read as a mixture of implemented workflow evidence and system design.

### Authentication and billing design

The documented scope includes:

- Google OAuth 2.0
- Microsoft OAuth 2.0
- JWT and refresh-token handling
- Token revocation and reuse-detection design
- Paystack subscription lifecycle design
- Trial and account-state handling

These controls require renewed execution and security verification before being described as production controls.

### Memory and routing

The architecture includes short- and long-term context concepts plus routing to WhatsApp, Telegram, Slack, and Discord. Current availability and delivery reliability are not claimed.

### Reliability and observability

The architecture specifies or partially implements:

- Retry handling
- Failed-job records
- Webhook-event tracking
- Idempotency controls
- Disconnect and administrative alerts
- Workflow health checks
- Reconciliation processes
- Audit logging

Inspection of the broader project evidence found gaps in provisioning, logging and metering, deduplication, and circuit-breaker behaviour. These remain rebuild and verification work.

---

## Architecture

MailIQ was designed around shared workflow templates and isolated customer execution contexts.

    Customers
        │
        ▼
    Application / API
        │
        ├──────────────┬──────────────┐
        ▼              ▼              ▼
    PostgreSQL      OAuth 2.0       Paystack
        │
        ▼
    n8n orchestration
        │
        ├─────────────────────┐
        ▼                     ▼
    Email processing      Agent factory
        │                     │
        ▼                     ▼
    Gmail / Outlook      Customer context
        │                     │
        └──────────┬──────────┘
                   ▼
                AI layer
                   │
                   ▼
         Structured intelligence
                   │
          ┌────────┼────────┐
          ▼        ▼        ▼
       WhatsApp Telegram Slack / Discord

This diagram describes the intended system architecture. It does not certify that every component is currently deployed or verified.

## Historical/design technology evidence

| Layer | Evidence represented in the project |
|---|---|
| Workflow orchestration | n8n |
| AI/LLM integrations | OpenAI and Groq/Llama designs |
| Database | PostgreSQL |
| Authentication | OAuth 2.0 and JWT designs |
| Email providers | Gmail API and Microsoft Graph API |
| Messaging | WhatsApp, Telegram, Slack, and Discord |
| Billing | Paystack design and workflow evidence |
| Containers/infrastructure | Docker and Railway documentation |
| Frontend | Netlify/Vercel documentation |

The table records project evidence and design scope, not a currently operating production stack.

## Repository documentation

- [Architecture](docs/architecture.md) — system structure and major components
- [Database](docs/database.md) — data model and persistence design
- [Security](docs/security.md) — authentication, authorisation, credentials, and security considerations
- [Integrations](docs/integrations.md) — external-provider designs
- [Deployment](docs/deployment.md) — historical/intended deployment architecture
- [API & Events](docs/api-and-events.md) — APIs, webhooks, and event flows
- [Testing & QA](docs/testing.md) — test strategy and validation plans
- [Operations](docs/operations.md) — monitoring, failure handling, and operational design

Documentation describes intent and design unless implementation evidence explicitly proves otherwise.

## Required verification before any “live” or “production-ready” claim

1. Reconcile account, credential, workflow, and subscription state references.
2. Configure the required services and credentials in a controlled test environment.
3. Execute every critical onboarding, processing, delivery, billing, and failure path.
4. Verify deduplication, idempotency, retry, and circuit-breaker behaviour.
5. Add complete logging, metering, reconciliation, and alerting.
6. Perform security review and tenant-isolation testing.
7. Record sustained operating evidence and real customer outcomes separately.

## Current role in the portfolio

MailIQ is valuable as evidence of substantial system architecture and workflow engineering. Its immediate portfolio role is to support technical discussions, reliability audits, and bounded repair work—not to imply that a live SaaS business or production deployment currently exists.

---

## Author

**Oyekola Ololade**

AI Systems Engineer

[GitHub](https://github.com/oyekola-ololade) · [LinkedIn](https://www.linkedin.com/in/ololade-oyekola-5b1797397/)
