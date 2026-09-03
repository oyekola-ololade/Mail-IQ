# MailIQ v1.0 — Architecture & Workflow Record

**Version class:** HISTORICAL BASELINE  
**Primary authority:** Architecture Specification v1.0  
**Runtime status:** not current; complete publishable JSON bundle not recovered.

## System boundary

v1.0 is the earliest named MailIQ architecture retained in the reconstructed archive. It established the product problem, provider/inbox processing boundary and the first system-level decomposition before later generations repeatedly changed tenancy, credentials, backend responsibility and deployment.

## Workflow evidence

The archive supports the existence of an early architecture/workflow model, but it does **not** support reconstructing a complete v1.0 n8n bundle from later exports. No later JSON should be relabelled as v1.0.

### What can be stated

- MailIQ already centered on turning inbox activity into structured intelligence and downstream action.
- Provider ingestion, processing/classification and delivery concepts existed at the architecture level.
- Later workflow counts and node-level specifications must not be projected backward into v1.0.

### Artifact rule

If a historical JSON is later provenance-matched to v1.0, add it under `artifacts/` with a source note and sanitization record. Until then this version remains documentation-led evidence.

## Why it changed

Later versions introduced increasingly explicit workflow decomposition, backend/API responsibility, multi-tenant state handling, provider-token lifecycle, deployment choices and operational controls.

## Evidence status

| Area | Status |
|---|---|
| Architecture specification | SURVIVES / HISTORICAL |
| Complete workflow inventory | NOT ESTABLISHED |
| Complete JSON bundle | NOT RECOVERED |
| Runtime test evidence | NOT CURRENTLY MAPPED |
| Demo/screenshots | no placeholders for historical versions |

## Supersession

Superseded by v1.1 and later generations. Use v5.0 for current architecture decisions.