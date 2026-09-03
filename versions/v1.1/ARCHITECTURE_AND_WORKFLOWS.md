# MailIQ v1.1 — Architecture & Workflow Record

**Version class:** HISTORICAL  
**Primary authority:** Complete Workflow Architecture v1.1  
**Runtime status:** historical; no complete current-safe JSON bundle is represented as recovered.

## Architectural direction

v1.1 moved MailIQ toward a much more workflow-centric design. The surviving archive describes this as a mostly/all-n8n direction relative to the earlier baseline and materially changes the assumptions about how application/backend logic and workflow orchestration are divided.

## Workflow interpretation

This generation is important because MailIQ begins to look less like a single automation and more like a coordinated workflow system. However, the current archive control does not establish a complete, safely publishable v1.1 export set.

### Supported interpretation

- stronger n8n-centric workflow decomposition;
- multiple cooperating workflow responsibilities rather than a single monolithic flow;
- early design decisions later reconsidered when state, credentials, tenancy and application boundaries became more explicit.

### Do not infer

- that later 35/36/38 workflow counts belong to v1.1;
- that any v5-era workflow is a valid v1.1 artifact;
- that v1.1 was a current production deployment.

## Change from v1.0

The key change is the move from a broad early architecture into a more explicit workflow architecture. Later versions then reintroduced/clarified an API/backend boundary and hardened state ownership.

## Evidence status

| Area | Status |
|---|---|
| Workflow architecture document | SURVIVES / HISTORICAL |
| Exact complete workflow count | NOT PROMOTED FROM LATER VERSIONS |
| Complete JSON bundle | NOT RECOVERED AS A VERIFIED SET |
| Current runtime evidence | NO |
| Demo/screenshots | no placeholders for historical versions |

## Supersession

Superseded by v2.2 and later generations.