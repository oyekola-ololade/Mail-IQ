# MailIQ Database Architecture

## 1. Overview

MailIQ uses PostgreSQL as the primary persistent data layer.

The database supports the application's customer, authentication, configuration, workflow, subscription, memory, operational, and audit requirements.

The database is designed to work alongside the n8n workflow layer rather than replacing it. n8n is responsible for workflow orchestration, while PostgreSQL provides persistent application state and structured records required across workflow executions.

---

## 2. Database Responsibilities

The database provides persistent storage for areas including:

- Customer information
- Authentication state
- Connected email accounts
- Customer configuration
- Workflow configuration
- Subscription state
- AI processing context
- Memory
- Operational records
- Failed executions
- Audit information

The database therefore acts as the persistent state layer underneath the event-driven workflow architecture.

---

## 3. High-Level Data Model

At a conceptual level:

    Customer
       │
       ├──────────────┐
       │              │
       ▼              ▼
    Authentication   Subscription
       │
       ▼
    Email Connections
       │
       ▼
    Customer Configuration
       │
       ├──────────────┐
       │              │
       ▼              ▼
    Workflow State   Memory
       │
       ▼
    Processing / Operational Records
       │
       ▼
    Audit / Error Records

The exact implementation schema may evolve as the platform develops.

---

## 4. Customer Data

Customer records represent the users or organisations using MailIQ.

Customer-related state can include:

- Customer identity
- Account status
- Configuration
- Subscription state
- Connected platforms
- Notification preferences
- AI preferences
- Memory context

Customer identity is the primary boundary used to associate application state with the correct tenant.

---

## 5. Multi-Tenant Data Isolation

MailIQ is designed as a multi-tenant system.

Customer-specific records must therefore remain associated with the correct customer context throughout application and workflow execution.

Conceptually:

    Customer A
       │
       ├── Email Connection A
       ├── Configuration A
       ├── Memory A
       └── Workflow State A

    Customer B
       │
       ├── Email Connection B
       ├── Configuration B
       ├── Memory B
       └── Workflow State B

A workflow execution should resolve the customer context before accessing customer-specific state.

This provides a logical isolation boundary between tenants.

---

## 6. Authentication Data

Authentication-related state supports the connection between the MailIQ account and external identity providers.

MailIQ integrates with:

- Google OAuth 2.0
- Microsoft OAuth 2.0

The authentication architecture also includes application-level JWT authentication and token lifecycle handling.

Sensitive authentication material must be treated as credential data and should not be exposed through normal application responses or logs.

---

## 7. Email Connection State

Email connection records associate a customer with their connected email provider.

The system supports:

- Gmail
- Microsoft Outlook

Conceptually:

    Customer
       │
       ▼
    Email Connection
       │
       ├── Provider
       ├── Connection State
       └── Authentication State

Email connection state is also relevant to customer disconnect detection and administrative alerting.

---

## 8. Workflow State

The database provides persistent state that supports the n8n workflow architecture.

Workflow-related state may include:

- Customer workflow configuration
- Workflow activation state
- Provider configuration
- Delivery configuration
- Execution-related records
- Failure state
- Operational metadata

The database and n8n therefore have complementary responsibilities:

    PostgreSQL
        │
        │ Persistent State
        ▼
    n8n
        │
        │ Workflow Execution
        ▼
    External Systems

---

## 9. AI and Processing Context

MailIQ's AI processing depends on customer-specific context.

Relevant persistent state can include:

- User preferences
- Classification overrides
- Sender trust information
- Memory
- Processing configuration

This allows the AI workflow to combine the current email with persistent customer context.

---

## 10. Memory

MailIQ incorporates both short-term and long-term memory.

Memory exists to provide continuity and relevant context during AI processing.

Conceptually:

    Customer
       │
       ├── Short-Term Memory
       │
       └── Long-Term Memory
                │
                ▼
          AI Context Builder
                │
                ▼
           AI Processing

Memory is associated with the appropriate customer context so that information from one tenant is not unintentionally exposed to another.

