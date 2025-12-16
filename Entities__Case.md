# Entity — Case

## Status
**Authoritative (Core Domain)**

This document defines the **Case** entity as the top-level investigation container.
Case is a **core module** concept and must exist in all deployments.

See also:
- `docs/plan/Architecture/Tenancy.md`
- `docs/plan/Architecture/BusinessUnits.md`
- `docs/plan/Architecture/AuditLogging.md`

---

## Purpose

A Case represents the primary container for an investigation.
All Incidents, Evidence, Notes, Tasks, Participants, Notifications, and (later) AI/Chat Overlay interactions roll up to a Case.

Cases are the primary unit for:
- Investigator workflow
- Reporting
- Access and visibility boundaries (subject to Tenant and Business Unit scoping rules)

---

## Ownership and Scope

### Tenant Scope (Required)
Case is tenant-owned and must include:
- `TenantUniqueId` (required)

### Business Unit Scope (Explicit, TBD)
Business Unit behavior must be explicit (silence is not permission).

**This entity must declare one of the approved scoping models:**
- Tenant-only
- BusinessUnit-scoped
- Hybrid

**Current decision:** Not yet finalized.
- Include `BusinessUnitUniqueId` as **explicitly optional** until Business Unit scoping is finalized.

---

## Required Fields (Minimum Contract)

> This section defines the minimum stable contract. Additional fields may be added later, but these must not be removed.

### Identity / Tenancy
- `UniqueId` (GUID, PK)
- `TenantUniqueId` (GUID, NOT NULL)
- `BusinessUnitUniqueId` (GUID, NULLABLE) — see scoping above

### Display / Search
- `CaseNumber` (string, required) — human-friendly identifier
- `Title` (string, required)
- `Description` (string, nullable)

### Status
- `StatusKey` (string, required) — e.g., Open / Suspended / Closed
- `PriorityKey` (string, nullable) — tenant-defined lookup
- `ClosedUtc` (datetime, nullable)

### Ownership
- `OwnerUserUniqueId` (GUID, required)

### System Fields
- `CreatedUtc` (datetime, required; UTC)
- `UpdatedUtc` (datetime, required; UTC)
- `IsDeleted` (bit, required; soft-delete only)

---

## Relationships (Conceptual)

### One-to-Many (Case → Child)
- Incidents (required concept)
- CaseNotes (future)
- CaseTodos / Tasks (future)
- CaseParticipants (future)
- CaseTags (future)

### Rollups (Case aggregates via Incident)
- Evidence and files (incident-scoped)
- OSINT results (deferred)
- Notifications (additive; must not block workflows)

---

## Business Rules

- A Case may exist with **zero Incidents** initially.
- Case closure does not hard-close incidents or evidence.
- Deletion is **soft delete only** (`IsDeleted = 1`).
- Tenant isolation is mandatory for all reads and writes.

---

## Audit Requirements

The following actions must be audited (see `Architecture/AuditLogging.md`):
- Case creation
- Case updates
- Case closure / status changes
- Case soft-delete
- Permission/visibility changes (when introduced)

Audit records must include `TenantUniqueId` and include `BusinessUnitUniqueId` when BU-scoped.

---

## Rollup Behavior Requirements

- Case-level views **must not duplicate incident-scoped entities into Case tables**.
- Case-level lists are produced via **SqlCatalog rollups** (design contract; no inline SQL).

---

## Open Questions (Must Be Resolved Explicitly)

- Is `BusinessUnitUniqueId` mandatory at Case creation?
- Is `CaseNumber` unique per Tenant, per Business Unit, or per environment?
- Are Case types tenant-defined (CaseType lookup) and do they drive templates?

---

## Non-Goals (For This Entity Spec)

- No evidence schema details here
- No notification channel behavior here
- No OSINT behavior here
- No Chat Overlay behavior here (design lives under `docs/plan/Future/Obscura/`)
