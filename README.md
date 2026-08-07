
# MailIQ

> AI-powered email intelligence SaaS that turns incoming email into structured, actionable intelligence and delivers it through the channels teams already use.

## Overview

MailIQ connects to Gmail and Outlook, monitors incoming email, processes messages through AI, and delivers structured intelligence to the user's preferred communication platform.

The system is designed as a multi-tenant SaaS platform with automated customer onboarding, personalised AI agent provisioning, email classification, urgency scoring, conversation memory, subscription management, and fault-tolerant workflow orchestration.

## Core Capabilities

- Real-time Gmail and Outlook email processing
- AI-powered email classification
- 1–10 urgency scoring
- Structured email summaries and action recommendations
- Personalised AI agent provisioning
- WhatsApp, Telegram, Slack, and Discord delivery
- Google and Microsoft OAuth 2.0
- Subscription billing and trial management
- Short-term and long-term conversation memory
- Automated retry and failure handling
- Multi-tenant architecture
- Administrative monitoring and alerts

## Architecture

MailIQ uses a workflow-driven architecture combining AI services, APIs, databases, authentication, billing, and messaging infrastructure.

The system is designed around reusable workflow templates and isolated customer execution contexts, allowing personalised agents to be provisioned without maintaining a separate workflow architecture for every customer.

Detailed architecture documentation is available in [`docs/`](./docs/).

## Technology

- Python
- n8n
- Groq AI
- PostgreSQL
- Docker
- Railway
- Gmail API
- Microsoft Graph API
- WhatsApp
- Telegram
- Slack
- Discord
- Paystack
- OAuth 2.0

## Project Status

**Production System**

MailIQ has been designed and implemented as a functional SaaS platform. This repository documents its architecture, engineering decisions, workflows, infrastructure, and implementation.

## Documentation

Documentation will be added progressively as the system architecture and implementation are organised within this repository.

## Author

**Ololade Oyekola**

AI Systems Engineer

[LinkedIn](https://www.linkedin.com/in/ololade-oyekola-5b1797397/) · [GitHub](https://github.com/oyekola-ololade)
