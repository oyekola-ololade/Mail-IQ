# MailIQ v3.1 — Architecture & Workflow Record

**Version class:** HISTORICAL IMPLEMENTATION-DETAIL GENERATION  
**Primary authority:** Complete Build Spec v3.1 + backend specification  
**Archive role:** node-level historical fallback when later v5 companion detail is missing.

## What v3.1 added

v3.1 expanded the v3 architecture into much more detailed workflow-generation and backend/build instructions. It is one of the most useful historical sources for understanding node-level intent, but it is **not** current architecture authority.

## Workflow-system interpretation

This generation contains detailed node-level specifications for multiple system workflows and therefore provides useful historical implementation intent for:

- workflow responsibilities;
- inputs/outputs;
- database/state writes;
- provider/API calls;
- routing/branch behavior;
- operational sequences.

When the reconstructed v5 workflow companion needs a historical fallback for node-level behavior, v3.1 can be consulted **only after** v5 architecture and later export evidence.

## Important limitation

A v3.1 node-level spec can describe behavior that was later changed by v4.1/v5.0. Therefore:

1. do not call a v3.1 workflow current merely because its specification is detailed;
2. do not overwrite later state/tenancy decisions with older node-level instructions;
3. preserve provenance when a surviving JSON appears to match this generation.

## Change from v3.0

The architecture direction is broadly expanded into implementation detail rather than completely replaced. The major architectural break comes later with v4.1's shared-workflow/tenant-isolation model.

## Evidence status

| Area | Status |
|---|---|
| Complete Build Spec / backend spec | SURVIVES / HISTORICAL |
| Node-level workflow detail | STRONG HISTORICAL SOURCE |
| Complete provenance-mapped JSON bundle | NOT YET ESTABLISHED |
| Current architecture authority | NO |
| Demo/screenshots | no placeholders for historical versions |

## Supersession

Superseded as architecture authority by v4.1 and v5.0; retained as historical fallback detail.