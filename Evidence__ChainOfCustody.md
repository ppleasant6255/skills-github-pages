# Evidence — Chain of Custody

## Status
**Authoritative (Foundation)**

This document defines Chain of Custody rules for CaseBunker Evidence.
Chain of custody is critical to defensible evidence handling.

See also:
- `docs/plan/Evidence/EvidenceModel.md`
- `docs/plan/Architecture/AuditLogging.md`

---

## Purpose

Chain of custody records the controlled possession and transfer history of evidence.
It exists to support:
- Integrity
- Accountability
- Legal defensibility

Chain of custody is **not optional** for physical evidence.
For digital evidence, custody is represented by access controls and immutable storage plus audit trails; custody-style transfers may still be required depending on workflow (not assumed).

---

## Core Principles

1. **Append-Only**
   - Custody history must be append-only (no edits, no deletions).

2. **Explicit Transfer Events**
   - Custody changes must be recorded as explicit events.

3. **Auditable**
   - Every custody event must generate audit records.

4. **No Implicit Custody**
   - Custody is never inferred from metadata alone.

---

## Custody Actors

Custody may be held by:
- A User (investigator, custodian)
- A Facility / Location (evidence room, safe)
- A Container (sealed bag ID, locker ID)

The exact actor set must be documented explicitly when implemented.
This document establishes the requirement that custody is attributable and auditable.

---

## Custody Event Types (Conceptual)

Minimum event types:
- Collected (initial acquisition)
- Transferred (handoff between custodians)
- CheckedIn (into a facility/container)
- CheckedOut (out of a facility/container)
- Sealed (tamper seal applied)
- Unsealed (tamper seal broken)
- Disposed (final disposition, if allowed)

Do not assume additional types without explicit documentation.

---

## Transfer Requirements

A custody transfer event must record conceptually:
- From custodian (may be null for initial collection)
- To custodian
- Timestamp (UTC)
- Reason / notes (optional but recommended)
- Witness/approval (not assumed; may be required later)
- Any seal/container identifiers (if used)

Transfers must not block core workflows, but they **must** be auditable and complete for evidence that requires custody tracking.

---

## Digital Evidence Handling

Digital evidence integrity relies on:
- Immutable EvidenceFile storage
- Hash/integrity metadata
- Audited access and downloads
- Append-only custody/event log when custody semantics are used

Digital files must never be silently replaced.

---

## Relationship to Notifications and OSINT

- Notifications may be emitted for custody events but must be additive and non-blocking.
- OSINT results are not evidence by default and therefore do not receive chain-of-custody treatment unless explicitly converted into Evidence by user action.

---

## Forbidden Behaviors

- Editing or deleting custody history
- “Auto-custody” changes without explicit event creation
- Claiming custody for non-evidence data
- Treating access logs alone as chain of custody for physical evidence

---

## Open Questions (Must Be Resolved Explicitly)

- Do we require signatures for transfers in v1?
- Are facility/container custodians represented as entities or free text?
- Which custody events require dual approval or witnesses (if any)?

---

## Non-Goals (For This Document)

- UI design for custody workflows
- Signature capture mechanics
- Database table definitions
