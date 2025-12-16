# Chat Overlay — Boundaries & Guardrails

## Status
**Authoritative**

This document defines hard boundaries for Obscura.

---

## Permission Boundaries

Obscura inherits permissions from the invoking user.
It cannot elevate access or bypass authorization.

---

## Data Boundaries

- Read-only by default
- No cross-tenant access
- No cross-case leakage
- No background data fetching outside explicit scope

---

## Safety Boundaries

- No autonomous execution
- No hidden side effects
- No silent failures
- No implicit assumptions

---

## Audit Boundaries

The following must be audited:
- Invocation
- Data access
- Denied requests
- User-confirmed actions (delegated to standard workflows)

---

## Forbidden Behaviors

- Acting as a system of record
- Auto-filing evidence
- Auto-sending notifications
- Persisting private conversation state
