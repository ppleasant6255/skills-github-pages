# Pro Execution Contract

## Status
**Authoritative (Binding on Pro Sessions)**

---

## Purpose

This document defines the **execution contract** for ChatGPT Pro when working on CaseBunker.
It converts planning into a constrained execution environment.

This contract is binding for all Pro-assisted work.

---

## Absolute Rules (Non-Negotiable)

When operating under this contract, Pro MUST:

- Follow all documents in `docs/plan/` as authoritative
- Treat locked rules as immutable
- Ask when information is missing
- Produce incremental ZIP patches only
- Provide SHA-256 hashes for every ZIP
- Respect execution order and validation criteria

---

## Prohibited Behaviors

Pro MUST NOT:

- Guess table names, columns, or entities
- Invent schemas, defaults, or workflows
- Rename entities “for clarity”
- Skip phases or reorder execution
- Modify UX navigation without approval
- Introduce background execution assumptions
- Create Evidence, Notifications, or OSINT implicitly
- Treat AI output as authoritative data

---

## Required Behaviors

Pro MUST:

- Cite relevant plan documents when producing work
- Keep changes minimal and scoped
- Preserve build-green state
- Use XAML + code-behind for MAUI
- Route all reads through SqlCatalog
- Route all writes through API using ResilientApiCaller.CallAsync
- Use soft deletes only
- Maintain Tenant isolation everywhere

---

## Output Requirements

Every Pro output that modifies the solution MUST include:

1. ZIP archive containing:
   - Correct folder paths
   - Only intended changes
2. Clear file tree listing
3. SHA-256 checksum
4. Extraction instructions

No inline code dumps for multi-file changes.

---

## Interaction Rules

If Pro encounters:
- Missing schema detail
- Ambiguous rule
- Conflicting documents

Pro MUST:
- Stop
- Ask a clarifying question
- Not proceed until resolved

---

## Failure Handling

If Pro violates this contract:
- The output is considered invalid
- Work must be discarded
- The contract must be reasserted

---

## Summary

This contract turns Pro from a creative assistant into a **deterministic execution engine**.
Adherence is mandatory.
