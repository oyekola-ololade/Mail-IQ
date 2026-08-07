# MailIQ Workflow Architecture

## 1. Overview

MailIQ uses n8n as the primary workflow orchestration layer.

The workflow architecture is designed around reusable automation patterns, customer-specific execution contexts, automated provisioning, structured AI processing, multi-channel delivery, and failure handling.

A central design objective is to avoid manually building and maintaining a completely separate workflow for every customer.

---

## 2. Workflow Architecture Model

The system can be viewed as several major workflow layers:

    Customer Lifecycle
           │
           ▼
    Provisioning Factory
           │
           ▼
    Personalised Customer Workflows
           │
           ▼
    Email Processing
           │
           ▼
    AI Intelligence
           │
           ▼
    Delivery
           │
           ▼
    Monitoring / Recovery

Each layer has a distinct responsibility while remaining connected through workflow data and customer configuration.

---

## 3. Customer Provisioning Factory

The provisioning factory is responsible for creating and activating the workflow configuration required by a new customer.

The customer configuration determines the required combination of email provider and delivery platform.

The implemented architecture supports 16 platform/email-provider combinations.

Conceptually:

    New Customer
         │
         ▼
    Customer Configuration
         │
         ├── Email Provider
         ├── Delivery Platform
         ├── AI Configuration
         └── User Preferences
         │
         ▼
    Factory Workflow
         │
         ▼
    Select Required Variant
         │
         ▼
    Provision Workflow
         │
         ▼
    Activate Workflow

This removes the need for manual workflow creation during customer onboarding.

---

## 4. Customer Workflow Context

Each customer workflow operates using customer-specific configuration.

The workflow context can include:

- Customer identity
- Connected email provider
- Connected delivery platform
- AI configuration
- User-defined rules
- Sender trust information
- Memory
- Subscription state
- Notification preferences

The workflow therefore uses a shared architectural pattern while executing with customer-specific state.

---

## 5. Email Ingestion

The email processing lifecycle begins when an email event enters the system.

The ingestion workflow is responsible for receiving the event and determining the customer and processing context.

    Email Provider
         │
         ▼
    Incoming Event
         │
         ▼
    Validate Event
         │
         ▼
    Identify Customer
         │
         ▼
    Load Customer Context
         │
         ▼
    Continue Processing

Gmail and Microsoft Outlook are supported as email providers.

---

## 6. Processing and AI Workflow

After ingestion, the email is passed through the intelligence workflow.

The workflow prepares the relevant context before sending the message for AI processing.

    Email
      │
      ▼
    Context Preparation
      │
      ├── Customer Preferences
      ├── User Rules
      ├── Sender Information
      ├── Recent Context
      └── Long-Term Memory
      │
      ▼
    AI Processing
      │
      ▼
    Structured Result
      │
      ▼
    Output Validation

The AI system performs multiple operations within the processing pipeline.

These include:

- 12-category classification
- Urgency scoring from 1–10
- Key information extraction
- Deadline detection
- Recommended action generation
- Sender trust scoring

---

## 7. SKIP Logic

MailIQ includes SKIP logic to reduce unnecessary AI processing.

The objective is to avoid spending AI resources on messages that do not require full analysis.

Conceptually:

    Incoming Email
         │
         ▼
    Processing Decision
         │
       ┌─┴─┐
       │   │
     SKIP Analyse
       │   │
       ▼   ▼
    Finish AI Pipeline
            │
            ▼
       Structured Result

The exact conditions for SKIP are part of the implementation and workflow configuration.

---

## 8. User Rules and Overrides

The AI processing layer incorporates user-defined override rules.

These rules allow customer-specific behaviour to influence the standard classification and processing logic.

Conceptually:

    Email
      │
      ▼
    Standard AI Analysis
      │
      ▼
    User Rules / Overrides
      │
      ▼
    Final Classification
      │
      ▼
    Final Action

This provides a mechanism for personalised behaviour without changing the underlying workflow architecture.

---

## 9. Memory Architecture

MailIQ incorporates both short-term and long-term memory.

The memory layer provides additional context to AI processing and supports continuity across interactions.

    Current Email
         │
         ├──────────────┐
         ▼              ▼
    Short-Term       Long-Term
      Memory           Memory
         │              │
         └──────┬───────┘
                ▼
          AI Context
                │
                ▼
          AI Processing

Memory is treated as part of the customer's execution context.

