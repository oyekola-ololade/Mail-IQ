# MailIQ Architecture

This section documents the system architecture behind MailIQ, including the major services, data flows, workflow orchestration, multi-tenant execution model, integrations, and engineering decisions.

## Architecture Overview

MailIQ is a multi-tenant AI email intelligence SaaS platform.

The architecture is designed around an event-driven processing pipeline that:

1. Authenticates a customer and connects their Gmail or Outlook account.
2. Receives and processes incoming email events.
3. Retrieves the relevant customer configuration and context.
4. Classifies and analyses the email using the AI processing layer.
5. Extracts structured intelligence including category, urgency, key information, deadlines, and recommended actions.
6. Applies customer-specific rules and memory.
7. Delivers the resulting intelligence through the customer's configured communication channels.
8. Records relevant execution, subscription, and operational data for monitoring and recovery.

The repository documents the architecture, integration boundaries, workflow design, security model, deployment approach, testing strategy, and operational model behind this system. Implementation evidence is being progressively added as the platform is rebuilt.
## Major System Components

| Component | Responsibility |
|---|---|
| Frontend | Customer-facing application and configuration |
| Application/API | Authentication, customer management, configuration, and API operations |
| PostgreSQL | Persistent application, customer, configuration, execution, and audit data |
| n8n | Workflow orchestration and automation |
| AI Layer | Email classification, extraction, scoring, reasoning, and structured output |
| Gmail API | Gmail authentication and email access |
| Microsoft Graph API | Outlook authentication and email access |
| Messaging Integrations | Delivery through WhatsApp, Telegram, Slack, and Discord |
| Paystack | Subscription and billing lifecycle |
| OAuth Providers | Google and Microsoft authentication |
| Infrastructure | Hosting, containers, networking, and deployment |

## Core Architectural Principles

### Multi-Tenancy

MailIQ is designed to support multiple customers while maintaining logical isolation between customer data, credentials, configurations, workflows, and execution contexts.

### Automated Provisioning

Customer onboarding is designed around automated workflow provisioning rather than manually creating a new workflow for every customer.

### Fault Tolerance

Workflow failures are treated as recoverable system states. Retry logic, failure tracking, alerts, and reconciliation processes are used to prevent individual failures from silently breaking customer processing.

### Idempotent Processing

Webhook and event-driven operations are designed to prevent duplicate events from creating duplicate processing or customer-visible actions.

### Security by Design

Authentication, token management, webhook validation, tenant isolation, and auditability are treated as architectural concerns rather than features added after implementation.

### Structured AI Output

AI processing is constrained around structured outputs so downstream workflows can reliably consume classifications, scores, extracted information, and recommended actions.

## Detailed Documentation

The repository contains dedicated documentation for each major engineering area:

- [System Architecture](system-architecture.md) — Overall MailIQ system structure and component relationships
- [Workflow Architecture](workflow-architecture.md) — Automation workflows, orchestration, and processing logic
- [Database Architecture](../database.md) — Persistent data and storage architecture
- [Security Architecture](../security.md) — Authentication, credentials, access control, and security considerations
- [Integrations Architecture](../integrations.md) — External providers and service integrations
- [Deployment & Infrastructure](../deployment.md) — Production hosting, containers, and infrastructure
- [API & Event Architecture](../api-and-events.md) — APIs, webhooks, event flows, and communication boundaries
- [Testing & QA](../testing.md) — Testing strategy and workflow validation
- [Operations & Reliability](../operations.md) — Monitoring, failure handling, retries, and operational procedures
