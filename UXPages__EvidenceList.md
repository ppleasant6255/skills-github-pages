# UX — Evidence List Page

## Status
**Authoritative (Skeleton)**

---

## Purpose

The Evidence List page presents a read-only, incident-scoped list of EvidenceItems.
It provides visibility and navigation without exposing custody or file mutation workflows.

This page **must not exist** unless the Evidence module is enabled.

See also:
- `docs/plan/Evidence/EvidenceModel.md`
- `docs/plan/Entities/Incident.md`
- `docs/plan/Architecture/ModulesAndFeatureFlags.md`

---

## Scope & Context

- Scope: **Incident**
- Context indicators must show:
  - Case identifier
  - Incident identifier
  - Tenant
  - Business Unit (if applicable)

No cross-incident visibility is allowed.

---

## Required Elements (List Columns)

Minimum visible fields:

- EvidenceNumber
- Title / Label
- Evidence Type
- Status
- Collected Date (if available)
- Owner / Custodian (display name)
- Integrity Indicator (if applicable)

Columns must be sortable where it makes sense.

---

## Core Actions

Allowed actions:

- Open Evidence (navigates to Evidence Detail page)
- Add Evidence (if permitted and module enabled)
- Filter / Search

Add Evidence:
- Must be explicit user action
- Must follow standard UI workflows
- Must not be performed through Chat Overlay alone

---

## Read-Only Guarantees

This page:
- Does NOT edit evidence metadata inline
- Does NOT upload or replace files
- Does NOT perform custody actions

All mutations occur elsewhere.

---

## Empty State

If no evidence exists:
- Display a clear empty state
- Offer “Add Evidence” if permitted
- No implied automation or suggestions

---

## Error States

- Permission denied → explicit message
- Module disabled → page must not be reachable
- Incident missing / deleted → safe navigation back

---

## Audit Considerations

- Viewing the Evidence List may be auditable if required by policy
- No custody or integrity claims are made by viewing alone

---

## Non-Goals

- Evidence file preview
- Chain-of-custody workflows
- Evidence detail editing
- Bulk operations
