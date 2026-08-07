# MailIQ System Architecture

## 1. System Overview

MailIQ is a multi-tenant AI email intelligence SaaS platform that monitors connected Gmail and Outlook accounts, processes incoming email through an AI classification and intelligence pipeline, and delivers structured results through WhatsApp, Telegram, Slack, and Discord.

The system is designed around automated customer provisioning, event-driven email processing, personalised AI behaviour, multi-channel delivery, subscription management, and fault-tolerant workflow execution.

At a high level:

    Email Provider
         │
         ▼
    Email Event
         │
         ▼
    MailIQ Processing Layer
         │
         ├── Customer Context
         ├── AI Classification
         ├── Urgency Scoring
         ├── Detail Extraction
         ├── Deadline Detection
         ├── Sender Trust
         └── User Rules
         │
         ▼
    Structured Intelligence
         │
         ▼
    Delivery Router
         │
         ├── WhatsApp
         ├── Telegram
         ├── Slack
         └── Discord

---

## 2. Customer Provisioning Architecture

A central design decision in MailIQ is the use of a factory workflow that automatically provisions personalised AI agent workflows when a customer signs up.

Rather than manually creating workflows for individual users, the factory determines the customer's configuration and provisions the appropriate workflow combination.

The system was designed to support 16 platform/email-provider combinations.

    Customer Signup
          │
          ▼
    Customer Configuration
          │
          ▼
    Factory Workflow
          │
          ├── Email Provider
          ├── Delivery Platform
          ├── User Configuration
          └── Agent Settings
          │
          ▼
    Select Workflow Variant
          │
          ▼
    Provision Personalised Agent
          │
          ▼
    Activate Customer Workflow

This architecture allows customer onboarding to remain automated rather than requiring manual workflow creation.

---

## 3. Email Processing Pipeline

Once an email enters the system, MailIQ processes it through a structured AI pipeline.

The processing flow includes:

    Incoming Email
          │
          ▼
    Validate Event
          │
          ▼
    Identify Customer
          │
          ▼
    Retrieve Customer Context
          │
          ▼
    Apply User Rules
          │
          ▼
    AI Processing
          │
          ├── Category
          ├── Urgency
          ├── Key Details
          ├── Deadlines
          ├── Recommended Action
          └── Sender Trust
          │
          ▼
    Validate AI Output
          │
          ▼
    Build Structured Result
          │
          ▼
    Delivery Workflow

The AI system uses a 12-category classification system and an urgency score ranging from 1 to 10.

The system also includes SKIP logic intended to avoid unnecessary AI processing when a message does not require further analysis.

---

## 4. AI Intelligence Layer

MailIQ's AI processing is designed around structured output rather than unrestricted conversational responses.

The intelligence layer evaluates:

- Email category
- Urgency
- Important information
- Deadlines
- Recommended actions
- Sender trust
- User-defined overrides

The architecture also includes short-term and long-term memory.

    Email
      │
      ▼
    AI Context
      │
      ├── Current Email
      ├── User Preferences
      ├── Sender Information
      ├── Recent Context
      └── Long-Term Memory
      │
      ▼
    Structured AI Result

The objective is to provide context-aware intelligence while keeping the output predictable enough for downstream automation.

---

## 5. Multi-Channel Delivery

After processing, the structured result is routed to the customer's configured communication platform.

    Structured Intelligence
             │
             ▼
       Delivery Router
             │
       ┌─────┼─────┬─────┐
       ▼     ▼     ▼     ▼
    WhatsApp Telegram Slack Discord

The delivery layer abstracts the final communication channel from the AI processing layer.

This allows the core intelligence workflow to remain independent of the platform used to deliver the result.

---

## 6. Authentication

MailIQ integrates with both Google and Microsoft authentication systems.

The authentication architecture supports OAuth 2.0 for:

- Google / Gmail
- Microsoft / Outlook

The authentication layer is responsible for obtaining and maintaining the credentials required to access customer email accounts.

The system also includes JWT-based application authentication and token lifecycle handling.

---

## 7. Subscription and Billing

