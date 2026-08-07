# MailIQ API & Event Architecture

## 1. Overview

MailIQ is an event-driven SaaS system.

Rather than treating every operation as a direct request-response interaction, the platform uses APIs, webhooks, workflow triggers, and asynchronous processing to connect the application with external services.

The main communication paths are:

- Frontend → Application
- Google → MailIQ
- Microsoft → MailIQ
- MailIQ → n8n
- n8n → Groq
- n8n → WhatsApp
- n8n → Telegram
- n8n → Slack
- n8n → Discord
- Paystack → MailIQ

---

## 2. Communication Model

The system can be viewed as several interconnected event flows.

```text
                    CUSTOMER
                       │
                       ▼
                  Frontend/API
                       │
                       ▼
                Application State
                       │
                       ▼
                      n8n
                       │
        ┌──────────────┼──────────────┐
        │              │              │
        ▼              ▼              ▼
     Email           Groq          Delivery
    Providers          AI           APIs
        │              │              │
        │              │       ┌──────┼──────┐
        │              │       ▼      ▼      ▼
        │              │    WhatsApp Telegram Slack
        │              │
        │              └───────────────┐
        │                              ▼
        └──────────────────────► Processing
