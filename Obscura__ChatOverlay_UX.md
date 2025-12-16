# Chat Overlay — UX

## Status
**Authoritative (Design)**

This document defines the user experience of Obscura.
The UX is intentionally conservative and predictable.

---

## Entry Points

- Floating overlay button (context-aware)
- Context menu action (Case / Incident)
- Keyboard shortcut (optional; explicit enablement)

---

## Visual Model

- Overlay panel (non-modal)
- Does not block underlying workflow
- Dismissible at any time
- Persistent across navigation within same context

---

## Conversation Model

- Stateless by default
- Context is explicit and visible (Case / Incident identifiers)
- No hidden memory across sessions unless explicitly designed later

---

## Response Types

Obscura may provide:
- Summaries (Case, Incident, Evidence lists)
- Explanations (“What is this?”, “Why is this here?”)
- Navigation shortcuts
- Draft suggestions (never auto-applied)

---

## Explicit User Actions

Any action that would:
- Create data
- Modify data
- Trigger workflows

MUST require:
- Clear user confirmation
- Visible preview of changes
- Standard UI execution path (not chat-only)

---

## Error & Uncertainty Handling

- Obscura must express uncertainty
- Must surface permission denials clearly
- Must never fabricate data

---

## Accessibility

- Keyboard navigable
- Screen-reader compatible
- Respect system theme and font scaling
