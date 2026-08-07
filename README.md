# MailIQ

> AI-powered email intelligence SaaS that turns incoming Gmail and Outlook email into structured, actionable intelligence and delivers it through the communication channels teams already use.

[![Status](https://img.shields.io/badge/Status-Production_System-18181B?style=flat-square)](#project-status)
[![Architecture](https://img.shields.io/badge/Architecture-Multi--Tenant-18181B?style=flat-square)](#architecture)
[![n8n](https://img.shields.io/badge/Orchestration-n8n-18181B?style=flat-square)](#technology)

---

## Overview

MailIQ is a multi-tenant AI email intelligence platform designed to continuously monitor connected Gmail and Outlook accounts, analyse incoming messages, and deliver structured intelligence through WhatsApp, Telegram, Slack, or Discord.

Rather than simply summarising email, MailIQ processes each message through a structured AI pipeline that determines its category, urgency, important details, deadlines, and recommended action.

The platform also provisions personalised AI workflows for customers automatically, allowing new accounts to be onboarded without manually creating or configuring workflows for each customer.

---

## What MailIQ Does

```text
Gmail / Outlook
       │
       ▼
 Email Ingestion
       │
       ▼
 AI Processing
       │
       ├── Classification
       ├── Urgency Scoring
       ├── Key Detail Extraction
       ├── Deadline Detection
       └── Action Recommendation
       │
       ▼
 Structured Result
       │
       ▼
 Personalised Delivery
       │
       ├── WhatsApp
       ├── Telegram
       ├── Slack
       └── Discord
