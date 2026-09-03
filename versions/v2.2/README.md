# MailIQ v2.2 — Historical Complete Build Specification

[← Version Index](../INDEX.md) · [Architecture Diagram](ARCHITECTURE.md)

**Status:** HISTORICAL  
**Primary surviving authority:** Complete Build Spec v2.2  
**Role in lineage:** first strongly explicit two-layer build decomposition with a large named workflow set.

## System direction

v2.2 described MailIQ as a two-layer system and made the implementation plan much more concrete. The surviving control record associates this generation with:

- **36 workflow definitions**;
- n8n credential-oriented assumptions for provider access;
- MinIO in the architecture;
- a more explicit build decomposition than earlier versions.

## Architecture

[Open the v2.2 architecture diagram →](ARCHITECTURE.md)

The diagram preserves the two-layer build, 36-workflow generation, n8n credential-oriented provider access, database state and MinIO relationship as a distinct historical architecture.

## Workflow interpretation

The 36-workflow count belongs to this historical build generation. It must not be merged with the later 35-workflow design set or the later 38-export candidate pool and called one canonical total.

A future public historical workflow bundle should live under a provenance-labelled path such as `workflows/historical/v2.2/` only when the underlying files are confidently mapped to this generation and sanitized.

## Important assumptions later changed

### Credential/OAuth handling
v2.2 relied more heavily on n8n credential assumptions. Later versions moved provider token/OAuth state toward PostgreSQL-backed authoritative state to reduce scaling and provenance problems.

### Object storage
MinIO appears in this generation. It is not part of the current v5 default architecture.

### Workflow tenancy
Later architecture moved away from per-client/dynamic workflow proliferation toward shared definitions with isolated tenant execution/context.

## Why v2.2 matters

It is one of the strongest historical records for how MailIQ was intended to be built at workflow level before the v3/v4 state-management corrections.

## Evidence boundary

**Supported:** a detailed v2.2 build specification with 36 workflow definitions and the stated infrastructure assumptions.  
**Not supported:** current runtime status, current provider credential strategy, current MinIO use, or equivalence to the v5 candidate workflow pool.

## Media

Historical version. Architecture is documented; demo/screenshot evidence is not fabricated.
