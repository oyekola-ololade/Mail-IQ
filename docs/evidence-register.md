# Evidence register

## Drive inventory reviewed

The MailIQ Drive tree was recursively inspected before this repository update.

| Artifact type | Count |
|---|---:|
| JSON workflows/exports | 76 |
| PDF | 12 |
| DOCX | 6 |
| HTML | 9 |
| Markdown | 2 |
| PNG | 7 |
| JPEG | 1 |
| Presentations | 2 |
| **Total** | **115** |

The archive spans architecture specifications, workflow exports, frontend/UI prototypes, evidence media, presentations, build folders, logic audits, and handoff/truth-control documents.

## Evidence classes

| Evidence | What it supports | Public handling |
|---|---|---|
| MailIQ v5 master architecture | Current system intent and design decisions | Summarized in repository docs |
| 19 system workflow JSON files | Lifecycle, provider, operations, and control-plane implementation evidence | Catalogued; one sanitized representative published |
| 16 child-template JSON files | Gmail/Outlook × channel routing matrix | Catalogued; retained privately pending per-file review |
| Older 38-export set | Earlier architecture and implementation evolution | Counted separately; one placeholder-configured import published |
| Logic audit | Defects, contradictions, and rebuild priorities | Summarized in reliability findings |
| Build specifications | Data model, workflow behavior, infrastructure, and security intent | Used to reconcile current docs |
| Official MailIQ logo | Product identity | Published in `assets/` |
| Architecture overview image | Historical visual evidence | Published with an explicit historical label |
| UI/onboarding HTML | Interface history | Not published in this update |
| Evidence media/presentations | Historical proof and mixed project collateral | Not mass-published |

## Safety decision

The source archive contains material that must not be public, including credential-bearing documents, OAuth-secret files, and onboarding HTML carrying provider keys. Those files were excluded.

The public repository contains:

- the official logo;
- a labelled historical architecture image;
- evidence-derived documentation;
- a representative workflow with redacted credential references;
- an older import artifact configured with placeholders.

It does **not** contain:

- OAuth client secrets;
- live provider/API keys;
- database credentials;
- customer or personal email content;
- private Drive links;
- evidence files belonging to other projects.

## Truth boundary

Accurate public description:

> MailIQ is a substantial multi-tenant email-intelligence prototype, previously trialled and currently offline.

Allowed evidence-backed claims:

- Gmail and Outlook monitoring designs and exports exist.
- Structured classification, urgency scoring, extraction, and routing logic exist.
- Multi-channel routing includes WhatsApp, Telegram, Slack, and Discord.
- Multi-tenant, OAuth, subscription, operational, and reconciliation designs exist.
- The canonical Drive set contains 19 system workflows and 16 child templates.

Claims not made:

- live SaaS;
- paying customers;
- verified automatic provisioning end to end;
- production-ready reliability or security;
- all 35 workflows running as one deployed environment.

## Evidence versioning

The v5 master architecture supersedes the proposed v4.1 architecture where they conflict. Older assets remain useful for demonstrating system evolution, but current repository explanations use v5 as the architectural source of truth.
