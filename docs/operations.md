# MailIQ Operations & Reliability

## 1. Overview

MailIQ is designed to operate as an automated SaaS system with minimal manual intervention.

Because the platform depends on multiple external services, operational reliability requires more than simply keeping the application online.

The operational architecture is responsible for:

- Workflow monitoring
- Failure detection
- Error handling
- Retry behaviour
- Customer connection monitoring
- Administrative alerts
- Integration health
- Production maintenance
- Operational troubleshooting

The goal is to ensure that failures are detected quickly and isolated where possible rather than silently affecting customers.

---

## 2. Operational Architecture

The operational model can be represented as:

    Production System
          │
          ▼
    Workflow Execution
          │
          ▼
    Monitoring / Detection
          │
       ┌──┴──┐
       │     │
    Healthy Failure
       │     │
       │     ▼
       │  Error Handler
       │     │
       │     ▼
       │  Admin Alert
       │
       ▼
    Continue Operation

Operational monitoring therefore sits alongside the normal application workflow rather than being treated as a separate afterthought.

---

## 3. Core Operational Components

The main operational components are:

| Component | Operational Responsibility |
|---|---|
| n8n | Workflow execution and automation |
| Railway | Production hosting |
| PostgreSQL | Persistent application state |
| Error handlers | Failure detection and routing |
| WhatsApp | Administrative alert delivery |
| OAuth integrations | Customer connection health |
| External APIs | Email, AI, communication, and billing dependencies |

---

## 4. Workflow Monitoring

n8n is the primary workflow execution environment.

Operational monitoring focuses on whether workflows:

- Execute successfully
- Encounter node failures
- Exhaust retry attempts
- Trigger error handlers
- Produce expected outputs
- Maintain customer context

A workflow that technically executes but produces an incorrect customer-facing result should still be treated as an operational failure.

---

## 5. Error Detection

Workflow failures are routed through dedicated error-handling paths.

The general flow is:

    Workflow Failure
          │
          ▼
    Retry Attempts
          │
          ▼
    Failure Persists
          │
          ▼
    Error Handler
          │
          ├── Identify Workflow
          ├── Identify Customer
          ├── Record Failure
          └── Notify Administrator

This prevents individual workflow failures from remaining invisible.

---

## 6. Retry Strategy

External APIs and workflow nodes can fail temporarily.

MailIQ uses retry behaviour to allow recoverable failures to succeed without requiring manual intervention.

The implemented workflow configuration allows up to three attempts for failed nodes.

    Attempt 1
       │
     Fail
       │
       ▼
    Attempt 2
       │
     Fail
       │
       ▼
    Attempt 3
       │
     Fail
       │
       ▼
    Error Handler

Retries are intended for transient failures and should not be treated as a replacement for proper error handling.

---

## 7. Administrative Alerts

Important production failures generate administrative notifications.

WhatsApp is used as an operational notification channel.

    Production Event
          │
          ▼
       Detection
          │
          ▼
      Error Handler
          │
          ▼
    Administrative Alert
          │
          ▼
       WhatsApp

This allows critical failures to be surfaced without requiring continuous manual inspection of the workflow dashboard.

---

## 8. Customer Disconnect Monitoring

Customer email connections can become invalid because of:

- Revoked permissions
- Expired credentials
- Failed token refresh
- Provider-side changes
- Customer-initiated disconnects

MailIQ monitors for these conditions.

    Email Provider
          │
          ▼
    Authentication Failure
          │
          ▼
    Connection State Detection
          │
          ▼
    Customer Connection Flag
          │
          ▼
    Administrative Alert

The objective is to make connection failures visible instead of allowing them to silently stop email processing.

---

## 9. External Dependency Monitoring

MailIQ depends on several external systems.

These include:

- Gmail
- Microsoft Graph
- Groq
- Evolution API
- Telegram
- Slack
- Discord
- Paystack
- Railway
- Database infrastructure

A failure in one external service can affect a specific portion of the system without necessarily requiring the entire platform to stop.

The architecture therefore aims for failure isolation.

---

## 10. Failure Isolation

The system is designed so that failures should remain contained where practical.

For example:

    Slack Failure
         │
         ▼
    Slack Delivery Error
         │
         ▼
    Slack Error Path

This should not automatically imply:

    Slack Failure
         │
         ▼
    Entire MailIQ Platform Failure

The same principle applies to individual email providers, AI requests, and other integrations.

---

## 11. AI Service Failures

Groq is an external dependency.

Possible failure conditions include:

- API unavailable
- Request timeout
- Rate limiting
- Invalid response
- Unexpected model output

The workflow should treat these as explicit failure conditions.

    Email
      │
      ▼
    AI Request
      │
    ┌─┴─┐
    │   │
 Success Failure
    │   │
    ▼   ▼
Continue Retry
        │
        ▼
    Error Handling

AI output validation remains necessary even when the API request itself succeeds.

---

## 12. Delivery Failures

Customer-facing delivery can fail independently from email processing.

For example:

    Email Processing ✓
           │
           ▼
    AI Analysis ✓
           │
           ▼
    Delivery Request
           │
           ▼
    WhatsApp Failure ✗

In this situation, the intelligence-processing workflow may have succeeded while the delivery operation failed.

Operational monitoring therefore needs to distinguish between processing failures and delivery failures.

---

## 13. Billing Operations

Paystack is responsible for subscription billing events.

Operational monitoring should account for events such as:

- Successful payment
- Failed payment
- Subscription changes
- Trial lifecycle
- Billing webhook failures

The application should maintain the appropriate internal subscription state based on validated billing events.

