# MailIQ Security Architecture

## 1. Overview

Security is treated as a core architectural concern in MailIQ because the platform handles customer accounts, email connections, authentication credentials, subscription state, AI processing context, and communication-channel integrations.

The security architecture therefore focuses on authentication, token lifecycle management, tenant isolation, webhook security, access control, database safety, and auditability.

---

## 2. Security Model

At a high level:

    User
      │
      ▼
    Authentication
      │
      ▼
    Authorised Application
      │
      ▼
    Customer Context
      │
      ├── Configuration
      ├── Email Connection
      ├── Subscription
      └── Memory
      │
      ▼
    Workflow Execution
      │
      ▼
    External Integrations

Each stage must preserve the correct customer context and prevent unauthorised access to another customer's resources.

---

## 3. Authentication

MailIQ uses multiple authentication mechanisms for different parts of the platform.

### Application Authentication

Application-level authentication uses JWT-based authentication.

The application validates the user's authentication state before allowing access to protected resources.

### External Provider Authentication

MailIQ uses OAuth 2.0 to connect customer accounts with external email providers.

Supported providers include:

- Google
- Microsoft

This allows MailIQ to access customer email without requiring customers to provide their email passwords directly to the platform.

---

## 4. OAuth 2.0 Security

The OAuth architecture handles the lifecycle of external provider credentials.

The lifecycle can be represented as:

    Customer
       │
       ▼
    OAuth Authorization
       │
       ▼
    Authorization Code
       │
       ▼
    Access / Refresh Credentials
       │
       ▼
    Secure Application Storage
       │
       ▼
    API Access
       │
       ▼
    Token Refresh
       │
       ▼
    Continued Access

The system includes OAuth implementations for both Google and Microsoft.

---

## 5. Refresh Token Rotation

Refresh tokens are treated as security-sensitive credentials.

The authentication architecture includes refresh-token rotation.

Conceptually:

    Refresh Token A
          │
          ▼
       Refresh
          │
          ▼
    Refresh Token B
          │
          ▼
    Previous Token Invalidated

Rotation reduces the usefulness of a previously issued refresh token if it is compromised.

---

## 6. Refresh Token Reuse Detection

The system also accounts for refresh-token reuse.

Conceptually:

    Existing Refresh Token
             │
             ▼
       Token Used Again
             │
             ▼
       Reuse Detection
             │
             ▼
      Security Response

This provides an additional protection layer around the OAuth token lifecycle.

---

## 7. Token Revocation

Token revocation is part of the authentication architecture.

Revocation can be required when:

- A customer disconnects an account
- Credentials are invalidated
- A security event occurs
- A connection is no longer authorised

The objective is to ensure that credentials which should no longer provide access cannot continue to be used indefinitely.

---

## 8. Tenant Isolation

MailIQ is a multi-tenant system.

Customer identity therefore acts as an important security boundary.

Conceptually:

    Request
       │
       ▼
    Authenticate
       │
       ▼
    Resolve Customer
       │
       ▼
    Authorise Resource
       │
       ▼
    Access Customer Data

A request must not be able to substitute another customer's identifier and gain access to that customer's resources.

---

## 9. IDOR Protection

The application architecture accounts for insecure direct object reference risks.

Resources should be authorised against the authenticated customer's context rather than trusting identifiers supplied directly by the client.

Unsafe conceptual pattern:

    User A
      │
      ▼
    Request Resource ID: 123
      │
      ▼
    Direct Database Lookup

Safer pattern:

    User A
      │
      ▼
    Authenticate
      │
      ▼
    Resolve Customer A
      │
      ▼
    Verify Resource Belongs to Customer A
      │
      ▼
    Access Resource

This prevents a user from simply changing an object identifier to access another customer's resource.

---

## 10. Webhook Security

MailIQ relies on webhook-driven integrations for parts of its event-driven architecture.

Webhook endpoints therefore need to distinguish legitimate provider events from unauthorised requests.

The security architecture includes webhook authentication and signature verification where supported by the integration.

Conceptually:

    External Provider
          │
          ▼
       Webhook
          │
          ▼
    Validate Request
          │
       ┌──┴──┐
       │     │
     Valid Invalid
       │     │
       ▼     ▼
    Process Reject
      Event

Webhook validation occurs before trusted workflow processing begins.

---

## 11. Webhook Replay and Duplicate Processing

Event-driven systems can receive duplicate events.

MailIQ therefore uses idempotency-oriented processing principles to prevent the same event from producing unintended duplicate operations.

Conceptually:

    Webhook Event
         │
         ▼
    Identify Event
         │
         ▼
    Already Processed?
       ┌─┴─┐
       │   │
      Yes  No
       │   │
       ▼   ▼
    Ignore Process
             │
             ▼
          Record

