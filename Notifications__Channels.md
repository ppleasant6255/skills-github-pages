# Notifications — Channels

## Status
**Authoritative (Conceptual)**

This document defines notification channels at a conceptual level.

---

## Purpose

Channels define *how* notifications are delivered.
They do not define *when* or *whether* a notification is emitted.

---

## Core Principles

- Channels are configurable per tenant
- Channels are additive
- Channel failure must not block workflows
- Channel behavior is auditable

---

## Supported Channels (Initial)

- In-App (required)
- Email (optional)

Additional channels may be added later and must follow the same rules.

---

## Channel Configuration

Channel configuration is tenant-controlled and may include:
- Enable/disable per channel
- Channel-specific settings (conceptual)

Configuration changes must be audited.

---

## Delivery Semantics

- Delivery is best-effort
- Retries may occur but are not guaranteed
- Failures are recorded and auditable

No channel may claim guaranteed delivery.

---

## Forbidden Behaviors

- Synchronous delivery in core workflows
- Channel logic embedded in core domain code
- Silent channel failure
