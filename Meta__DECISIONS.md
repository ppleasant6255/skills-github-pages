# CaseBunker Planning Decisions — Consolidated Record

> **Purpose**
>
> This document is the authoritative consolidation of decisions explicitly made in this thread.
> It exists to preserve intent and guardrails after document overwrites and thread-splitting issues.
> This is not a full plan and not reconstructed history.

---

## 1. Governance & Truth Model

- docs/plan is the only authoritative source for implementation.
- Chat threads are advisory or validation-only.
- Only the ZIP-capable planning thread may read and generate ZIPs.
- Threads must never claim access to ZIPs or repos they cannot read.

---

## 2. Thread Capability Rules

- Threads cannot read ZIPs, repos, or files from other threads.
- If a document is not pasted in the thread, it is not visible.
- Correct response when lacking access: “Not verifiable from current documentation.”

---

## 3. Folder-to-Thread Authority Mapping

ZIP-Capable Planning Thread owns:
- docs/plan/Architecture
- docs/plan/Schema
- docs/plan/Future (including Obscura)
- docs/plan/ProExecution

Architecture Thread:
- Architecture/SystemOverview, Tenancy, BusinessUnits, RuleCompliance, AuditLogging, Modules

Entity & Schema Thread:
- Entities/*.md
- Schema drafts and maps

UX & MAUI Thread:
- UX principles, branding, naming
- Case and Incident pages first
- Evidence UX only after Case/Incident UX

Notifications Thread:
- NotificationEntities, Channels, Throttling, Subscriptions

Evidence Thread:
- EvidenceModel, ChainOfCustody, Transfers, AccessRules

OSINT Thread:
- Providers, Credentials, RateLimiting, Correlation, OSINT_Entity_Map

Future / Obscura Thread:
- Future/Obscura/*
- AI Reports, PII Modes

---

## 4. Architecture Decisions

- Multi-tenant system with Business Units.
- Rules can be strict (tenant) or additive (BU).
- Module enablement is tenant-controlled.
- Audit logging is mandatory and stored in a separate database.

---

## 5. Global Data Rules

- GUID UniqueId primary keys everywhere.
- TenantUniqueId on all tenant-owned entities.
- Soft deletes only.
- No inline SQL assumptions.
- No schema guessing.

---

## 6. Core Model Decisions

- Case is the top-level container.
- Incident is the operational anchor.
- Most entities are incident-scoped.
- Case-level views are rollups, not duplicated tables.

---

## 7. Evidence Rules

- Evidence is incident-scoped.
- Evidence is never auto-created.
- Chain of custody is explicit and auditable.
- OSINT output is not evidence by default.

---

## 8. Notifications Rules

- Notifications are additive only.
- Failures must never block workflows.
- Notifications are event-driven, not authoritative.
- Delivery is not guaranteed.
- Throttling and quotas are required.
- Subscriptions are explicit and tenant-controlled.
- All notification lifecycle events must be audited.

---

## 9. OSINT Rules (Locked)

- OSINT is additive only.
- No OSINT profiles.
- No Person entity usage.
- No PII in OSINT queries.
- City/State free-text locations only.
- Raw OSINT results always stored.
- Retention tied to requesting user active status.
- OSINT never auto-creates Evidence.
- OSINT never acts as system of record.

---

## 10. UX & MAUI Ordering

- Infrastructure first.
- Case List → Case Detail first.
- Incident UX follows Case UX.
- Evidence List before Evidence Detail.
- XAML + code-behind only.
- No navigation changes without approval.
- Page lockdown concept exists.

---

## 11. Obscura (Deferred)

- Obscura is Phase 6+.
- Lives under docs/plan/Future/Obscura.
- No Obscura work until core Case, Incident, and Evidence UX are complete.
- Obscura must not bypass RBAC, tenancy, BU scoping, or audit logging.

---

## 12. Validation Protocol

- Cross-domain validation happens only in ZIP-capable thread.
- Output must list Alignments, Conflicts, Violations, Required Changes, Not Verifiable.
- No redesign during validation.
- Missing documentation must be stated explicitly.

---

## 13. Final Principle

Accuracy over speed.
Truthfulness over helpfulness.
Silence over invention.

If something cannot be verified from documentation, that is the answer.
