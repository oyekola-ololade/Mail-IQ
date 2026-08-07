# MailIQ Integrations Architecture

## 1. Overview

MailIQ depends on several external services to provide email access, AI processing, communication delivery, authentication, billing, and infrastructure.

The integration architecture separates these external dependencies from the core MailIQ workflow logic wherever practical.

At a high level:

    External Services
          │
          ▼
    Integration Layer
          │
          ▼
    MailIQ Workflow Layer
          │
          ▼
    Application State

The major integrations include:

- Gmail API
- Microsoft Graph API
- Groq AI
- WhatsApp
- Telegram
- Slack
- Discord
- Paystack
- Google OAuth
- Microsoft OAuth

---

## 2. Integration Map

| Integration | Purpose | Direction |
|---|---|---|
| Gmail API | Email access and processing | MailIQ ← Gmail |
| Microsoft Graph API | Outlook email access and processing | MailIQ ← Microsoft |
| Groq AI | AI email analysis | MailIQ ↔ Groq |
| WhatsApp | Customer intelligence delivery and administration | MailIQ → WhatsApp |
| Telegram | Customer intelligence delivery | MailIQ → Telegram |
| Slack | Customer intelligence delivery | MailIQ → Slack |
| Discord | Customer intelligence delivery | MailIQ → Discord |
| Google OAuth | Gmail account authentication | MailIQ ↔ Google |
| Microsoft OAuth | Outlook account authentication | MailIQ ↔ Microsoft |
| Paystack | Subscription billing | MailIQ ↔ Paystack |

---

## 3. Gmail Integration

Gmail is one of MailIQ's supported email providers.

The Gmail integration is responsible for connecting customer Gmail accounts to the MailIQ email-processing pipeline.

Conceptually:

    Customer
       │
       ▼
    Google OAuth
       │
       ▼
    Gmail Authorization
       │
       ▼
    Gmail API
       │
       ▼
    MailIQ
       │
       ▼
    Email Processing

The integration allows MailIQ to monitor and process incoming Gmail messages for connected customers.

---

## 4. Microsoft Outlook Integration

Microsoft Outlook is the second major email provider supported by MailIQ.

The Microsoft Graph API provides the interface through which MailIQ interacts with Outlook email.

Conceptually:

    Customer
       │
       ▼
    Microsoft OAuth
       │
       ▼
    Microsoft Authorization
       │
       ▼
    Microsoft Graph API
       │
       ▼
    MailIQ
       │
       ▼
    Email Processing

The Microsoft integration allows the same core email intelligence architecture to support Outlook alongside Gmail.

---

## 5. Email Provider Abstraction

MailIQ supports multiple email providers while maintaining a common downstream processing architecture.

    Gmail ──────────────┐
                        │
                        ▼
                  Email Ingestion
                        │
    Outlook ────────────┘
                        │
                        ▼
                 Common Processing
                        │
                        ▼
                   AI Pipeline
                        │
                        ▼
                    Delivery

This separation means that provider-specific authentication and retrieval logic can feed into a common intelligence pipeline.

---

## 6. Google OAuth

Google OAuth 2.0 is used to authorise MailIQ to access a customer's Gmail account.

The authentication flow can be represented as:

    Customer
       │
       ▼
    MailIQ
       │
       ▼
    Google Authorization
       │
       ▼
    Authorization Code
       │
       ▼
    Token Exchange
       │
       ▼
    MailIQ Credential State
       │
       ▼
    Gmail API Access

The authentication architecture includes token lifecycle management, including refresh-token rotation, reuse detection, and revocation.

---

## 7. Microsoft OAuth

Microsoft OAuth 2.0 provides the equivalent authentication mechanism for Outlook users.

    Customer
       │
       ▼
    MailIQ
       │
       ▼
    Microsoft Authorization
       │
       ▼
    Authorization Code
       │
       ▼
    Token Exchange
       │
       ▼
    MailIQ Credential State
       │
       ▼
    Microsoft Graph API

The Microsoft authentication flow is integrated into the same broader customer provisioning and email-processing architecture.

---

## 8. Groq AI Integration

Groq AI provides the primary AI processing capability used by MailIQ.

The implemented system uses:

**Llama 3.3 70B Versatile**

The AI integration is responsible for transforming email content and customer context into structured intelligence.

Conceptually:

    Email
      │
      ▼
    Context Builder
      │
      ├── User Rules
      ├── Memory
      ├── Sender Context
      └── Customer Preferences
      │
      ▼
    Groq AI
      │
      ▼
    Structured Intelligence
      │
      ├── Category
      ├── Urgency
      ├── Key Details
      ├── Deadlines
      └── Recommended Action

The AI output is validated before downstream workflow actions are performed.

---

## 9. WhatsApp Integration

WhatsApp is one of MailIQ's primary customer delivery channels.

The implemented architecture uses Evolution API as the WhatsApp gateway.

Conceptually:

    MailIQ
       │
       ▼
    Delivery Workflow
       │
       ▼
    Evolution API
       │
       ▼
    WhatsApp
       │
       ▼
    Customer

WhatsApp is also used for administrative monitoring and error alerts.

---

## 10. Telegram Integration

Telegram provides an additional delivery channel for processed email intelligence.

    MailIQ
       │
       ▼
    Delivery Workflow
       │
       ▼
    Telegram Bot API
       │
       ▼
    Customer

