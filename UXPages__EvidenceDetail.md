# UX — Evidence Detail Page

## Status
**Authoritative (Skeleton)**

---

## Purpose

The Evidence Detail page presents a single EvidenceItem and its associated EvidenceFiles and custody history.
The initial UX is conservative:
- Read-only by default
- Explicit, intentional entry points for mutation
- No silent file replacement
- No implied chain-of-custody claims beyond recorded events

This page must not exist unless the Evidence module is enabled.

See also:
- `docs/plan/Evidence/EvidenceModel.md`
- `docs/plan/Evidence/ChainOfCustody.md`
- `docs/plan/UX/Pages/EvidenceList.md`
- `docs/plan/Architecture/AuditLogging.md`

---

## Scope & Context

- Scope: **Incident**
- Must display context:
  - Case identifier
  - Incident identifier
  - EvidenceNumber + Title
  - Tenant
  - Business Unit (if applicable)

Evidence must never be shown cross-incident.

---

## Required Sections

### 1) Header
- EvidenceNumber
- Title / Label
- Evidence type
- Status
- Owner / Custodian (display name)
- Created / Updated timestamps (UTC display formatting as UX convention)

### 2) Description / Notes (Read-Only Display)
- Evidence description
- Any tags/classification if present (future)

### 3) Attachments (EvidenceFiles)
- List of associated files with:
  - Filename
  - Content type
  - Size
  - Hash/integrity indicator (if available)
  - Created timestamp
- Allowed actions (initial):
  - View / Download (permission-gated)
  - Open file viewer (if implemented)
- Forbidden actions:
  - Replace file
  - Edit file metadata inline

### 4) Custody Summary (Read-Only)
- Current custodian (if available)
- Most recent custody event
- Link to full custody history section

### 5) Custody History (Read-Only List)
- Append-only event list (chronological)
- Event type
- From → To (when applicable)
- Timestamp
- Notes (if any)

### 6) Audit / Activity (Optional Read-Only)
- If permitted, show recent activity summary (no raw audit dump)
- Audit access rules apply

---

## Core Actions (Explicit Entry Points)

Actions must be explicit buttons or menu items, permission-gated:

- Edit Evidence Metadata (opens dedicated edit flow; no inline editing)
- Add Attachment (dedicated flow)
- Record Custody Event (dedicated flow)
- Archive / Dispose (if allowed; dedicated flow)

All actions must:
- Require explicit user intent
- Be auditable
- Never block core workflows outside Evidence itself

---

## Error & Edge States

- Evidence not found → safe navigation back to Evidence List
- Permission denied → explicit message
- Module disabled → page must not be reachable
- Evidence soft-deleted → show “Deleted” state and restrict actions

---

## Non-Goals (For This Page Spec)

- Full custody signature capture UX
- Bulk evidence operations
- Automated evidence generation
- OSINT conversion workflows
