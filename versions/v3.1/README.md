# MailIQ v3.1 — Historical Node-Level Build Expansion

[← Version Table of Contents](../TABLE_OF_CONTENTS.md) · [Architecture Diagram](ARCHITECTURE.md)

**Status:** HISTORICAL FALLBACK  
**Primary surviving authority:** Complete Build Spec v3.1 + backend specification.

## What this generation adds

v3.1 expands the v3 architecture into detailed node-level workflow and backend build guidance. In the archive it is the preferred historical fallback when a later document references behavior but does not contain the same node-level specificity.

## Architecture

[Open the v3.1 architecture diagram →](ARCHITECTURE.md)

The diagram presents the node-level processing pattern: trigger → validation → authoritative state load → provider operation → processing → persistence → tenant-aware delivery/error path.

## Architectural relationship

v3.1 should be read as implementation-detail expansion on the v3 state/infrastructure direction, not as current authority over v4/v5 decisions.

## Workflow relationship

This generation is useful for reconstructing historical workflow intent because it contains node-level specifications. It is therefore a legitimate fallback source when rebuilding missing documentation, but it must be labelled as historical whenever later architecture changed the behavior.

## Supersession rule

Where v3.1 conflicts with v4.1 or v5.0:

1. v5.0 architecture decisions win;
2. v4.1 explains important transition rationale;
3. v3.1 can supply historical node-level detail only where compatible.

## Evidence boundary

**Supported:** detailed historical workflow/backend specifications and implementation intent.  
**Not supported:** current runtime behavior or a claim that v3.1 node-level specifications remain unmodified in v5.

## Media

Historical version. Architecture is documented; demo/screenshot evidence is not fabricated.
