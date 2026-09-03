# 07 — Conversational Agent / Tool Workflows

**Subsystem status:** later candidate workflows documented; public JSON publication/revalidation pending.

## Candidate workflows

- `SW-20 Conversational Agent`
- `TW-01 Calendar`
- `TW-02 Email Search`
- `TW-03 Settings`
- `TW-04 Draft / Send`
- `TW-05 Token Refresh Handler`

## System role

This later-generation group exposes controlled conversational/tool actions on top of MailIQ state and integrations rather than treating a language model as the system of record.

## Control principles

- tools operate through defined actions/contracts;
- deterministic state/permission checks should surround consequential actions;
- token/provider state remains authoritative outside free-form model output;
- draft/send actions require clear identity/authorization boundaries;
- failures should return explicit tool/error state rather than fabricated success.

## Verification needs

- tool-call input validation;
- tenant/account scoping;
- calendar/search/settings result correctness;
- draft vs send distinction;
- token-refresh failure handling;
- model/tool error behavior;
- no leakage of credentials or cross-tenant email state.