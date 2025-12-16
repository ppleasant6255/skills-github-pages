# Evidence — Access Rules

## Status
**Authoritative (Supporting)**

---

## Purpose

Defines high-level access rules for evidence without embedding RBAC logic or schemas.

---

## Core Principles

- Evidence access is restrictive by default
- Access is always permission-gated
- Access rules never bypass Tenant or Business Unit isolation

---

## Access Types

Conceptual access types include:
- View metadata
- View files
- Download files
- Add attachments
- Edit metadata
- Record custody events
- Archive / dispose

Exact permissions are defined elsewhere.

---

## Inheritance Rules

- Evidence access may inherit from Incident access
- Evidence access must never exceed Incident access
- Explicit evidence-level restrictions may further limit access

---

## Audit Requirements

- Evidence access (view/download) may be audited per policy
- Permission changes affecting evidence access must be audited

---

## Forbidden Behaviors

- Implicit access through unrelated roles
- Cross-incident evidence access
- Silent permission failures

---

## Non-Goals

- RBAC matrix
- UI permission management
