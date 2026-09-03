# 04 — Notifications / Delivery Coordination

**Subsystem status:** candidate workflows documented; public JSON publication/revalidation pending.

## Candidate workflows

- `SW-05 Notification Engine`
- `SW-07 Digest Dispatcher`
- `SW-08 Quiet Hours Flush`
- `SW-08b Telegram Chat ID Capture`
- `SW-09 Slack OAuth Callback`
- `SW-10 Discord Bot Join Handler`

## System role

This group manages how processed MailIQ results reach configured destinations and how destination-specific identity/configuration is established.

## Coordination responsibilities

- immediate vs digest-style delivery;
- quiet-hours deferral and later flush;
- destination identity/config capture;
- integration callbacks;
- delivery result/state handoff to operational/account state.

## Verification needs

- correct tenant destination selection;
- quiet-hours behavior across boundary times;
- digest deduplication;
- destination authorization/config failure;
- retry without duplicate delivery;
- partial destination outage surfaced rather than reported as complete success.