---

## 10. Output Validation

AI output is validated before it is passed to downstream delivery workflows.

This is important because downstream automation depends on predictable structured data.

    AI Response
         │
         ▼
    Output Validation
         │
       ┌─┴─┐
       │   │
     Valid Invalid
       │     │
       ▼     ▼
    Continue Error Handling

The system's QA process includes explicit AI output validation.

---

## 11. Multi-Channel Delivery

Once the intelligence result has been validated, the workflow routes it to the configured communication platform.

    Structured Result
          │
          ▼
     Delivery Router
          │
     ┌────┼────┬────┐
     ▼    ▼    ▼    ▼
    WA  Telegram Slack Discord

The delivery layer is separated from the core AI processing logic.

This allows the same intelligence pipeline to support different communication channels.

---

## 12. Retry Architecture

Workflow nodes use automatic retry logic to recover from transient failures.

The implemented system uses up to three attempts for failed nodes.

    Workflow Node
         │
         ▼
      Execute
         │
       ┌─┴─┐
       │   │
    Success Failure
       │   │
       ▼   ▼
    Continue Retry
            │
        ┌───┴───┐
        │       │
      Retry  Exhausted
        │       │
        ▼       ▼
     Continue Failed State

Retry behaviour is intended to handle temporary failures without immediately treating the workflow execution as permanently failed.

---

## 13. Error Handler Workflows

MailIQ uses dedicated error handling workflows to provide operational visibility when workflow execution fails.

    Workflow Failure
          │
          ▼
      Error Handler
          │
          ├── Record Failure
          ├── Identify Workflow
          ├── Identify Customer
          └── Alert Administrator
                    │
                    ▼
              WhatsApp Alert

This allows failures to be surfaced without requiring continuous manual monitoring of individual workflows.

---

## 14. Customer Disconnect Handling

Customer email connections can become invalid or disconnected.

MailIQ includes customer disconnect alerting so that the administrative side of the platform can identify these states.

    Email Connection
          │
          ▼
    Connection Failure
          │
          ▼
    Detect Disconnect
          │
          ▼
    Customer / Admin State
          │
          ▼
    Administrative Alert

The specific recovery process depends on the authentication and provider state.

---

## 15. Workflow Lifecycle

The overall lifecycle of a customer workflow is:

    1. Customer Signup
           │
           ▼
    2. Configuration
           │
           ▼
    3. Factory Provisioning
           │
           ▼
    4. Workflow Activation
           │
           ▼
    5. Email Event
           │
           ▼
    6. Context Preparation
           │
           ▼
    7. AI Processing
           │
           ▼
    8. Output Validation
           │
           ▼
    9. Delivery
           │
           ▼
    10. Monitoring / Logging

---

## 16. Workflow Design Principles

### Reusability

Workflow patterns are designed to be reused across customers rather than manually recreated.

### Customer-Specific Execution

Shared workflow architecture is combined with customer-specific configuration and state.

### Separation of Responsibilities

Provisioning, ingestion, AI processing, delivery, billing, and error handling are treated as separate workflow responsibilities.

### Failure Awareness

Failures are expected and handled through retries, error handlers, alerts, and operational records.

### Structured Data Flow

Workflows pass structured data between stages so downstream nodes can make deterministic decisions.

### Automated Provisioning

Customer onboarding should not depend on manual workflow configuration.

---

## 17. Workflow Testing

MailIQ's workflow testing covers the major execution paths required for reliable operation.

Testing includes:

- OAuth flows
- Webhook payloads
- AI output validation
- Delivery confirmation
- Workflow variants
- Error handling

The 16 workflow variants were systematically tested as part of the QA process.

---

## 18. Architecture Summary

The MailIQ workflow architecture can be summarised as:

    Customer
       │
       ▼
    Provisioning Factory
       │
       ▼
    Personalised Workflow
       │
       ▼
    Email Ingestion
       │
       ▼
    Context + Memory
       │
       ▼
    AI Processing
       │
       ├── Classification
       ├── Urgency
       ├── Extraction
       ├── Deadlines
       ├── Trust
       └── User Rules
       │
       ▼
    Output Validation
       │
       ▼
    Multi-Channel Delivery
       │
       ▼
    Monitoring
       │
       └── Retry / Error Handling

This architecture allows MailIQ to combine automated customer provisioning with personalised AI processing while maintaining reusable workflow patterns and operational visibility.
