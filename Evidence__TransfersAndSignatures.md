# Evidence — Transfers & Signatures

## Status
**Authoritative (Supporting)**

---

## Purpose

This document defines how evidence transfers and acknowledgements are represented conceptually.
It completes the Evidence planning set without introducing implementation details.

---

## Core Principles

- Transfers are explicit events
- Transfers are append-only
- Transfers are auditable
- Signatures are acknowledgements, not magic proof

---

## Transfer Events

A transfer represents a change in custody responsibility.

Conceptual data captured:
- Evidence reference
- From custodian (nullable for initial collection)
- To custodian
- Timestamp (UTC)
- Reason / notes
- Optional signature/acknowledgement reference

Transfers must never be inferred from metadata changes.

---

## Signatures

Signatures represent acknowledgement of receipt or responsibility.

Rules:
- Signatures are optional unless explicitly required by policy
- Absence of a signature does not invalidate custody history
- Signature capture mechanics are implementation details and out of scope here

---

## Digital vs Physical Evidence

- Physical evidence may require explicit transfer acknowledgements
- Digital evidence may rely on access controls and audit logs
- Both use the same conceptual transfer model

---

## Audit Requirements

- Every transfer event must be audited
- Signature capture (if any) must be audited
- Failed or cancelled transfers must be auditable

---

## Non-Goals

- UI signature capture design
- Cryptographic signature formats
- Legal admissibility guarantees
