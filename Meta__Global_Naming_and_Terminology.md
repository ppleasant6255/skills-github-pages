# Global Naming & Terminology

## Status
**Authoritative (Cross-Cutting)**

---

## Purpose

This document establishes **global naming, terminology, and vocabulary rules** for CaseBunker.
It exists to prevent:
- Accidental pluralization/singularization drift
- Inconsistent entity names
- AI- or human-invented synonyms
- Schema and UX mismatch

All planning, implementation, and documentation must conform.

---

## Canonical Entity Names (Locked)

The following names are **canonical** and must be used verbatim:

- Tenant
- BusinessUnit
- Case
- Incident
- Evidence
- EvidenceItem
- EvidenceFile
- Notification
- NotificationEvent
- NotificationSubscription
- NotificationDelivery
- Audit
- User
- Role
- Permission
- Module
- Chat Overlay (Obscura)

Do **not** invent alternates (e.g., “Investigation” instead of Case).

---

## Table Naming Rules (Hard Lock)

- Table names must match schema exactly
- No pluralization changes
- No singularization changes
- No aliases
- No abbreviations

If a table name is unknown:
- **Stop**
- **Document the question**
- Do not guess

---

## Identifier Naming Rules

### Primary Keys
- Always named: `UniqueId`
- Type: `UNIQUEIDENTIFIER`
- Generated via `newsequentialid()`

### Foreign Keys
- Pattern: `<EntityName>UniqueId`
- Example: `CaseUniqueId`, `IncidentUniqueId`

No exceptions.

---

## Tenant & Business Unit Fields

- Tenant-owned entities include: `TenantUniqueId`
- Business Unit scoped entities include: `BusinessUnitUniqueId`
- Nullable BU fields must be explicitly documented

---

## Status & Lookup Naming

- Status-like fields use `*Key` suffix
  - Examples: `StatusKey`, `PriorityKey`, `TypeKey`
- Keys are stable identifiers
- Labels are tenant-configurable display values

Do not hardcode labels.

---

## Time & Date Naming

- All timestamps are UTC
- Use `*Utc` suffix
  - Examples: `CreatedUtc`, `UpdatedUtc`, `OccurredUtc`

---

## Boolean Naming

- Use `Is*` prefix
  - Example: `IsDeleted`
- No negative booleans (`IsNotDeleted` is forbidden)

---

## Soft Delete Rules

- Soft delete only
- Use `IsDeleted`
- Never overload meaning
- Never reuse deleted records silently

---

## UX Terminology Rules

- UX labels should match canonical entity names
- Avoid synonyms unless explicitly documented as display-only
- Context must always be explicit (Case vs Incident)

---

## Audit Terminology

- “Audit” refers to immutable audit records only
- Do not use “audit” to mean logs, telemetry, or analytics

---

## Prohibited Behaviors

- Guessing names
- Renaming entities for readability
- Introducing new terminology without documentation
- “Fixing” names ad hoc

---

## Summary

Consistency is a feature.
Names are contracts.
When in doubt: stop and document.
