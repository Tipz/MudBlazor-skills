---
name: frontend-design
description: Design or review the visual hierarchy, composition, spacing, typography, density, and responsive presentation of business UI. Use before implementation when a Blazor/MudBlazor screen needs a clearer or more intentional visual design. Do not use for interaction flows, usability rules, or MudBlazor API selection.
metadata:
  domain: frontend-visual-design
  network: offline
  compatibility: Codex, OpenCode, and Cursor with local filesystem access; no network required
---

# Frontend Design

Turn product purpose and real content into a deliberate visual composition before choosing component details. Preserve an established application design language unless the user explicitly asks to change it.

## Offline contract

- Work from the brief, repository, existing screens, local assets, and bundled references.
- Do not require web search, Figma, image generation, a cloud service, or an external design system.
- Do not fetch fonts, icons, templates, or inspiration during the normal workflow. Reuse locally available assets and typography.
- Treat visual review from a runnable local application or supplied screenshot as stronger evidence than abstract style advice.

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

These preferences constrain the eventual implementation; this skill does not define Razor lifecycle, component APIs, bindings, or JavaScript interop.

## Relationship with other skills

Use this skill for visual hierarchy, composition, presentation, density, and aesthetic consistency.

- For user flows, interaction behavior, validation, application states, accessibility behavior, and usability decisions, use `ui-ux-pro-max` first.
- For concrete MudBlazor component choice, parameters, theming APIs, and implementation details, use `mudblazor-offline` after the visual direction is clear.
- For Blazor render modes, lifecycle, navigation infrastructure, state, and interop, use `blazor-webapp-offline`.

When several skills apply, preserve this handoff: UX model -> visual composition -> MudBlazor mapping -> Blazor implementation. Do not reopen settled UX decisions merely to make the screen more decorative.

## Progressive disclosure

Do not preload all references. Read only what the task needs:

- Page hierarchy, emphasis, grouping, or review of an existing screen: [references/visual-hierarchy.md](references/visual-hierarchy.md).
- Spacing rhythm, alignment, whitespace, compactness, or control density: [references/spacing.md](references/spacing.md).
- Type scale, labels, line length, numeric data, or text hierarchy: [references/typography.md](references/typography.md).
- Forms, dashboards, detail pages, workspaces, cards, or responsive composition: [references/layout-patterns.md](references/layout-patterns.md).
- Generic AI-dashboard symptoms, excess decoration, or a final visual critique: [references/anti-patterns.md](references/anti-patterns.md).

## Establish the visual baseline

Before proposing changes:

1. Identify the primary user task, audience, content, and expected desktop/mobile use.
2. Inspect nearby screens, shared layouts, theme values, CSS, typography, icons, and spacing conventions.
3. Separate intentional design language from accidental inconsistency. Reuse the intentional parts.
4. Identify constraints already decided by UX, accessibility, localization, or the component library.
5. For an existing UI, diagnose the few visual problems that most impair scanning or comprehension; do not redesign unrelated areas.

If evidence is incomplete, make the smallest reversible visual assumption and state it. Do not invent a new brand or design system to fill a gap.

## Design workflow

Work in this order before coding:

1. Determine the primary user task.
2. Determine the page and information hierarchy.
3. Identify primary, secondary, and tertiary actions.
4. Identify the dominant visual area and the expected scanning path.
5. Reduce unnecessary containers, borders, and competing emphasis.
6. Establish a small, repeatable spacing rhythm.
7. Establish a restrained typography hierarchy.
8. Group related controls and separate unrelated regions.
9. Check density against task frequency and data volume.
10. Check alignment, visual balance, and use of whitespace.
11. Check consistency with the existing application and real content.
12. Check narrow-width reflow and priority before handing off for implementation.

Express the result as a concise visual plan: hierarchy, major regions, alignment, density, spacing rhythm, typography roles, surface treatment, responsive changes, and exceptions to existing language. A small ASCII wireframe is useful when spatial relationships are otherwise ambiguous.

## Visual decision rules

- Let importance determine size, position, contrast, and whitespace; do not make every region equally prominent.
- Use proximity and alignment before adding borders or surfaces.
- Prefer one clear page-level primary action. Repeated row-level actions may be locally primary without competing with it.
- Match density to the work: frequent desktop operations and data comparison usually need more compact treatment than onboarding or marketing content.
- Keep repeated patterns truly consistent. Use an exception only when it communicates different meaning or priority.
- Spend visual distinctiveness where it supports the product context; keep the rest quiet.
- Use real or structurally realistic content when judging wrapping, balance, empty space, and table width.
- Preserve visible focus, readable contrast, semantic order, and error/status visibility supplied by the UX plan.

## Anti-pattern gate

Reject or justify each of these before implementation:

- excessive cards, nested cards, or every section inside `MudPaper`;
- borders, shadows, gradients, pills, or rounded corners applied without hierarchy;
- arbitrary accent colors or multiple competing primary buttons;
- icon-only controls whose meaning is not immediately clear;
- giant empty hero regions in operational business screens;
- inconsistent spacing, floating alignments, or center-aligned forms;
- decoration that reduces useful information density;
- identical dashboard tiles used for unrelated information;
- generic AI-dashboard styling unrelated to the application's domain;
- a new visual language that ignores established application patterns.

The detailed critique checklist is in [references/anti-patterns.md](references/anti-patterns.md).

## Handoff and verification

Hand the visual plan to `mudblazor-offline`; do not prescribe unverified component parameters. During implementation, change the design only when a verified framework constraint requires it, and preserve the intent rather than the exact primitive.

Review the result at representative widths with realistic long values and state variations. Check hierarchy at a glance, alignment, wrapping, density, repeated spacing, focus visibility, and consistency with adjacent screens. If no rendered review was possible, report that explicitly.
