# MailIQ Testing & Quality Assurance

## 1. Overview

MailIQ was tested as a multi-integration, event-driven SaaS system rather than as a collection of isolated workflows.

Testing focused on the areas most likely to cause production failures:

- OAuth authentication
- Email-provider integrations
- Webhook payloads
- AI output validation
- Workflow variants
- Multi-channel delivery
- Retry behaviour
- Error handling
- Customer disconnect states

The objective was to verify that the complete processing chain behaves predictably across different customer configurations.

---

## 2. Testing Philosophy

The testing approach follows the principle:

    Test the complete workflow,
    not just individual nodes.

A successful node execution does not necessarily mean that the complete system worked correctly.

For example:

    Email Received
         │
         ▼
    AI Processing ✓
         │
         ▼
    Output Validation ✓
         │
         ▼
    WhatsApp Delivery ✗

The overall workflow has still failed from the customer's perspective.

Testing therefore considers both individual components and complete end-to-end behaviour.

---

## 3. Test Architecture

The main testing flow is:

    Input / Event
         │
         ▼
    Authentication
         │
         ▼
    Payload Validation
         │
         ▼
    Workflow Execution
         │
         ▼
    AI Processing
         │
         ▼
    Output Validation
         │
         ▼
    Delivery
         │
         ▼
    Confirmation
         │
         ▼
    Final Result

Each boundary provides an opportunity to detect and isolate failures.

---

## 4. Workflow Variant Testing

MailIQ supports multiple combinations of email providers and delivery platforms.

The implemented architecture contains 16 workflow variants.

These variants were systematically tested to verify that provider-specific and delivery-specific paths behaved correctly.

Testing included combinations involving:

### Email Providers

- Gmail
- Microsoft Outlook

### Delivery Platforms

- WhatsApp
- Telegram
- Slack
- Discord

The purpose of variant testing was to ensure that one integration path did not silently break another.

---

## 5. OAuth Testing

OAuth flows were tested for both supported email providers.

### Google

Testing covered the Gmail authentication flow and the resulting application connection state.

### Microsoft

Testing covered the Microsoft authentication flow and Outlook connection state.

The OAuth testing process considered:

- Authorisation
- Callback handling
- Token exchange
- Credential state
- Refresh behaviour
- Disconnect conditions
- Revocation behaviour

---

## 6. Authentication Failure Testing

Authentication failures were tested as explicit system states rather than treated as unexpected exceptions.

Examples include:

- Invalid authentication state
- Expired credentials
- Revoked credentials
- Disconnected customer account
- Invalid OAuth state
- Failed token refresh

The expected behaviour is for the system to detect the failure and route it through the appropriate recovery or notification path.

---

## 7. Webhook Testing

Webhook payloads were tested to verify that external events could be correctly received and processed.

Testing focused on:

- Payload structure
- Required fields
- Event identification
- Customer identification
- Invalid payload handling
- Duplicate events
- Authentication / signature validation where supported
- Downstream workflow execution

A webhook is not considered successfully processed simply because the HTTP request was received.

The resulting workflow execution and final state must also be correct.

---

## 8. AI Output Testing

AI output is a critical testing boundary because downstream automation depends on predictable structured results.

Testing therefore includes validation of:

- Output structure
- Required fields
- Category values
- Urgency score
- Extracted information
- Recommended action
- Unexpected output
- Invalid output

The general flow is:

    AI Request
        │
        ▼
    Model Response
        │
        ▼
    Schema / Output Validation
        │
      ┌─┴─┐
      │   │
    Valid Invalid
      │     │
      ▼     ▼
    Continue Error Path

The purpose is to prevent malformed model output from being treated as trusted workflow data.

---

## 9. Email Classification Testing

MailIQ classifies incoming email into 12 categories.

Testing therefore needs to verify that representative email types are assigned to the expected categories.

The testing process should consider:

- Clearly classifiable messages
- Ambiguous messages
- Multiple possible categories
- Irrelevant messages
- Messages requiring user overrides

The classification result is evaluated as part of the complete AI output rather than as an isolated model response.

---

## 10. Urgency Scoring Testing

MailIQ assigns an urgency score from 1–10.

Testing considers whether the returned score:

- Exists
- Falls within the expected range
- Is represented in the expected format
- Is consistent with the structured output requirements

Boundary values are particularly important:

- Minimum urgency
- Maximum urgency
- Values near the boundaries

Invalid values should be rejected rather than passed into downstream processing.

---

## 11. User Rule Testing

User-defined override rules were included in the testing scope.

Testing verifies that customer-specific rules can influence the normal processing behaviour without breaking the rest of the workflow.

Conceptually:

    Email
      │
      ▼
    Standard Analysis
      │
      ▼
    User Rule
      │
      ▼
    Final Result
      │
      ▼
    Delivery

Testing should include both:

- Customers with no custom rules
- Customers with active custom rules

---

## 12. SKIP Logic Testing

MailIQ includes SKIP logic designed to avoid unnecessary AI processing.

Testing verifies that:

- Messages meeting SKIP conditions are skipped appropriately
- Messages requiring AI analysis are not incorrectly skipped
- The workflow continues correctly after a SKIP decision
- SKIP does not produce unintended customer-facing behaviour

The key test is therefore not simply whether SKIP occurs, but whether the correct processing decision is made.

---

## 13. Memory Testing

MailIQ includes short-term and long-term memory.

Testing should verify that relevant customer context remains associated with the correct customer.

Important considerations include:

- Correct customer context
- Memory retrieval
- Memory persistence
- Context availability during processing
- Customer isolation

Memory must never cause information from one customer to appear in another customer's processing context.

---

## 14. Delivery Testing

Each supported delivery platform was included in the workflow testing process.

