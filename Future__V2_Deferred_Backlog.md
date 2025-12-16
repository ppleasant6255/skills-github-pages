# V2 / Deferred Backlog

## Status
**Non-Authoritative (Deferred Planning Only)**

---

## Purpose

This document captures ideas, subsystems, and enhancements that are
**explicitly deferred beyond V1**.

Nothing in this document is required for:
- Initial launch
- Core workflows
- Legal defensibility
- Pro upgrade eligibility

This exists to prevent future scope bleed.

---

## Deferred Subsystems

### OSINT (Open Source Intelligence)

Status: **Deferred to V2**

Constraints (Locked):
- OSINT is additive only
- OSINT never auto-creates Evidence
- OSINT never ingests PII by default
- OSINT never bypasses audit or permissions
- OSINT results are raw and retained per user lifecycle

Rationale:
- High legal sensitivity
- Provider volatility
- Requires separate validation phase

---

### Advanced Automation

Examples (Non-Binding):
- Task suggestions
- Workflow reminders
- Bulk metadata helpers

Constraints:
- Must be user-initiated
- Must be auditable
- Must never be autonomous

---

### Analytics & Reporting

Examples:
- Case duration metrics
- Incident frequency summaries
- Evidence volume tracking

Constraints:
- Read-only
- Aggregate only
- No behavioral scoring

---

### External Integrations

Examples:
- Secure export
- Partner systems
- Law firm tooling

Constraints:
- Explicit opt-in
- Tenant-controlled
- Audited

---

## Explicitly Out of Scope (Until Revisited)

- Predictive analytics
- Risk scoring
- Surveillance automation
- Facial recognition
- Background monitoring

---

## Re-Entry Rules

A deferred item may only move into V1+ planning if:
1. Explicitly proposed
2. Reviewed against System_Boundaries_and_NonGoals.md
3. Approved intentionally

---

## Summary

Deferred does not mean forgotten.
Deferred means **not allowed to leak**.
