# MailIQ Deployment & Infrastructure

## 1. Overview

MailIQ is deployed as a distributed SaaS system consisting of application infrastructure, workflow orchestration, authentication providers, external integrations, and supporting services.

The infrastructure was designed to support:

- Production workflow execution
- Automated customer provisioning
- External API integrations
- OAuth authentication
- AI processing
- Multi-channel delivery
- Subscription billing
- Operational monitoring
- Containerised services

---

## 2. Infrastructure Overview

The major infrastructure components are:

| Component | Responsibility |
|---|---|
| Railway | Hosting and production infrastructure |
| n8n | Workflow orchestration |
| Docker | Containerisation |
| Netlify / Vercel | Frontend hosting |
| Google Cloud | Google OAuth configuration |
| Microsoft Azure | Microsoft application registration |
| Evolution API | WhatsApp connectivity |
| Groq | AI processing |
| PostgreSQL | Persistent application state |

The infrastructure is divided between application hosting, workflow execution, external authentication, AI processing, communication services, and persistent storage.

---

## 3. High-Level Deployment Architecture

```text
                         ┌─────────────────────┐
                         │       Customer      │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │   Frontend / Web UI │
                         │  Netlify / Vercel   │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │   Application/API   │
                         └──────────┬──────────┘
                                    │
                ┌───────────────────┼───────────────────┐
                │                   │                   │
                ▼                   ▼                   ▼
        ┌───────────────┐   ┌───────────────┐   ┌───────────────┐
        │  PostgreSQL   │   │     n8n       │   │  Paystack     │
        │ Persistent    │   │ Orchestration │   │   Billing     │
        │    State      │   │               │   │               │
        └───────────────┘   └───────┬───────┘   └───────────────┘
                                    │
                 ┌──────────────────┼──────────────────┐
                 │                  │                  │
                 ▼                  ▼                  ▼
          ┌────────────┐    ┌────────────┐    ┌──────────────┐
          │ Gmail /    │    │   Groq AI  │    │ Communication│
          │ Microsoft  │    │            │    │  Platforms   │
          └────────────┘    └────────────┘    └──────────────┘
