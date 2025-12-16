# Architecture — Audit Logging

## Status
**Authoritative**

This document defines audit logging requirements for CaseBunker.
Audit is mandatory, cross-cutting, and non-optional.

---

## Purpose
Audit provides accountability, traceability, compliance support, and forensic reconstruction.
Audit is not analytics or telemetry.

---

## Audit as a First-Class System
- Append-only
- Immutable
- Separate from operational data
- Complete or incorrect

---

## Audit Storage Model

### Separate Audit Database
Audit records are stored in a separate database from operational data.
Operational systems may write audit events but must never mutate audit data.

---

## Required Audit Context
Each audit record includes at minimum:
- `AuditUniqueId` (GUID)
- `TimestampUtc` (UTC)
- `TenantUniqueId`
- `ActorType`
- `ActorUniqueId` (nullable for system)
- `ActionType`
- `TargetType`
- `TargetUniqueId` (nullable)
- `Outcome` (Success | Failure | Partial | Denied)
- `FailureReason` (nullable)
- `SourceSystem`

Optional (encouraged):
- `BusinessUnitUniqueId`
- Correlation/request identifiers

---

## Actions That MUST Be Audited

### Identity & Access
- Authentication attempts
- Authorization failures
- Role/permission changes

### Data Operations
- Entity create/update/soft-delete
- Bulk operations

### Administrative
- Tenant config changes
- Business Unit changes
- Module enable/disable
- Retention policy changes

### Notifications
- Emission
- Delivery attempts
- Failures
- Throttling/quota enforcement

### Evidence
- Evidence creation/access/transfer
- Chain-of-custody events

### Chat Overlay
- Invocation
- Data access
- User-confirmed actions
- Denied/restricted actions

### OSINT (When Implemented)
- Query execution
- Provider access
- Result storage
- Rate-limit enforcement

---

## Audit and Failure
Failed attempts must be audited. Silent failure is forbidden.

---

## Audit and Tenancy / Business Units
- Always include `TenantUniqueId`
- Include `BusinessUnitUniqueId` when BU-scoped
- Tenant-level actions must be explicitly marked

---

## Retention and Purging
- Retention is tenant-configurable within system bounds
- Purge actions must be audited (who/what/why/when)

---

## Access to Audit Data
- Restricted access
- Viewing/exporting audit records must be auditable

---

## Forbidden Patterns
- Audit in operational tables
- Best-effort or sampled audit
- Mutating audit records
- Silent suppression of audit failures

---

## Summary
Audit is mandatory, complete, immutable, and separate from operational data.
