# MailIQ v1.1 — Historical Workflow-Heavy Architecture

[← Version Index](../INDEX.md) · [Architecture Diagram](ARCHITECTURE.md)

**Status:** HISTORICAL  
**Primary surviving authority:** Complete Workflow Architecture v1.1  
**Role in lineage:** materially more n8n-centric than v1.0.

## What changed

v1.1 pushed MailIQ toward a mostly/all-n8n architecture and materially changed the assumptions around how application behavior and workflow orchestration were divided.

## Architecture

[Open the v1.1 architecture diagram →](ARCHITECTURE.md)

The diagram visualizes the workflow-heavy direction recorded for this generation and the concentration of provider/intelligence/delivery behavior around n8n.

## Architectural direction

This generation is important because it represents the point where workflow orchestration became a much larger part of the product design. Later generations reversed some of that concentration by restoring a clearer application/API boundary and moving authoritative state outside dynamic workflow credentials.

## Workflow model

The archive records a complete workflow architecture for this generation, but the current public GitHub repository does not contain a verified complete v1.1 JSON set. Any future historical export added here must be tied to v1.1 by source metadata/document evidence rather than filename resemblance.

## Why it was superseded

Later design work identified the need for:

- clearer API/backend responsibility;
- scalable credential/OAuth state management;
- stronger tenant/state provenance;
- more explicit deployment and operations design.

## Evidence boundary

**Supported:** a real workflow-heavy v1.1 architecture existed and materially changed the initial system direction.  
**Not supported:** that all later workflows belong to v1.1, that this architecture remained current, or that the v1.1 system was production-ready.

## Media

Historical version. Architecture is documented; demo/screenshot evidence is not fabricated.
