# System Boundaries & Explicit Non-Goals

## Status
**Authoritative (Hard Guardrail)**

---

## Purpose

This document defines what CaseBunker explicitly **will not do**.
These boundaries are non-negotiable and exist to prevent scope creep,
assumption injection, and unsafe automation.

If a future idea conflicts with this document, this document wins
unless explicitly amended.

---

## Core System Boundaries

CaseBunker is:

- A **case-centric investigation management system**
- A **recorded, auditable workspace**
- A **human-driven investigative tool**

CaseBunker is NOT an autonomous system.

---

## Explicit Non-Goals (Global)

CaseBunker does NOT:

- Perform investigations autonomously
- Make decisions on behalf of users
- Act as legal advice
- Guarantee correctness or completeness of data
- Replace investigator judgment
- Perform background actions without user initiation

---

## Data & Authority Boundaries

- CaseBunker is authoritative only for entities it explicitly defines
- No subsystem may become a system of record by implication
- No derived or inferred data is treated as authoritative

---

## Automation Boundaries

Automation is allowed only when:
- Explicitly designed
- Explicitly documented
- Explicitly user-initiated

Automation is NOT allowed to:
- Mutate core data silently
- Run continuously without visibility
- Bypass audit logging

---

## AI & Assistant Boundaries

AI-assisted features (including Chat Overlay / Obscura):

- Are advisory only
- Do not act without confirmation
- Do not bypass permissions
- Do not persist hidden state
- Do not fabricate or infer missing facts

---

## Notifications Boundaries

- Notifications are additive only
- Notification delivery failure never blocks workflows
- Notifications do not create or modify domain data

---

## OSINT Boundaries (V2+)

- OSINT is explicitly deferred
- OSINT does not create Evidence automatically
- OSINT does not ingest PII by default
- OSINT is not required for core workflows

---

## UX Boundaries

- UX reflects domain truth
- No hidden state
- No implied automation
- No workflow shortcuts that bypass rules

---

## Enforcement

If any future design, code, or documentation violates these boundaries:
- Stop
- Document the conflict
- Resolve explicitly before proceeding

---

## Summary

Boundaries are safety.
Non-goals are design decisions.
Nothing outside these bounds is allowed accidentally.