Telegram is therefore treated as a delivery integration rather than being coupled directly to the AI processing layer.

---

## 11. Slack Integration

Slack provides another destination for MailIQ's structured email intelligence.

    MailIQ
       │
       ▼
    Delivery Workflow
       │
       ▼
    Slack
       │
       ▼
    Customer

The Slack integration allows customers to receive email intelligence inside an existing team communication environment.

---

## 12. Discord Integration

Discord is supported as an additional communication channel.

    MailIQ
       │
       ▼
    Delivery Workflow
       │
       ▼
    Discord
       │
       ▼
    Customer

As with the other delivery platforms, Discord is downstream of the core AI intelligence pipeline.

---

## 13. Delivery Abstraction

The delivery architecture is designed so that the intelligence pipeline does not need to fundamentally change based on the customer's chosen platform.

    Structured Intelligence
             │
             ▼
       Delivery Router
             │
       ┌─────┼─────┬─────┐
       ▼     ▼     ▼     ▼
    WhatsApp Telegram Slack Discord

This makes the communication platform an output concern rather than an AI-processing concern.

---

## 14. Paystack Integration

Paystack provides subscription billing for MailIQ.

The platform uses Paystack to manage the payment side of the subscription lifecycle.

Conceptually:

    Customer
       │
       ▼
    Subscription
       │
       ▼
    Paystack
       │
       ├── Trial
       ├── Payment
       ├── Renewal
       └── Subscription State
       │
       ▼
    MailIQ Application

MailIQ includes a 7-day trial and subscription lifecycle handling.

The application maintains the customer-facing subscription state required by the platform.

---

## 15. Webhook-Based Integrations

Several external integrations rely on event-driven communication.

A general integration pattern is:

    External Service
          │
          ▼
       Webhook
          │
          ▼
    Authentication
          │
          ▼
    Signature / Payload Validation
          │
          ▼
    Workflow Processing
          │
          ▼
    Application State

Webhook security and validation are documented separately in the security architecture.

---

## 16. Integration Error Handling

External integrations introduce failure conditions that are outside MailIQ's direct control.

Examples include:

- API failures
- Expired credentials
- Rate limits
- Invalid payloads
- Network failures
- Provider outages
- Customer disconnections
- Delivery failures

The workflow architecture therefore uses retry handling and error workflows.

    External API
         │
         ▼
       Request
         │
       ┌─┴─┐
       │   │
    Success Failure
       │   │
       ▼   ▼
    Continue Retry
            │
            ▼
       Error Handler
            │
            ▼
       Admin Alert

The implemented workflow system uses up to three attempts for failed nodes.

---

## 17. Customer Disconnect Handling

Email providers can invalidate or disconnect customer credentials.

MailIQ includes customer disconnect alerting so that these states can be detected and surfaced operationally.

    Email Provider
          │
          ▼
    Authentication Failure
          │
          ▼
    Detect Disconnect
          │
          ▼
    Update / Flag State
          │
          ▼
    Administrative Alert

The customer can then be directed through the appropriate reconnection process.

---

## 18. Integration Testing

The integration architecture requires testing across both individual providers and complete end-to-end flows.

Testing performed for MailIQ includes:

- Google OAuth flows
- Microsoft OAuth flows
- Webhook payload validation
- AI output validation
- Delivery confirmation
- Workflow variants
- Error handling

Because MailIQ supports multiple email and delivery combinations, integration testing is particularly important to prevent one provider-specific change from breaking unrelated workflow paths.

---

## 19. Integration Design Principles

### Provider Independence

Email-provider-specific behaviour is kept separate from the common intelligence pipeline.

### Delivery Independence

The AI processing layer is separated from the final communication platform.

### Credential Isolation

External authentication credentials are treated as security-sensitive application state.

### Failure Awareness

External API failures are expected and handled through retries and error workflows.

### Validation

External events and AI responses are validated before being treated as trusted workflow data.

### Replaceability

Integrations are treated as separate components so that changes to one provider do not require redesigning the entire system.

---

## 20. Complete Integration Flow

The complete integration path can be represented as:

    Customer
       │
       ▼
    Google / Microsoft OAuth
       │
       ▼
    Gmail / Outlook
       │
       ▼
    MailIQ Email Ingestion
       │
       ▼
    Customer Context + Memory
       │
       ▼
    Groq AI
       │
       ▼
    Structured Intelligence
       │
       ▼
    Delivery Router
       │
       ├── Evolution API → WhatsApp
       ├── Telegram Bot API → Telegram
       ├── Slack → Slack
       └── Discord → Discord

    Separately:

    Customer Subscription
           │
           ▼
        Paystack
           │
           ▼
    Subscription State
           │
           ▼
       MailIQ Platform

---

## 21. Integration Summary

MailIQ's integration architecture connects the core workflow engine to the external services required to provide a complete SaaS product.

The major integration groups are:

### Email

- Gmail API
- Microsoft Graph API

### Authentication

- Google OAuth 2.0
- Microsoft OAuth 2.0

### AI

- Groq AI
- Llama 3.3 70B Versatile

### Communication

- WhatsApp
- Telegram
- Slack
- Discord

### Billing

- Paystack

The architecture keeps these integrations connected through defined workflow boundaries so that email ingestion, AI processing, delivery, and billing can evolve independently.
