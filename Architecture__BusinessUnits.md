# Architecture — Business Units

## Status
**Authoritative**

This document defines Business Units as organizational segments within a Tenant.
All Business Unit behavior is subordinate to Tenancy.

See also: `Architecture/Tenancy.md`

---

## Purpose
Business Units support large organizations with multiple groups operating under one tenant by providing scoped administration and visibility (where explicitly enabled).

---

## Core Model
A Business Unit belongs to exactly one Tenant.

Minimum identity:
- `BusinessUnitUniqueId` (`UNIQUEIDENTIFIER`)
- `TenantUniqueId` (`UNIQUEIDENTIFIER`)

---

## Administration Roles

### Tenant Admin
Tenant Admin can:
- Create/manage Business Units
- Configure tenant-wide modules/defaults
- Define rules as **Strict** or **Additive**

UI label requirement:
- Flyout/menu must display: **`<Business Unit Name> Admin Settings`**

### Business Unit Admin
Business Unit Admin manages a single unit:
- Manages unit membership and permitted settings
- Extends additive policies where allowed

---

## Policy Semantics (Strict vs Additive)

### Strict
- Defined at Tenant level
- Applies to every Business Unit
- Cannot be weakened or overridden by a Business Unit

### Additive
- Tenant defines baseline and allowed extension surface
- Business Units may extend within tenant-approved bounds
- Business Units may not weaken tenant baselines

---

## Scoping Rules (Critical)

### Explicitness Rule
**Business Unit scoping must be explicit in documentation.**
Silence is **not permission**.

### Allowed Scoping Models
Each entity/module must declare one model:

1. **Tenant-Only Scope**
   - Includes `TenantUniqueId`
   - No `BusinessUnitUniqueId`

2. **Business Unit Scoped**
   - Includes `TenantUniqueId` + `BusinessUnitUniqueId`

3. **Hybrid Scope**
   - `TenantUniqueId` + nullable `BusinessUnitUniqueId`
   - Requires explicit rules for null vs set behavior

No other scoping models are allowed without explicit documentation.

---

## Membership & Active Unit Context
Users may belong to multiple Business Units; an explicit active unit context is required when it matters (case creation, incident creation, evidence operations, admin settings).

---

## Modules and Business Units
Modules are tenant-controlled.
Business Unit toggles exist only if explicitly documented as additive, and may never re-enable a tenant-disabled module.

---

## Audit & Business Units
If an action is BU-scoped, audit must capture `BusinessUnitUniqueId`.
If tenant-level, it must be explicitly marked as tenant-scoped.

---

## Open Questions (Must Be Resolved Later)
- Is `BusinessUnitUniqueId` mandatory on Case creation?
- Do Incidents inherit BU scope or store their own?
- Are Notifications BU-scoped or tenant-scoped by default?
- Are Evidence operations BU-scoped by default?

---

## Summary
- Business Units segment within a Tenant
- Tenant Admin sets strict/additive rules
- BU scoping must be explicit; silence is conflict
- Audit preserves BU context where applicable
