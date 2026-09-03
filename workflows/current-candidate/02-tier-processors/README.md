# 02 — Tier Processors

**Subsystem status:** recovered candidate exports documented; public JSON publication/revalidation pending.

## Candidate workflows

- `Free Tier Processor`
- `Basic Tier Processor`
- `Standard Tier Processor`
- `Premium Tier Processor`

These represent plan-specific processing behavior in the later candidate pool.

## System role

Provider events are normalized/routed into the appropriate processing path using authoritative tenant/account/plan state. The processor then performs the plan-supported classification/extraction/routing behavior and contributes to delivery/usage state.

## Verification needs

For each plan path verify:

- correct account/plan selection;
- no cross-tenant state leakage;
- classification/extraction outputs;
- plan-specific limits/features;
- delivery handoff;
- usage metering;
- malformed message and provider failure behavior.

## Publication rule

Do not infer that a plan processor is current merely because a similarly named export exists in an older build generation.