---

## 14. Database Operations

PostgreSQL stores persistent application state.

Operational responsibilities include:

- Maintaining database connectivity
- Protecting credentials
- Monitoring failed database operations
- Preventing unintended data loss
- Maintaining customer isolation

Database failures should be treated as high-priority infrastructure events because multiple workflow components may depend on persistent state.

---

## 15. Customer Isolation

MailIQ operates as a multi-customer SaaS platform.

Operational processes must therefore preserve customer boundaries.

Important requirements include:

- Correct customer identification
- Correct credential association
- Correct memory association
- Correct workflow association
- Correct delivery destination
- No cross-customer data leakage

Operational debugging should also avoid exposing customer information unnecessarily.

---

## 16. Operational Logging

Production troubleshooting depends on being able to identify what happened during a failed workflow.

Useful operational information includes:

- Workflow name
- Execution status
- Failure point
- Customer identifier
- External service involved
- Error type
- Retry count
- Timestamp
- Resulting state

Logs and diagnostic information should avoid exposing:

- Access tokens
- API keys
- Passwords
- OAuth secrets
- Sensitive customer content

---

## 17. Incident Response

A production incident should follow a controlled sequence.

    Detect
      │
      ▼
    Identify
      │
      ▼
    Isolate
      │
      ▼
    Recover
      │
      ▼
    Verify
      │
      ▼
    Document

### Detect

Determine that a workflow, integration, or infrastructure component has failed.

### Identify

Determine the affected workflow, customer path, and external dependency.

### Isolate

Prevent the failure from unnecessarily affecting unrelated workflows.

### Recover

Restore the affected component or workflow.

### Verify

Confirm that the expected customer-facing behaviour has returned.

### Document

Record the cause and resolution where appropriate.

---

## 18. Common Failure Categories

### Authentication Failure

Customer or application credentials become invalid.

### External API Failure

A third-party service is unavailable or returns an error.

### Workflow Failure

An n8n node or workflow execution fails.

### AI Failure

Groq is unavailable or produces invalid output.

### Delivery Failure

A communication platform fails to deliver the generated intelligence.

### Database Failure

Persistent state cannot be read or written.

### Billing Failure

A Paystack event cannot be processed correctly.

---

## 19. Operational Troubleshooting

When investigating a failed customer workflow, the recommended sequence is:

    1. Identify Customer
          │
          ▼
    2. Identify Workflow
          │
          ▼
    3. Identify Failed Stage
          │
          ▼
    4. Identify External Dependency
          │
          ▼
    5. Check Retry Attempts
          │
          ▼
    6. Inspect Error Handler
          │
          ▼
    7. Verify Persistent State
          │
          ▼
    8. Verify Customer-Facing Result

This approach helps distinguish between application bugs, integration failures, and temporary infrastructure problems.

---

## 20. Maintenance

Operational maintenance may include:

- Reviewing failed workflow executions
- Reviewing integration failures
- Checking customer disconnects
- Updating workflow logic
- Updating API credentials
- Updating container configurations
- Updating dependencies
- Reviewing database state
- Testing critical workflows after changes

Maintenance should be performed without unnecessarily disrupting unrelated customer workflows.

---

## 21. Deployment and Operations Relationship

Deployment and operations are closely connected.

A production change should be considered complete only after the resulting system has been verified operationally.

    Code / Workflow Change
             │
             ▼
         Deployment
             │
             ▼
       Workflow Test
             │
             ▼
       Integration Test
             │
             ▼
       Production Check
             │
             ▼
        Monitoring

Deployment documentation is maintained separately in:

`docs/deployment.md`

---

## 22. Security During Operations

Operational procedures must preserve the same security principles used during normal application execution.

Operational personnel should avoid exposing:

- OAuth tokens
- API keys
- Customer email contents
- Customer personal information
- Database credentials
- Internal secrets

Operational debugging should use the minimum information required to identify and resolve the problem.

Security architecture is documented separately in:

`docs/security.md`

---

## 23. Reliability Principles

### Fail Explicitly

Failures should become visible system states rather than silently disappearing.

### Retry Recoverable Failures

Temporary failures should be given an opportunity to recover automatically.

### Alert Persistent Failures

Failures that cannot recover automatically should notify the administrator.

### Isolate Dependencies

One external integration should not unnecessarily take down unrelated functionality.

### Preserve Customer Context

Every operational event should remain associated with the correct customer and workflow.

### Verify Recovery

A resolved error is not considered closed until the expected behaviour has been confirmed.

---

## 24. Operational Maturity

The current operational architecture provides a foundation for automated monitoring and failure recovery.

Future improvements could include:

- Centralised observability
- Structured application logging
- Metrics dashboards
- Automated health checks
- Service-level objectives
- Incident severity levels
- Automated incident correlation
- Runbooks
- Backup and disaster-recovery procedures
- Automated uptime monitoring
- Deployment rollback procedures

These can be added as the production system grows.

---

## 25. Operations Summary

MailIQ's operational architecture is designed around the assumption that failures will occur.

The objective is therefore not to pretend that external services and distributed workflows will always succeed.

Instead, the system uses:

- Retry behaviour
- Error handlers
- Administrative alerts
- Customer disconnect detection
- Failure isolation
- Structured troubleshooting
- Integration monitoring
- Persistent application state

The resulting operational model is:

    Detect
      ↓
    Retry
      ↓
    Recover
      ↓
    Alert if necessary
      ↓
    Verify
      ↓
    Continue operating

This allows MailIQ to operate as an automated SaaS platform while keeping important production failures visible and actionable.