---

## 11. Subscription Data

Paystack provides subscription and billing functionality.

The application needs persistent subscription state so that customer access and workflow behaviour can respond to billing events.

Conceptually:

    Customer
       │
       ▼
    Subscription
       │
       ├── Trial
       ├── Active
       ├── Renewal
       ├── Failed Payment
       └── Cancelled

The subscription state is separate from the external payment provider itself.

Paystack provides payment events, while the application maintains the customer-facing subscription state required by MailIQ.

---

## 12. Operational Records

Operational data supports reliability and troubleshooting.

Relevant records can include:

- Failed jobs
- Workflow errors
- Webhook events
- Connection failures
- Processing failures
- Delivery failures
- Reconciliation information

These records allow administrators to determine what happened during a failed workflow execution.

---

## 13. Failed Job Tracking

MailIQ uses failure tracking as part of its reliability architecture.

A failed execution can be represented conceptually as:

    Workflow Execution
           │
           ▼
        Failure
           │
           ▼
      Retry Attempts
           │
           ▼
    Failure Persisted
           │
           ├── Error Details
           ├── Workflow Context
           ├── Customer Context
           └── Processing State
           │
           ▼
      Admin Alert

Persisting failure information makes it possible to investigate failures after the original workflow execution has ended.

---

## 14. Auditability

Audit information provides visibility into important application and operational events.

Audit records can be used to support:

- Security investigation
- Workflow troubleshooting
- Authentication investigation
- Customer activity review
- Operational debugging

Audit data should contain sufficient context to identify what occurred without exposing sensitive credentials or secrets.

---

## 15. Data Flow

A simplified application data flow is:

    Customer
       │
       ▼
    Application
       │
       ├── Read Customer State
       ├── Read Configuration
       ├── Read Connection State
       └── Read Subscription State
       │
       ▼
    n8n Workflow
       │
       ├── Process Event
       ├── Retrieve Context
       ├── Execute AI
       └── Deliver Result
       │
       ▼
    Persist Relevant State
       │
       ▼
    PostgreSQL

---

## 16. Database and Workflow Separation

The database should not be treated as the workflow engine.

Instead:

### PostgreSQL

Responsible for:

- Persistent state
- Structured application records
- Customer data
- Configuration
- Operational records
- Audit information

### n8n

Responsible for:

- Workflow execution
- Event processing
- API orchestration
- Automation logic
- Retry behaviour
- External integrations

This separation allows the workflow layer and persistence layer to evolve independently.

---

## 17. Security Considerations

The database architecture must account for the security requirements of a multi-tenant SaaS system.

Important considerations include:

- Tenant isolation
- Access control
- Credential protection
- Sensitive data handling
- SQL safety
- Auditability
- Authentication state protection
- Prevention of cross-customer data access

The broader security architecture is documented separately.

---

## 18. Schema Evolution

The MailIQ database schema is expected to evolve as the application develops.

New requirements may introduce changes to:

- Customer configuration
- AI preferences
- Memory
- Subscription state
- Workflow execution records
- Analytics
- Operational monitoring

Database changes should therefore be introduced deliberately and documented alongside the corresponding application or workflow changes.

---

## 19. Database Architecture Summary

The MailIQ database acts as the persistent state layer supporting the wider SaaS architecture.

    Customer
       │
       ├── Authentication
       ├── Email Connections
       ├── Configuration
       ├── Subscription
       ├── Memory
       ├── Workflow State
       └── Operational Records
               │
               ▼
           PostgreSQL
               │
               ▼
        n8n Workflow Layer
               │
               ▼
        External Integrations

The database architecture is intentionally separated from workflow execution so that persistent application state remains available independently of individual workflow runs.

---

## 20. Further Documentation

Future database documentation can expand this section with:

- Entity relationship diagrams
- Table definitions
- Primary and foreign key relationships
- Indexing strategy
- Migration strategy
- Data retention
- Backup and recovery
- Query patterns
- Database security controls
