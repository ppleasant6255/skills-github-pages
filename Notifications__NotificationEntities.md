# Notifications — Notification Entities

## Status
**Authoritative (Additive Subsystem)**

This document defines notification-related entities for CaseBunker.
Notifications are **additive**, **non-blocking**, and **event-driven**.

See also:
- `docs/plan/Architecture/AuditLogging.md`
- `docs/plan/Architecture/Tenancy.md`
- `docs/plan/Architecture/BusinessUnits.md`
- `docs/plan/Architecture/ModulesAndFeatureFlags.md`

---

## Core Principles

- Notifications are never required for core workflows
- Notification failure must never block business operations
- Notifications are not a system of record
- Delivery is best-effort, not guaranteed
- All notification activity is auditable

---

## Scope and Ownership

### Tenant Scope (Required)
All notification entities are tenant-owned and must include:
- `TenantUniqueId`

### Business Unit Scope (Explicit)
Business Unit behavior must be explicit.

**Current decision:** Notifications are **tenant-scoped by default**.
- Include `BusinessUnitUniqueId` only if/when a notification is explicitly BU-scoped.
- Silence is not permission.

---

## Core Notification Concepts

### NotificationEvent
Represents an event emitted by the system that *may* result in notifications.

Characteristics:
- Emitted asynchronously
- Non-blocking
- Audited at emission

Examples:
- Case created
- Incident status changed
- Evidence collected
- Custody transfer recorded

---

### NotificationSubscription
Represents an explicit opt-in by a user or role to receive notifications for certain events.

Characteristics:
- Explicit and tenant-controlled
- May be user-specific or role-based
- Audited on create/update/delete

---

### NotificationDelivery
Represents a single delivery attempt for a notification.

Characteristics:
- Channel-specific (email, in-app, etc.)
- Records success, failure, or retry
- Audited for each attempt

---

### NotificationChannel
Represents a configured delivery mechanism.

Examples:
- In-app
- Email
- SMS (future)
- Webhook (future)

Channels are configuration, not logic.

---

## Required Fields (Conceptual)

> This section defines required concepts, not schema.

### NotificationEvent
- UniqueId
- TenantUniqueId
- EventTypeKey
- SourceEntityType
- SourceEntityUniqueId
- CreatedUtc

### NotificationSubscription
- UniqueId
- TenantUniqueId
- Subscriber (User or Role reference)
- EventTypeKey
- IsEnabled
- CreatedUtc
- IsDeleted (soft delete)

### NotificationDelivery
- UniqueId
- TenantUniqueId
- NotificationEventUniqueId
- ChannelKey
- AttemptUtc
- Outcome
- FailureReason (nullable)

---

## Audit Requirements

Must audit:
- Event emission
- Subscription changes
- Delivery attempts
- Delivery failures
- Throttling/quota enforcement

Audit records must include Tenant context and BU context if applicable.

---

## Forbidden Behaviors

- Blocking workflows on notification success
- Treating notifications as guaranteed delivery
- Implicit subscriptions
- Cross-tenant delivery
- Writing notification state into core entity tables

---

## Open Questions (Must Be Resolved Explicitly)

- Are subscriptions allowed at Role level only, or User + Role?
- Should NotificationEvent payload snapshots be stored or referenced?
- Do some events require mandatory notifications (conceptually)? If yes, how do we express “mandatory emission but non-mandatory delivery”?

---

## Non-Goals

- Channel implementation details
- UI for managing subscriptions
- External broker or queue assumptions
