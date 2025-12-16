# UX — Permission and Access Feedback

## Status
**Authoritative (Cross-Cutting)**

---

## Purpose

When users lack access, the UX must be explicit and non-confusing.
No silent failures.

---

## UX Rules

- Permission denied must show:
  - A clear message
  - The action or resource that was denied
- Do not expose sensitive details (e.g., existence of hidden cases) beyond what authorization allows
- Avoid “Not Found” when the real issue is permissions unless policy requires it

---

## Non-Goals

- RBAC policy design (handled elsewhere)
