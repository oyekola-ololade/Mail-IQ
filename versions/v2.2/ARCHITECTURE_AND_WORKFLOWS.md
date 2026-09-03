# MailIQ v2.2 — Architecture & Workflow Record

**Version class:** HISTORICAL BUILD SPEC  
**Primary authority:** Complete Build Spec v2.2  
**Known workflow scale:** 36 workflow definitions in the surviving build specification.

## Architectural direction

v2.2 formalized MailIQ as a two-layer system and made the workflow decomposition materially more explicit. The surviving build record describes **36 workflow definitions**, n8n credential assumptions and MinIO in the architecture.

## What the 36-workflow generation proves

This version is evidence that MailIQ was designed as a coordinated system of many workflows rather than one oversized automation. The workflow definitions covered system responsibilities across onboarding/provisioning, email processing, integrations/delivery and operational behavior.

The exact historical bundle must still be provenance-matched before individual JSON files are published under this version.

## Major design characteristics

- two-layer system decomposition;
- explicit multi-workflow build specification;
- n8n credential assumptions that later became a scaling/state concern;
- MinIO included in the infrastructure model;
- more concrete build-level responsibilities than v1.x.

## Why it changed

Later generations corrected several assumptions:

1. dynamic/per-user n8n credential creation was not retained as the primary tenancy model;
2. OAuth/provider state moved toward PostgreSQL authority;
3. infrastructure converged toward Railway services;
4. MinIO was eventually removed from the current design;
5. shared workflow definitions replaced per-client proliferation.

## Workflow artifact policy

Do not substitute the later 35-workflow design set or 38-export candidate pool for the v2.2 36-workflow generation. If original v2.2 JSON/spec artifacts are mapped, place them under `artifacts/` and record their provenance.

## Evidence status

| Area | Status |
|---|---|
| Complete Build Spec | SURVIVES / HISTORICAL |
| 36 workflow definitions | DOCUMENTED |
| Exact publishable JSON set | NOT YET PROVEN/MAPPED |
| MinIO design | HISTORICAL ONLY |
| Credential model | HISTORICAL / SUPERSEDED |
| Demo/screenshots | no placeholders for historical versions |

## Supersession

Superseded by v3.0, which changed provider/OAuth and infrastructure decisions substantially.