# Evidence — Evidence Model

## Status
**Authoritative (Foundation)**

This document defines the foundational Evidence model for CaseBunker.
Evidence is a first-class subsystem for corporate investigations and must be defensible.

See also:
- `docs/plan/Entities/Incident.md`
- `docs/plan/Architecture/Tenancy.md`
- `docs/plan/Architecture/BusinessUnits.md`
- `docs/plan/Architecture/AuditLogging.md`

---

## Purpose

Evidence captures and organizes material relevant to an investigation.
Evidence may be digital or physical and must support defensible handling, access, and auditing.

Evidence must never be created automatically by other subsystems.
Evidence may be associated with data produced by other subsystems (e.g., OSINT), but OSINT output is **not evidence by default**.

---

## Scope and Ownership

### Incident Scope (Hard Lock)
Evidence is **incident-scoped**.

- Evidence items attach to an Incident.
- Case-level evidence views are rollups via SqlCatalog.

### Tenant Scope (Required)
All evidence entities must include:
- `TenantUniqueId`

### Business Unit Scope (Explicit, TBD)
Business Unit behavior must be explicit.
Until finalized:
- Include `BusinessUnitUniqueId` as optional only where needed.
- Do not assume BU inheritance rules.

---

## Evidence Concepts

### EvidenceItem (Logical Evidence)
A logical evidence record describing “what this is” (title, description, type, status).
EvidenceItem is not a file itself.

### EvidenceFile (Digital Artifact)
Represents a digital object linked to an EvidenceItem.
Examples: uploaded PDF, image, audio, exported archive.

EvidenceFile requires:
- size
- content type
- storage reference
- integrity metadata (hash)

### Physical Evidence
Physical evidence is represented by EvidenceItem metadata and custody records.
Physical evidence may also have associated EvidenceFiles (photos, scans).

---

## Evidence Identity and Numbering

Evidence needs a human-friendly identifier (EvidenceNumber) in addition to `UniqueId`.

The exact uniqueness scope is **not assumed** and must be resolved explicitly:
- Per Incident
- Per Case
- Per Tenant

---

## Evidence Mutability Rules

- EvidenceItem metadata may be updated (audited).
- EvidenceFiles are immutable once stored.
  - A “replacement” is a new EvidenceFile linked to the EvidenceItem.
- Chain-of-custody is append-only.

---

## Evidence States (Conceptual)

Evidence should support at least:
- Draft (initial capture)
- Collected (acknowledged)
- Archived (no longer active)
- Disposed (if allowed; must be auditable)

Do not assume additional states without explicit documentation.

---

## Required Auditing (Non-Negotiable)

Evidence operations must be auditable (see `Architecture/AuditLogging.md`):

- EvidenceItem creation/update/soft-delete
- EvidenceFile creation (upload, import)
- Evidence access (view/download)
- Custody transfer events
- Disposition/archival actions
- Permission changes affecting evidence visibility

Audit records must include Tenant and BU context when applicable.

---

## Forbidden Behaviors

- Hard deletes of evidence or files
- Silent file replacement
- Evidence creation by automated subsystems without explicit user action
- Treating OSINT results as evidence by default
- Chain-of-custody claims for non-evidence data

---

## Rollup Requirements

- Case-level Evidence List is a rollup:
  - EvidenceItem is incident-scoped
  - Case evidence is derived via Incident relationships
- Rollups are performed via SqlCatalog reads (no inline SQL).

---

## Open Questions (Must Be Resolved Explicitly)

- EvidenceNumber uniqueness scope (Incident/Case/Tenant)
- Should EvidenceItem support tagging and classification in v1?
- Do we require mandatory custody records for all evidence items, or only physical?
- What minimum integrity metadata is required for EvidenceFile (hash type)?

---

## Non-Goals (For This Document)

- Transfer signatures and attestation (separate document)
- Evidence access rules matrix (separate document)
- Storage provider implementation details
