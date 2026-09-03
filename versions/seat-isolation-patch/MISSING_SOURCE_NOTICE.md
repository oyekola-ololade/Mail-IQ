# MailIQ — Seat-Isolation Patch Record

**Status:** REFERENCED HISTORICAL PATCH — ORIGINAL STANDALONE SOURCE NOT LOCATED

The archive records an intermediate seat-isolation hardening patch that addressed tenant/seat state separation before the v5 architecture consolidated the final direction.

## Supported interpretation

- tenant/seat isolation became an explicit design concern;
- the patch's intent is reflected in later v5 state/tenancy rules;
- the original standalone patch artifact was not located during the 2026-09-03 audit.

## Do not fabricate

Do not manufacture a patch diff, workflow export or exact schema migration. Later v5 text may explain the resulting state model but must not be relabelled as the missing original patch.

## Recovery procedure

If the original patch is later found:
1. preserve the raw source unchanged;
2. record source path/date/hash;
3. compare against v4.1 and v5;
4. document exact affected tenant/seat state contracts;
5. map any workflow/schema changes with provenance.

Historical patch: no demo/screenshot placeholders.