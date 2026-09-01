# Public evidence security policy

## Never commit

- OAuth client secrets or refresh tokens
- provider API keys
- n8n credential payloads
- database connection strings
- Paystack secrets
- real email content or customer identifiers
- production webhook URLs containing private tokens
- private Drive URLs or internal access details

## Before publishing a workflow export

- inspect `credentials`, headers, query parameters, webhook URLs, code nodes, sticky notes, sample payloads, and pinned data;
- replace account-specific IDs and destinations with descriptive placeholders;
- remove execution data;
- confirm the workflow is inactive;
- run a secret scan;
- review the diff manually.

## Runtime design intent

The v5 architecture specifies encrypted token storage, bounded JWT verification, rotated refresh tokens with reuse detection, authenticated internal webhooks, idempotent event ingestion, and explicit tenant ownership constraints. These are design requirements until a particular deployment is configured and tested.
