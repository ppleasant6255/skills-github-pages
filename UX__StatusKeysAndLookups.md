# UX — Status Keys & Lookups

## Status
**Authoritative (Cross-Cutting)**

---

## Purpose

This document defines how status-like fields are represented in UX without forcing premature schema decisions.

Many entities reference:
- Status
- Priority
- Type
- Classification

These are represented in docs as `*Key` values (e.g., `StatusKey`) to preserve tenant configurability.

---

## UX Rules

- UX displays human-friendly labels resolved from tenant-configured lookups
- Keys are stable identifiers; labels are display values
- Do not hardcode labels in UX designs unless explicitly marked as defaults

---

## Required Behavior

- If a key cannot be resolved, display:
  - The raw key (clearly marked), or
  - “Unknown” with the key visible (never hidden)

---

## Non-Goals

- Database schema for lookups
- Admin UI for managing lookups
