# Execution Order & Dependency Graph

## Status
**Authoritative (Execution Hardening)**

---

## Purpose

This document defines the **only allowed execution order** for building CaseBunker from the plan.
It prevents rework, scope bleed, and premature UI or subsystem implementation.

This document is binding for all future work (human or AI).

---

## Global Rule

**No downstream work may begin until upstream prerequisites are complete.**

If a prerequisite is missing or ambiguous:
- Stop
- Ask
- Do not guess

---

## Phase 0 — Foundations (Must Be Green)

Prerequisites:
- Solution builds
- Basic CI/build scripts (if any) run locally
- Repo structure is stable

Outputs:
- Clean build
- No warnings that mask failures

---

## Phase 1 — Schema Foundations

Order:
1. Tenant / Identity foundations (already designed/in progress)
2. Core domain tables:
   - Case
   - Incident
3. Evidence tables:
   - EvidenceItem
   - EvidenceFile
   - Custody events
4. Notifications tables:
   - NotificationEvent
   - Subscription
   - Delivery
   - Throttling/quota support (conceptual; schema later)

Rules:
- GUID `UniqueId` PK everywhere
- `TenantUniqueId` on all tenant-owned tables
- Soft delete only (`IsDeleted`)
- No table naming changes
- Defaults use `SYSUTCDATETIME()` and `newsequentialid()`

---

## Phase 2 — SqlCatalog Reads

Order:
1. Case list + case detail queries
2. Incident list + incident detail queries
3. Evidence list + evidence detail queries
4. Notification rollups (already started in earlier work)

Rules:
- No inline SQL in application code
- SqlCatalog queries must include tenant filters
- Explicit columns only (no `SELECT *`)

---

## Phase 3 — API Write Surface

Order:
1. Case create/update/close/soft-delete
2. Incident create/update/soft-delete
3. Evidence create + add attachment + custody event
4. Notification emission and subscription management (additive)

Rules:
- All writes through API using ResilientApiCaller.CallAsync
- No synchronous dependency on Notifications
- All actions auditable

---

## Phase 4 — MAUI UX (Strict Page Order)

Hard order (locked):
1. Case List
2. Case Detail
3. Incident List
4. Incident Detail
5. Evidence List
6. Evidence Detail

Rules:
- XAML + code-behind only
- No navigation changes without explicit approval
- Module gating controls visibility (Evidence/Notifications/Chat Overlay)

---

## Phase 5 — Notifications (Non-Blocking Integration)

Order:
- Event emission instrumentation (audit + event creation)
- Delivery attempts (channel by channel)
- Throttling enforcement
- Subscription management UX (future)

Rules:
- Failures never block core operations
- Audit coverage for emission, delivery attempts, failures, throttling

---

## Phase 6 — Chat Overlay (Obscura)

Status:
- Design complete (pre-Pro requirement)
- Build deferred until core workflows are stable

Rules:
- Read-only by default
- No autonomous actions
- No background execution
- Fully auditable interactions

---

## Phase 7 — V2 / Deferred Work

Includes:
- OSINT
- advanced analytics
- advanced automation

Rules:
- Must not leak into V1 phases
- Must be explicitly re-approved for inclusion

---

## Dependency Graph (Summary)

- Schema → SqlCatalog Reads → API Writes → MAUI Pages
- Evidence UX depends on Case+Incident UX completion
- Notifications must never be a prerequisite for any workflow
- Chat Overlay depends on stable core domain + UX

---

## Stop Conditions (Mandatory)

Stop and ask if:
- Table/entity name is unknown
- Column name is unknown
- Scoping (Tenant vs Business Unit) is ambiguous for a feature
- A workflow requires notifications to succeed
- A change would affect navigation without approval

---

## Summary

This document is the execution spine.
Following it reduces risk and accelerates time-to-test after Pro upgrade.
