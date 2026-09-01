# Workflow evidence

This directory contains representative MailIQ n8n artifacts selected from the Drive archive.

## Included

### `sanitized/SW-01_Onboarding_Factory_SANITIZED.json`

A 24-node sanitized export of the onboarding/factory workflow. Credential references are redacted and URLs/IDs use placeholders.

Use it to inspect:

- factory-style tenant provisioning;
- external resource creation;
- state handoff between workflow steps;
- the provisioning mismatches documented in [Reliability findings](../docs/reliability-and-rebuild.md).

### `historical/MailIQ_n8n_import_fixed.json`

A 70-node historical import artifact. It is inactive and uses placeholder values for provider/application configuration.

Use it as evolution evidence—not as the current canonical implementation.

## Do not import blindly

1. Review every node and expression.
2. Replace placeholders only in a controlled environment.
3. Create new credentials inside n8n.
4. Use test provider accounts and synthetic messages.
5. Keep workflows inactive until success, failure, duplicate, and replay paths pass.
6. Never commit a freshly exported workflow without reviewing embedded IDs, URLs, examples, and credentials.

The complete canonical inventory is documented in [workflow-catalog.md](../docs/workflow-catalog.md). The repository intentionally does not mass-publish every Drive export.
