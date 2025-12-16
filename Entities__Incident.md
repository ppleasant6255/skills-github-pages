# Entity — Incident

## Status
**Authoritative (Core Domain)**

This document defines the **Incident** entity as the operational anchor within a Case.
Most operational entities attach to an Incident.

See also:
- `docs/plan/Entities/Case.md`
- `docs/plan/Architecture/Tenancy.md`
- `docs/plan/Architecture/BusinessUnits.md`
- `docs/plan/Architecture/AuditLogging.md`

---

## Purpose

An Incident represents a discrete event, allegation, or investigative unit within a Case.
Incidents are the primary anchor for operational data such as Evidence, People links, Notes, Tasks, Surveillance, and (later) OSINT.

---

## Ownership and Scope

### Tenant Scope (Required)
Incident is tenant-owned and must include:
- `TenantUniqueId` (required)

### Case Parent (Required)
Incident must include:
- `CaseUniqueId` (required)

### Business Unit Scope (Explicit, TBD)
Business Unit scoping must be explicit (silence is not permission).

**Current decision:** Not yet finalized.
- Include `BusinessUnitUniqueId` as **explicitly optional** until Business Unit scoping is finalized.
- If BU scoping is later required for Case, Incident must declare whether it:
  - Inherits BU from Case, or
  - Stores its own BU value (and must match Case)

This must be resolved explicitly later; no assumptions.

---

## Required Fields (Minimum Contract)

### Identity / Tenancy / Parent
- `UniqueId` (GUID, PK)
- `TenantUniqueId` (GUID, NOT NULL)
- `BusinessUnitUniqueId` (GUID, NULLABLE)
- `CaseUniqueId` (GUID, NOT NULL)

### Display / Search
- `IncidentNumber` (string, required) — human-friendly identifier
- `Title` (string, required)
- `Description` (string, nullable)

### Status / Time
- `StatusKey` (string, required)
- `OccurredUtc` (datetime, nullable; UTC) — when the incident occurred (if known)

### Ownership
- `OwnerUserUniqueId` (GUID, required)

### System Fields
- `CreatedUtc` (datetime, required; UTC)
- `UpdatedUtc` (datetime, required; UTC)
- `IsDeleted` (bit, required; soft-delete only)

---

## Relationships (Conceptual)

### Belongs To
- Case

### One-to-Many (Incident → Child)
- EvidenceItems (incident-scoped)
- IncidentNotes (future)
- IncidentTodos / Tasks (future)
- IncidentPersons (future; note: OSINT rules forbid Person usage in OSINT, but core domain may still use Person elsewhere)
- SurveillanceSchedules / Results (future)
- Notifications (rollup; additive)

### Rollups (Incident → Case)
- Case-level views aggregate Incidents into Case rollups via SqlCatalog queries.

---

## Business Rules

- An Incident cannot exist without a Case.
- Moving an Incident between Cases is **not assumed**; must be explicitly documented if allowed.
- Deletion is soft-delete only.
- Incident-scoped data must not be duplicated into Case tables.

---

## Audit Requirements

Must audit:
- Incident creation
- Incident updates
- Incident status changes
- Incident soft-delete
- Parent linkage changes (if ever allowed)

Audit must preserve Tenant scope and include Business Unit context when applicable.

---

## Open Questions (Must Be Resolved Explicitly)

- Is `IncidentNumber` unique per Case or per Tenant?
- Should Incident inherit BusinessUnit from Case (enforced) or store its own?
- Are Incidents allowed to be re-parented to a different Case?

---

## Non-Goals (For This Entity Spec)

- Evidence and chain-of-custody details (handled under `docs/plan/Evidence/`)
- Notifications delivery mechanics (handled under `docs/plan/Notifications/`)
- OSINT subsystem details (deferred)
- Chat Overlay UX (handled under `docs/plan/Future/Obscura/`)
