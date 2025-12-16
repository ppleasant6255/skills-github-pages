# Architecture — Tenancy

## Status
**Authoritative**

This document defines the tenancy model for CaseBunker.
All other architectural, data, and UX decisions must conform to this model.

---

## Purpose

CaseBunker is a **multi-tenant corporate investigations platform**.
Tenancy defines the **hard isolation boundary** for data, configuration, audit, and execution.

---

## Core Tenancy Model

### Tenant
A **Tenant** represents a single customer organization.

A Tenant is the **highest isolation boundary** in the system.

All tenant-owned data:
- Is logically isolated from other tenants
- Must never be visible across tenants
- Must never be processed across tenants

### Tenant Identity
Every tenant is identified by:
- `TenantUniqueId` (`UNIQUEIDENTIFIER`)
- Globally unique
- Immutable

All tenant-owned entities **must include `TenantUniqueId`** unless explicitly documented otherwise.

---

## Tenant Isolation Rules (Hard Locks)

1. **No Cross-Tenant Data Access**
   - No reads, writes, aggregation, analytics, or background processing across tenants

2. **No Shared Tenant State**
   - No global caches containing tenant data
   - No shared mutable configuration across tenants

3. **No Cross-Tenant Identifiers**
   - Entity identifiers must never be resolved without a Tenant filter

4. **No Silent Tenant Context**
   - Tenant context must be explicit; implicit or inferred context is forbidden

---

## Tenant Scope in Data Model

### Required on All Tenant-Owned Tables
Unless explicitly exempted, **every table** must include:
- `TenantUniqueId UNIQUEIDENTIFIER NOT NULL`
- Indexed
- Used in **every read filter**
- Used in **every write constraint**

### Explicit Exemptions Only
If an entity does **not** include `TenantUniqueId`, it must be:
- Explicitly documented
- Non-tenant-owned
- Read-only
- Immutable

Silence is **not** exemption.

---

## Tenant Scope in Application Layers

### API Layer
- Every request resolves and validates Tenant context before operations
- Tenant context must not be overridden by client input

### SqlCatalog Layer
- Every query **must include Tenant filtering**
- Tenant filtering must be explicit

### Background & Deferred Work
- Work executes **within a single Tenant**
- Tenant context must be persisted with the work item

---

## Tenant Administration
Tenant-level configuration applies to all Business Units unless overridden where allowed:
- Module enablement
- Retention policies
- Notification defaults
- Audit policies

Tenant configuration:
- Is authoritative
- Cannot be weakened by Business Units
- Can only be extended additively where explicitly allowed

---

## Relationship to Business Units
- Tenant = **hard isolation boundary**
- Business Unit = **segmentation within a tenant**

Business Units operate only after Tenant scope is established.
Business Unit behavior is defined in `Architecture/BusinessUnits.md`.

---

## Audit & Tenancy
Audit records:
- Must include `TenantUniqueId`
- Must never mix tenants
- Must respect Tenant retention rules

---

## Forbidden Patterns
- Global queries without Tenant filters
- Shared queues across tenants
- Cross-tenant batch jobs
- Tenant inference from identifiers
- “Admin” features that bypass Tenant context
- Debug/backdoor modes that leak tenant data

---

## Enforcement
Tenancy violations are critical defects and are not acceptable in alpha or debugging.

---

## Summary
- Tenant is the primary security boundary
- Tenant context is explicit and mandatory
- All data, execution, and audit respect Tenant isolation
