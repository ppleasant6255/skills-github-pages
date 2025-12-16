# Architecture — Modules & Feature Flags

## Status
**Authoritative**

This document defines module enablement behavior in CaseBunker.

---

## Purpose
Modules allow tenant-controlled runtime capability toggles affecting UI, API, and execution.

---

## Core Principles
1. Tenant-controlled
2. Explicitly enabled/disabled
3. Disabled = invisible and inactive
4. Modules never block core workflows
5. Module state is auditable

---

## Module States
Per tenant:
- Enabled
- Disabled

---

## Tenant Control
Only Tenant Admins may enable/disable modules.
Business Units may not override tenant module state unless explicitly documented as additive.

---

## Default Module Behavior

### Core Modules (Always Enabled)
- Cases
- Incidents
- Identity & Access
- Audit Logging

### Optional Modules
Examples:
- Evidence
- Notifications
- Chat Overlay
- OSINT
- AI Reports
- Geofencing
- Surveillance

---

## Behavior When Disabled (Hard Rules)

### UI
- No navigation entry
- No menu items
- No deep links
- No settings pages

### API
- Reject access with clear, audited denial
- No silent fallback

### Background & Execution
- No jobs, schedules, or queued tasks

### Data
- Preserve existing data
- Create no new data
- Mutate no data

Disabled means inactive, not hidden.

---

## Module Enablement and Audit
Must audit:
- Enablement
- Disablement
- Attempted access to disabled module

---

## Modules and UX
No placeholders, dead links, or broken flows for disabled modules unless explicitly designed.

---

## Modules and Chat Overlay
Chat Overlay is treated as a module.
Disabled overlay means no invocation and no background execution.

---

## Forbidden Patterns
- Auto-enabling modules
- Implicit enablement
- Cross-module dependencies forcing enablement
- “Soft disabled” modules that still execute

---

## Summary
Modules are tenant-controlled capabilities. Disabled means inactive and invisible. Core modules are always on.
