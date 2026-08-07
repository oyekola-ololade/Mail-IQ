```markdown
# MailIQ

> AI-powered email intelligence SaaS that turns incoming Gmail and Outlook email into structured, actionable intelligence and delivers it through the communication channels teams already use.

---

## Overview

MailIQ is a multi-tenant AI email intelligence platform designed to continuously monitor connected Gmail and Outlook accounts, analyse incoming messages, and deliver structured intelligence through WhatsApp, Telegram, Slack, or Discord.

Rather than simply summarising email, MailIQ processes each message through a structured AI pipeline that determines its category, urgency, important details, deadlines, and recommended action.

The platform also provisions personalised AI workflows for customers automatically, allowing new accounts to be onboarded without manually creating or configuring workflows for each customer.

---

## What MailIQ Does

```text
Gmail / Outlook
       │
       ▼
 Email Ingestion
       │
       ▼
 AI Processing
       │
       ├── Classification
       ├── Urgency Scoring
       ├── Key Detail Extraction
       ├── Deadline Detection
       └── Action Recommendation
       │
       ▼
 Structured Result
       │
       ▼
 Personalised Delivery
       │
       ├── WhatsApp
       ├── Telegram
       ├── Slack
       └── Discord
```

MailIQ is designed to turn an inbox into an actionable intelligence layer rather than another interface the user has to constantly monitor.

---

## Core Capabilities

### AI Email Intelligence

- 12-category email classification
- 1–10 urgency scoring
- Key information extraction
- Deadline and date detection
- Recommended action generation
- Structured AI output
- Token-efficient processing with SKIP logic
- Trust-based sender scoring
- User-defined classification overrides

### Personalised AI Agents

MailIQ uses a factory-style workflow architecture to automatically provision personalised AI workflows for new customers.

The architecture supports multiple combinations of:

- Email provider
- Delivery platform
- Customer configuration
- AI behaviour
- Notification preferences

This allows customer-specific execution without maintaining a separate manually designed workflow architecture for every account.

### Communication Channels

Processed intelligence can be delivered through:

- WhatsApp
- Telegram
- Slack
- Discord

### Authentication & Billing

- Google OAuth 2.0
- Microsoft OAuth 2.0
- JWT authentication
- Refresh-token rotation
- Token revocation and reuse detection
- Paystack subscription billing
- 7-day trial handling
- Subscription lifecycle management

### Memory

MailIQ maintains both short-term and long-term conversational context, allowing the system to retain relevant information about previous interactions and customer preferences.

### Reliability

The platform includes:

- Automatic retry handling
- Failed-job tracking
- Webhook event tracking
- Idempotency controls
- Customer disconnect alerts
- Administrative error monitoring
- Workflow health checks
- Reconciliation processes
- Audit logging

---

# Architecture

MailIQ is built around a multi-tenant architecture with shared workflow templates and isolated customer execution contexts.

A simplified architecture looks like:

```text
                         ┌─────────────────────┐
                         │     Customers       │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │   Application/API   │
                         └──────────┬──────────┘
                                    │
                    ┌───────────────┼───────────────┐
                    │               │               │
                    ▼               ▼               ▼
               PostgreSQL       OAuth 2.0        Paystack
                    │
                    ▼
              n8n Orchestration
                    │
          ┌─────────┴──────────┐
          │                    │
          ▼                    ▼
   Email Processing       Agent Factory
          │                    │
          ▼                    ▼
    Gmail / Outlook      Customer Context
          │                    │
          └─────────┬──────────┘
                    ▼
                 AI Layer
                    │
                    ▼
          Structured Intelligence
                    │
          ┌─────────┼─────────┐
          ▼         ▼         ▼
       WhatsApp  Telegram   Slack / Discord
```

The detailed architecture, database model, workflow design, security model, infrastructure, and operational architecture are documented separately in the repository.

---

# Multi-Tenant Workflow Architecture

One of the key architectural decisions in MailIQ is avoiding a model where every customer requires a completely separate manually maintained workflow.

Instead, the platform uses reusable workflow templates combined with customer-specific execution context.

```text
                    Workflow Template
                           │
                           ▼
                    Customer Fan-Out
                           │
          ┌────────────────┼────────────────┐
          ▼                ▼                ▼
      Customer A       Customer B       Customer C
          │                │                │
          ▼                ▼                ▼
   Execution Context Execution Context Execution Context
          │                │                │
          ▼                ▼                ▼
     AI Agent A        AI Agent B        AI Agent C
```

This provides a more maintainable foundation for scaling customer-specific automation while keeping the underlying workflow architecture reusable.

---

# Engineering Highlights

MailIQ was designed with production concerns beyond the core AI workflow.

## Security

The architecture addresses:

- OAuth credential protection
- JWT expiry and refresh
- Refresh-token rotation
- Refresh-token reuse detection
- Token revocation
- Webhook authentication
- Webhook signature verification
- Tenant isolation
- IDOR protection
- Dynamic SQL safety
- Audit logging

## Reliability

Failures are treated as expected system states rather than exceptional situations.

```text
Request
   │
   ▼
Processing
   │
   ├── Success ───────────────► Continue
   │
   └── Failure
          │
          ▼
      Retry Logic
          │
     ┌────┴────┐
     │         │
   Retry    Exhausted
     │         │
     ▼         ▼
 Continue   Failed Job
                │
                ▼
          Admin Alert
```

## Observability

Operational visibility is provided through:

- Audit logs
- Failed-job records
- Webhook event tracking
- Workflow health checks
- Reconciliation logs
- Administrative alerts

---

# Technology

| Layer | Technology |
|---|---|
| Workflow orchestration | n8n |
| AI | Groq AI / Llama 3.3 70B |
| Database | PostgreSQL |
| Authentication | OAuth 2.0 / JWT |
| Email providers | Gmail API / Microsoft Graph API |
| Messaging | WhatsApp / Telegram / Slack / Discord |
| Billing | Paystack |
| Containers | Docker |
| Infrastructure | Railway |
| Frontend | Netlify / Vercel |

---

# Project Status

**Production System**

MailIQ has been designed and implemented as a functional SaaS platform.

This repository is being organised as the engineering source of truth for the system, documenting its architecture, workflows, infrastructure, security decisions, and implementation as the project evolves.

---

# Repository Documentation

Detailed engineering documentation will be organised under:

```text
docs/
├── architecture/
├── database/
├── workflows/
├── security/
├── integrations/
└── deployment/
```

The README provides the system-level overview.

The documentation provides the deeper engineering detail.

---

# Key Engineering Decisions

The MailIQ architecture has evolved through identifying limitations and redesigning parts of the system around scalability, security, reliability, and maintainability.

Important architectural areas include:

- Shared workflow templates with isolated customer execution contexts
- Automated customer agent provisioning
- Multi-tenant data isolation
- OAuth token lifecycle management
- Refresh-token rotation and reuse detection
- Idempotent webhook processing
- Retry and failed-job handling
- AI output validation
- Operational monitoring and reconciliation

---

# Roadmap

Future development areas include continued improvements to:

- Platform scalability
- AI processing efficiency
- Observability
- Workflow reliability
- Customer configuration
- Analytics
- Operational tooling

---

## Author

**Ololade Oyekola**

AI Systems Engineer

[GitHub](https://github.com/oyekola-ololade) · [LinkedIn](https://www.linkedin.com/in/ololade-oyekola-5b1797397/)
```
