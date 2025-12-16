# UX — Soft Delete Visibility Rules

## Status
**Authoritative (Cross-Cutting)**

---

## Purpose

CaseBunker uses soft deletes only.
UX must handle deleted items safely and predictably.

---

## UX Rules

- Deleted records must not appear in normal lists by default
- If a user navigates to a deleted record (deep link or stale navigation):
  - Show a “Deleted” state view
  - Restrict actions
  - Provide safe navigation back

---

## List Filters (Optional)

If “Include Deleted” is allowed:
- It must be explicit (toggle or filter)
- It must be permission-gated
- It must be remembered per user (optional; not assumed)

---

## Non-Goals

- Undelete workflows
- Retention purge behavior
