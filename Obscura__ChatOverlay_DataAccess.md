# Chat Overlay — Data Access

## Status
**Authoritative**

This document defines what data Obscura may access and how.

---

## Access Model

- All data access flows through existing APIs
- No direct database access
- No inline SQL
- Respect Tenant and Business Unit scoping

---

## Allowed Data

Read-only access to:
- Case metadata
- Incident metadata
- Evidence metadata (no file mutation)
- Notification history
- Audit summaries (if user permitted)

---

## Prohibited Data

- Raw credentials
- Secrets
- Cross-tenant data
- OSINT providers (v1)

---

## Data Freshness

- Responses reflect current persisted state
- No speculative or predictive data

---

## Audit Requirements

All data access by Obscura must generate audit events consistent with `Architecture/AuditLogging.md`.