Testing includes:

- Message formatting
- Correct destination
- Delivery request
- Successful delivery
- Failed delivery
- Delivery confirmation
- Retry behaviour

The delivery layer is considered successful only when the intended customer-facing result is produced.

---

## 15. Multi-Channel Testing

The same AI-generated intelligence can be routed to different platforms.

Testing therefore verifies that the delivery router selects the correct platform based on customer configuration.

    Customer Configuration
           │
           ▼
      Delivery Router
           │
       ┌───┼───┬───┐
       ▼   ▼   ▼   ▼
      WA  TG Slack Discord

A change to one delivery integration should not unintentionally alter another delivery path.

---

## 16. Retry Testing

MailIQ uses automatic retry behaviour for failed workflow nodes.

The implemented workflow configuration allows up to three attempts.

Testing verifies that:

1. The initial operation is attempted.
2. A failure triggers retry behaviour.
3. The operation can recover on a subsequent attempt.
4. Repeated failure eventually reaches the error-handling path.
5. The workflow does not continue as if a permanently failed operation succeeded.

Conceptually:

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

---

## 17. Error Handler Testing

Dedicated error-handler workflows were tested to verify that production failures are surfaced to the administrator.

Testing verifies that failures can result in:

- Failure identification
- Workflow identification
- Customer identification
- Administrative notification

The error-handling path should itself be treated as a production-critical workflow.

---

## 18. Customer Disconnect Testing

Customer disconnect scenarios were tested because external OAuth credentials can become invalid.

Testing includes situations where:

- A customer disconnects an account
- Credentials become invalid
- Token refresh fails
- Provider access is revoked

The expected behaviour is to detect the disconnected state and trigger the appropriate operational alert.

---

## 19. End-to-End Testing

End-to-end testing validates the complete customer journey.

A representative test is:

    Customer Email
         │
         ▼
    Email Provider
         │
         ▼
    MailIQ Ingestion
         │
         ▼
    Customer Context
         │
         ▼
    AI Processing
         │
         ▼
    Output Validation
         │
         ▼
    Delivery Router
         │
         ▼
    Communication Platform
         │
         ▼
    Customer Receives Result

The end-to-end test is considered successful only when the expected final result reaches the configured destination.

---

## 20. Negative Testing

Negative testing verifies that the system behaves correctly when inputs or dependencies fail.

Examples include:

- Invalid OAuth state
- Invalid webhook payload
- Missing required fields
- Invalid AI output
- Expired credentials
- Failed external API request
- Failed delivery
- Repeated workflow failure
- Customer disconnect
- Duplicate event

The expected behaviour should be deterministic and should route failures into the appropriate handling path.

---

## 21. Integration Testing

Integration testing focuses on the boundaries between MailIQ and external services.

The major integration areas are:

- Google
- Microsoft
- Groq
- WhatsApp
- Telegram
- Slack
- Discord
- Paystack

Each integration needs to be tested both independently and as part of the complete workflow where practical.

---

## 22. Regression Testing

Regression testing is important because changes to shared workflow components can affect multiple customer variants.

A change to a shared processing component can potentially affect:

    Gmail + WhatsApp
    Gmail + Telegram
    Gmail + Slack
    Gmail + Discord
    Outlook + WhatsApp
    Outlook + Telegram
    Outlook + Slack
    Outlook + Discord

and the remaining supported workflow combinations.

The 16 workflow variants therefore form an important regression-testing surface.

---

## 23. QA Workflow

The overall QA process can be represented as:

    Change
      │
      ▼
    Component Test
      │
      ▼
    Integration Test
      │
      ▼
    Workflow Test
      │
      ▼
    Variant Regression Test
      │
      ▼
    End-to-End Test
      │
      ▼
    Production Validation

This provides progressively broader confidence as a change moves toward production.

---

## 24. Test Evidence

Testing evidence should ideally include:

- Workflow execution results
- Successful OAuth connections
- Failed OAuth scenarios
- AI output validation results
- Webhook test payloads
- Delivery confirmations
- Error-handler executions
- Retry executions
- Variant test results

Where practical, evidence should be stored alongside the project documentation without exposing customer data, credentials, tokens, or other sensitive information.

---

## 25. Test Data and Privacy

Production customer data should not be used unnecessarily for testing.

Test data should be designed to represent relevant scenarios while avoiding exposure of:

- Real email contents
- Access tokens
- Refresh tokens
- API keys
- Customer identifiers
- Personal information

Any evidence committed to the repository should be sanitised before publication.

---

## 26. QA Principles

### Test the System, Not Just the Node

A successful individual node does not guarantee a successful customer journey.

### Test Failure Paths

Production systems need reliable behaviour when dependencies fail.

### Test Integration Boundaries

External APIs are common sources of unpredictable behaviour.

### Test All Supported Variants

Shared workflow components can create cross-variant regressions.

### Validate AI Output

Model output must be treated as untrusted until validated.

### Test Customer Isolation

Multi-tenant systems must prevent cross-customer data access.

### Test Recovery

Retries and error handlers must be tested rather than assumed to work.

---

## 27. Testing Summary

MailIQ's QA approach covers the full path from external event ingestion to customer-facing delivery.

The major tested areas include:

- OAuth authentication
- Google integration
- Microsoft integration
- Webhook payloads
- AI output validation
- 12-category classification
- 1–10 urgency scoring
- User overrides
- SKIP logic
- Memory context
- Multi-channel delivery
- Retry behaviour
- Error handlers
- Customer disconnects
- 16 workflow variants
- End-to-end execution

The objective is to provide confidence that the system remains reliable not only when individual components work correctly, but also when integrations fail, inputs are invalid, or workflow execution needs to recover.
