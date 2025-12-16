# UX — Order & Principles

## Status
**Authoritative**

This document defines UX sequencing and principles for CaseBunker.
UX must follow domain order and must not introduce premature complexity.

---

## Core UX Ordering (Hard Lock)

Pages must be designed and implemented in this order:

1. Case List
2. Case Detail
3. Incident List
4. Incident Detail
5. Evidence List
6. Evidence Detail
7. Supporting entities

No downstream UX may be created before upstream pages are complete.

---

## Core Principles

- Clarity over density
- Explicit context at all times
- No hidden state
- No magical automation
- UX reflects domain truth

---

## Context Visibility

The UI must always make clear:
- Active Tenant
- Active Business Unit (when applicable)
- Active Case / Incident

---

## Navigation Rules

- No navigation changes without explicit approval
- Modules control visibility
- Disabled modules do not appear

---

## Summary

UX is subordinate to domain correctness and auditability.