This is particularly important for operations that trigger customer-visible messages or external side effects.

---

## 12. Database Security

PostgreSQL contains persistent application and customer state.

Security considerations include:

- Customer isolation
- Access control
- SQL injection prevention
- Sensitive credential protection
- Controlled database access
- Auditability

Dynamic SQL must be handled safely so that user-controlled values cannot alter the intended query structure.

---

## 13. Sensitive Data Handling

MailIQ interacts with sensitive information including authentication credentials and customer email data.

Sensitive values should therefore not be unnecessarily exposed through:

- Logs
- Error messages
- API responses
- Debug output
- Administrative notifications

Operational visibility should provide enough information to diagnose failures without exposing secrets.

---

## 14. Secret Management

Infrastructure credentials and third-party API credentials should be managed separately from application source code.

Relevant secrets include credentials associated with:

- Google
- Microsoft
- Paystack
- Messaging platforms
- AI providers
- Database access
- Infrastructure

Secrets should be supplied through the appropriate environment or secret-management mechanism rather than committed directly to the repository.

---

## 15. AI Security Considerations

AI processing introduces additional security considerations because customer email content is passed into the intelligence pipeline.

The workflow should maintain customer context boundaries throughout AI processing.

The AI layer should also return structured output that can be validated before downstream actions are performed.

Conceptually:

    Customer Email
         │
         ▼
    Controlled Context
         │
         ▼
    AI Processing
         │
         ▼
    Structured Output
         │
         ▼
    Validation
         │
         ▼
    Downstream Action

The validation stage prevents unvalidated model output from being treated as trusted application state.

---

## 16. Audit Logging

Audit logging provides visibility into important security and operational events.

Audit information can support investigation of:

- Authentication events
- OAuth events
- Customer account activity
- Workflow failures
- Configuration changes
- Security-related events

Audit records should avoid storing unnecessary secrets or sensitive credential material.

---

## 17. Error Handling and Security

Error handling must not become an information disclosure mechanism.

Errors should provide enough context for administrators to diagnose problems while avoiding exposure of:

- Access tokens
- Refresh tokens
- Passwords
- API keys
- Other secrets

Operational alerts should therefore focus on the identity of the failed operation, relevant workflow context, and actionable failure information rather than raw credentials.

---

## 18. Administrative Monitoring

MailIQ includes administrative monitoring for important operational failures.

Examples include:

- Workflow failures
- Customer disconnects
- Failed processing
- Integration problems

Administrative alerts can be delivered through WhatsApp.

The purpose is to provide rapid visibility into failures without requiring continuous manual inspection of the workflow infrastructure.

---

## 19. Security Boundaries

The major security boundaries can be represented as:

    ┌──────────────────────────────┐
    │          Customer            │
    └──────────────┬───────────────┘
                   │
             Authentication
                   │
                   ▼
    ┌──────────────────────────────┐
    │       Application Layer      │
    └──────────────┬───────────────┘
                   │
             Authorisation
                   │
                   ▼
    ┌──────────────────────────────┐
    │       Customer Context       │
    └───────┬───────────┬──────────┘
            │           │
            ▼           ▼
       PostgreSQL      n8n
            │           │
            └─────┬─────┘
                  ▼
         External Integrations

Security controls must remain consistent across these boundaries.

---

## 20. Security Principles

MailIQ's security architecture follows several core principles.

### Authenticate Before Access

Protected application resources require authentication.

### Authorise Against Customer Context

Authentication alone is not sufficient. Resources must also belong to the authenticated customer.

### Protect Credentials

OAuth tokens, API keys, and infrastructure credentials must be treated as secrets.

### Validate External Events

Webhook events should be authenticated and validated before being processed.

### Validate AI Output

AI-generated data should not automatically be treated as trusted application state.

### Minimise Information Exposure

Logs, errors, and alerts should avoid exposing sensitive information.

### Audit Important Events

Security and operational events should leave enough evidence for investigation.

---

## 21. Security Testing

Security-related testing should cover the major trust boundaries in the platform.

Important areas include:

- OAuth flows
- Token lifecycle
- Token revocation
- Webhook validation
- Customer isolation
- Resource authorisation
- SQL safety
- Authentication failures
- Invalid webhook payloads
- AI output validation

Security testing should be expanded alongside new integrations and application features.

---

## 22. Security Documentation Scope

This document describes the current security architecture at a system level.

Further security documentation can cover:

- Detailed authentication flows
- OAuth sequence diagrams
- Token storage architecture
- Webhook signature implementation
- Database access controls
- Tenant isolation implementation
- Secret management
- Security testing procedures
- Incident response
- Data retention
- Backup and recovery
