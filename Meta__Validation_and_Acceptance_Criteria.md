# Validation & Acceptance Criteria

## Status
**Authoritative (Execution Hardening)**

---

## Purpose

This document defines **objective acceptance criteria** for each major phase and artifact.
It answers one question only:

> “How do we know this is complete enough to move forward?”

If criteria are not met:
- Stop
- Do not proceed to the next phase

---

## Global Validation Rules (Apply Everywhere)

All artifacts must satisfy:

- Builds cleanly (no hidden failures)
- Honors all locked rules in:
  - `Architecture/*`
  - `Global_Naming_and_Terminology.md`
  - `System_Boundaries_and_NonGoals.md`
- No guessed names
- No invented entities
- No silent behavior
- All tenant-scoped items include `TenantUniqueId`
- All deletes are soft deletes

---

## Phase 1 — Schema Validation

Acceptance Criteria:
- All tables have `UniqueId` PK (GUID)
- All tenant-owned tables include `TenantUniqueId`
- All FK names follow `<EntityName>UniqueId`
- Defaults use `SYSUTCDATETIME()` and `newsequentialid()`
- No pluralization or renaming drift
- Soft delete implemented consistently (`IsDeleted`)

Blocking Failures:
- Missing tenant filter
- Hard delete
- Inconsistent naming
- Schema guessing

---

## Phase 2 — SqlCatalog Reads Validation

Acceptance Criteria:
- All reads go through SqlCatalog
- No inline SQL in application code
- Explicit column lists only
- Tenant filtering present in every query
- Queries return flat DTOs only

Blocking Failures:
- `SELECT *`
- Missing tenant filter
- Inline SQL usage

---

## Phase 3 — API Writes Validation

Acceptance Criteria:
- All writes go through API
- All calls use `ResilientApiCaller.CallAsync`
- All write operations are auditable
- No synchronous dependency on Notifications

Blocking Failures:
- Direct DB writes
- Notification-dependent workflows
- Missing audit coverage

---

## Phase 4 — MAUI UX Validation

Acceptance Criteria:
- Pages implemented strictly in locked order
- XAML + code-behind only
- Navigation matches plan exactly
- Context visibility is explicit
- Module gating respected

Blocking Failures:
- Evidence UX before Case/Incident UX
- Navigation changes without approval
- Code-only views

---

## Phase 5 — Notifications Validation

Acceptance Criteria:
- Notifications are additive only
- Notification failure does not block workflows
- Audit exists for:
  - Emission
  - Delivery attempts
  - Failures
  - Throttling
- Subscriptions are explicit and tenant-scoped

Blocking Failures:
- Workflow dependency on notifications
- Missing audit coverage
- Implicit subscriptions

---

## Phase 6 — Chat Overlay (Obscura) Validation

Acceptance Criteria:
- Matches all Obscura planning docs
- Read-only by default
- Explicit confirmation for any action
- Fully auditable interactions
- No background execution

Blocking Failures:
- Autonomous behavior
- Hidden state
- Permission bypass

---

## Phase 7 — V2 / Deferred Work Validation

Acceptance Criteria:
- Clearly marked as deferred
- Does not impact V1 behavior
- No bleed into core workflows

Blocking Failures:
- OSINT required for V1
- Automation assumptions
- Undocumented expansion

---

## Stop-and-Ask Triggers (Mandatory)

Stop and ask if:
- A name or schema element is unclear
- A rule appears contradictory
- A shortcut would save time but violate discipline

---

## Summary

Completion is not “it works.”
Completion is **it meets criteria without violating rules**.

This document is the gatekeeper.
