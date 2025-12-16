# Chat Overlay — Overview (Obscura)

## Status
**Authoritative (Design-Complete, Build-Deferred)**

Chat Overlay (codename **Obscura**) is a first-class UX surface in CaseBunker.
This design must be complete before upgrading to Pro.

---

## Purpose

Chat Overlay provides an investigator-facing assistant interface that:
- Surfaces existing CaseBunker data
- Assists with navigation, summarization, and explanation
- Never acts as a system of record
- Never mutates data without explicit user confirmation

Obscura is an **overlay**, not a workflow replacement.

---

## Non-Goals (Hard Locks)

- Obscura does NOT create Cases, Incidents, Evidence, or Notifications on its own
- Obscura does NOT bypass permissions, tenancy, or audit
- Obscura does NOT perform background actions
- Obscura does NOT guarantee correctness or completeness

---

## Invocation Model

Obscura may be invoked:
- From Case context
- From Incident context
- From global navigation (read-only context until scoped)

Invocation must always have:
- Explicit Tenant context
- Explicit user identity
- Explicit scope (Case / Incident / Global)

---

## Relationship to Modules

Chat Overlay is a **module**.
- Disabled module = no invocation, no execution
- Design completeness does not imply enablement

---

## Relationship to Other Subsystems

- Evidence: read-only summarization unless user explicitly acts
- Notifications: may explain notifications; does not emit them
- OSINT: no direct execution in v1
- Audit: all interactions are auditable

---

## Summary

Obscura is a controlled assistant overlay that enhances investigator efficiency
without becoming authoritative or autonomous.