MailIQ uses Paystack for subscription billing.

The billing lifecycle includes:

    Customer Signup
          │
          ▼
    Trial Period
          │
          ▼
    Subscription
          │
          ├── Active
          ├── Renewal
          ├── Failed Payment
          └── Cancellation
          │
          ▼
    Customer Access State

The platform includes a 7-day trial and subscription lifecycle handling.

Billing state is treated as part of the customer's platform state rather than as an isolated payment feature.

---

## 8. Reliability Architecture

MailIQ was designed with failure handling at the workflow level.

Automatic retry logic is used for workflow operations, with the implemented system using up to three attempts for failed nodes.

    Workflow Node
         │
         ▼
      Execute
         │
      ┌──┴──┐
      │     │
    Success Failure
      │     │
      ▼     ▼
    Continue Retry
            │
        ┌───┴───┐
        │       │
      Retry  Exhausted
        │       │
        ▼       ▼
     Continue Failed State
                    │
                    ▼
                Admin Alert

The system also includes error-handler workflows that alert the administrator when failures occur.

---

## 9. Monitoring and Operational Visibility

Administrative monitoring is built into the system rather than relying exclusively on manual inspection.

The platform includes:

- Workflow error monitoring
- Customer disconnect alerts
- Error-handler workflows
- Administrative WhatsApp alerts
- Workflow variant testing
- AI output validation
- Delivery confirmation testing

This provides visibility into failures across the automation chain.

---

## 10. Infrastructure

The production infrastructure includes:

- Self-hosted n8n
- Railway infrastructure
- Docker containerisation
- Netlify / Vercel frontend infrastructure
- Google Cloud OAuth configuration
- Microsoft Azure application registration
- Evolution API for WhatsApp connectivity

Infrastructure responsibilities are separated between application delivery, workflow orchestration, authentication providers, messaging infrastructure, and AI processing.

---

## 11. Testing and QA

MailIQ's workflow architecture was systematically tested across its workflow variants.

Testing covers:

- OAuth flows
- Webhook payloads
- AI output validation
- Delivery confirmation
- Workflow execution
- Error handling
- Workflow variant behaviour

The system also includes end-to-end testing designed to verify the complete path from authentication and email ingestion through AI processing and final message delivery.

---

## 12. Architectural Characteristics

The MailIQ architecture is primarily characterised by:

### Automated Provisioning

Customer-specific workflows are created and activated automatically.

### Multi-Tenant Execution

The platform is designed to support multiple customers while maintaining customer-specific configuration and execution contexts.

### Event-Driven Processing

Email events initiate downstream processing rather than requiring users to manually trigger analysis.

### Structured AI Processing

AI output is designed to feed deterministic downstream workflows.

### Multi-Channel Delivery

The intelligence layer is separated from the final communication channel.

### Fault Tolerance

Retries, error handlers, alerts, and validation reduce the impact of individual workflow failures.

### Modular Integrations

Email providers, AI processing, billing, and communication channels are connected through dedicated integration layers.

---

## 13. System Flow Summary

The complete system can be represented as:

    Customer
       │
       ▼
    Signup
       │
       ▼
    Authentication + Subscription
       │
       ▼
    Factory Provisioning
       │
       ▼
    Personalised Agent
       │
       ▼
    Gmail / Outlook
       │
       ▼
    Email Event
       │
       ▼
    AI Processing
       │
       ├── Classification
       ├── Urgency
       ├── Extraction
       ├── Deadlines
       ├── Trust
       └── Rules / Memory
       │
       ▼
    Structured Intelligence
       │
       ▼
    Delivery Router
       │
       ├── WhatsApp
       ├── Telegram
       ├── Slack
       └── Discord
       │
       ▼
    Monitoring + Error Handling

---

## 14. Further Architecture Documentation

This document provides the system-level architecture.

Additional documentation will cover:

- Workflow architecture
- AI processing design
- Multi-tenant data model
- Authentication and OAuth flows
- Database architecture
- Billing architecture
- Integration architecture
- Error handling and recovery
- Infrastructure and deployment
- Testing and QA
