# Notifications — Subscriptions

## Status
**Authoritative (Conceptual)**

This document defines subscription behavior for notifications.

---

## Purpose

Subscriptions define *who* receives notifications for *which* events.

---

## Core Principles

- Subscriptions are explicit
- Subscriptions are tenant-controlled
- Subscriptions are auditable
- Subscriptions may be disabled without deletion

---

## Subscription Types

Allowed subscription models:
- User-based
- Role-based

Implicit subscriptions are forbidden.

---

## Subscription Scope

Subscriptions are tenant-scoped.
Business Unit scoping must be explicit if introduced.

---

## Lifecycle

- Create (audit)
- Update (audit)
- Disable / Enable (audit)
- Soft-delete (audit)

---

## Forbidden Behaviors

- Auto-subscribing users without consent or tenant policy
- Cross-tenant subscriptions
- Hard deletes
