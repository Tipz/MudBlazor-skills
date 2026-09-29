---
name: ui-ux-pro-max
description: Design or review user flows, interaction behavior, states, validation, accessibility, and information architecture for data-heavy Blazor/MudBlazor business applications. Use for forms, navigation, tables, trees, dialogs, uploads, long-running operations, and desktop-first usability. Do not use for visual styling or concrete MudBlazor API details.
metadata:
  domain: business-application-ux
  network: offline
  compatibility: Codex, OpenCode, and Cursor with local filesystem access; no network required
---

# UI/UX Pro Max

Define how a business application should behave before choosing its visual treatment or concrete components. Optimize for task completion, error recovery, clarity, accessibility, and efficient repeated use.

## Offline contract

- Work from the user request, domain language, repository behavior, local requirements, and bundled references.
- Do not require web search, analytics services, Figma, cloud APIs, or an external pattern database.
- Do not assume product facts, user permissions, or operational guarantees that are absent from local evidence.
- Treat existing workflows as evidence, not automatically as good UX. Preserve deliberate conventions and call out harmful inconsistencies.

## Primary implementation stack

- .NET 10
- Blazor Web App
- Interactive Server
- MudBlazor

Implementation preferences:

- Prefer MudBlazor components over custom HTML widgets.
- Prefer existing MudBlazor capabilities before introducing custom JavaScript.
- Custom CSS is acceptable for layout and visual polish.
- JavaScript interop should only be introduced when Blazor/MudBlazor cannot reasonably solve the task.
- Do not introduce React, Vue, Angular, Tailwind, Bootstrap, shadcn/ui or another frontend framework unless explicitly requested.

This skill defines behavior and usability requirements, not Razor implementation or component signatures.

## Relationship with other skills

Use this skill for user goals, workflows, interaction models, information architecture, states, validation, recovery, and accessible behavior.

- For visual hierarchy, composition, typography, spacing, density, and aesthetic decisions, use `frontend-design` after the UX model is settled.
- For MudBlazor component selection, parameters, templates, and exact APIs, use `mudblazor-offline` after behavior is specified.
- For Blazor lifecycle, render modes, navigation infrastructure, state, circuits, and interop, use `blazor-webapp-offline`.

When several skills apply, preserve this handoff: UX model -> visual composition -> MudBlazor mapping -> Blazor implementation. Do not choose an interaction merely because a component makes it convenient.

## Progressive disclosure

Do not preload all references. Route only to the scenario at hand:

- Required fields, validation, save/cancel, server errors, or unsaved changes: [references/forms.md](references/forms.md).
- App navigation, information architecture, nested sections, trees, current location, or deep hierarchy: [references/navigation.md](references/navigation.md).
- Sorting, filtering, paging, selection, bulk actions, overflow, row actions, or large lists: [references/tables.md](references/tables.md).
- Loading, empty, error, disabled, dialogs, notifications, destructive actions, or long-running work: [references/states.md](references/states.md).
- Keyboard use, focus, labels, tooltips, contrast, announcements, or interaction feedback: [references/accessibility.md](references/accessibility.md).
- Drag/drop, multiple files, progress, retry, duplicates, large files, or interrupted uploads: [references/file-upload.md](references/file-upload.md).
- Desktop-first workflows, dense workspaces, long names, multi-pane layout, and repeated expert use: [references/desktop-apps.md](references/desktop-apps.md).

## Establish the workflow baseline

Before changing behavior:

1. Identify the user role, primary goal, entry point, success condition, and frequency of use.
2. Trace the current happy path and recovery paths in nearby screens or code.
3. Identify permissions, server authority, latency, concurrency, and irreversible effects that shape the UX.
4. Inventory the meaningful states and transitions, including initial, loading, partial, empty, error, success, disabled, stale, cancelled, and disconnected where relevant.
5. Distinguish a domain rule from a presentation convenience. Do not weaken validation or authorization for smoother UI.

If critical domain behavior is unknown, state the assumption in the UX plan. Prefer a reversible interaction and preserve user work.

## UX workflow

Work in this order:

1. Determine the user's goal.
2. Determine the shortest coherent primary workflow.
3. Determine required states and state transitions.
4. Determine possible input, server, permission, concurrency, and connectivity errors.
5. Determine destructive or irreversible operations.
6. Determine client and authoritative server validation strategy.
7. Determine loading and progress feedback.
8. Determine empty and first-use behavior.
9. Determine keyboard behavior and focus movement.
10. Determine accessibility names, semantics, announcements, and contrast requirements.
11. Determine whether confirmation is actually necessary or whether undo/recovery is better.
12. Map the resulting behavior to visual needs, then to locally verified UI components.

Record the outcome as an interaction contract: trigger, preconditions, visible state, allowed actions, completion, failure, cancellation, retry, focus result, and preserved data. Keep it proportional to the task; a small change does not need a full product specification.

## Core decision rules

- Keep the primary path obvious and make the next action predictable.
- Show system status where the user is looking and in language that names the affected object.
- Preserve valid input and selection after recoverable errors.
- Disable only the action that is temporarily unavailable; explain non-obvious disabled states.
- Prevent accidental duplicate execution at the event boundary, not only with visual disabling.
- Use confirmations for consequential, surprising, or hard-to-reverse actions. Do not confirm ordinary saves.
- Prefer undo for quick reversible actions when the system can guarantee it.
- Use transient notifications for confirmation, not for durable errors or information required to proceed.
- Keep long values inspectable. Truncation may improve scanning but must not destroy access to the full value.
- Preserve selection, expansion, filters, and working context when refresh or navigation semantics allow it.
- Treat client-side validation, hidden controls, and disabled buttons as guidance, never authorization.

## Map behavior without duplicating component documentation

Describe capabilities first: searchable selection, single-choice confirmation, multi-selection with batch action, cancellable progress, hierarchical navigation, or server-paged grid. Then use `mudblazor-offline` to select and verify the installed MudBlazor API.

Do not include remembered parameter names in the UX plan. If the available component cannot support a required behavior, revisit the mapping while preserving the user goal.

## Verification

Review the complete state model, not only the happy path. Use realistic long names, large result sets, server validation, no results, permission loss, slow operations, cancellation, retry, and keyboard-only operation where relevant.

Check that focus remains logical after dialogs, validation, dynamic content, deletion, and navigation; that status changes are perceivable; and that repeated execution cannot occur accidentally. If no interactive or assistive-technology review was performed, report the exact checks still needed.
