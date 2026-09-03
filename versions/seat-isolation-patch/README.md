# MailIQ — Seat-Isolation Patch Record

[← Version Table of Contents](../TABLE_OF_CONTENTS.md) · [Patch Architecture](ARCHITECTURE.md)

**Status:** REFERENCED PATCH / ORIGINAL NOT LOCATED  
**Relationship:** incorporated into the mature v5 state-isolation direction.

## Purpose supported by the archive

The patch addressed tenant/seat state isolation. It belongs to the sequence of corrections that made client/account/seat ownership more explicit and reduced the risk of cross-tenant or ambiguous state handling.

## Architecture

[Open the seat-isolation architecture diagram →](ARCHITECTURE.md)

The diagram shows only the supported architectural purpose: owner resolution, tenant/seat-scoped execution context, authoritative state access and same-owner persistence. Exact historical SQL/node changes are not invented.

## What is not preserved

The standalone original patch text was not located in the 2026-09-03 audit. Exact SQL, workflow-node changes, migration statements or test outputs must therefore not be invented.

## Current interpretation

Use v5.0 as the current authority for tenant/seat state handling. This record exists to preserve the fact that a dedicated isolation correction occurred in the lineage.

## Media

Architecture is documented. Demo/screenshot runtime evidence is not fabricated.
