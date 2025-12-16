# Notifications — Throttling

## Status
**Authoritative (Required)**

This document defines throttling and quota requirements for notifications.

---

## Purpose

Throttling prevents notification abuse, overload, and accidental denial of service.
It is mandatory for notifications.

---

## Throttling Levels (Minimum)

Throttling must exist at:
- Tenant level
- Channel level

Additional levels (e.g., user-level) may be added later.

---

## Quota Semantics

- Quotas are tenant-configurable within system-defined bounds
- Quotas may differ by channel
- Exceeding quotas must not block core workflows

---

## Behavior When Throttled

- Notification delivery attempts may be skipped or delayed
- Throttling actions must be auditable
- Throttling must never fail silently

---

## Forbidden Behaviors

- Unlimited notification emission
- Blocking workflows due to quota exhaustion
- Silent drops without audit records
