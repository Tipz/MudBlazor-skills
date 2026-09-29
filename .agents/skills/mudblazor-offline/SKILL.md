---
name: mudblazor-offline
description: Build, modify, review, and troubleshoot MudBlazor UI without network access. Use for MudBlazor components, forms, validation, DataGrid, Table, TreeView, dialogs, snackbars, layout, theming, responsive UI, accessibility, component API verification, and MudBlazor-specific build or runtime errors. Do not use for general Blazor lifecycle, render-mode, state, navigation, DI, circuit, or JS interop tasks.
compatibility: Codex, OpenCode, and Cursor with local filesystem and shell access; no network required
metadata:
  domain: dotnet-mudblazor
  network: offline
---

# MudBlazor Offline Development

Work entirely from local evidence. Produce UI code that matches the repository's installed MudBlazor package and established component conventions.

## Offline contract

- Do not browse, fetch URLs, call remote MCP servers, query online documentation, or run commands that may download packages.
- Do not run `dotnet restore`, `dotnet add package`, package upgrades, workload installs, or template installs unless the user explicitly allows network access.
- Never silently replace a missing package or API with a guessed equivalent.
- If a required artifact is unavailable locally, continue with all work that local evidence supports, then name the exact missing artifact and give a command the user can run later in a connected environment.
- Treat package XML documentation, assemblies, generated files, and the compiling project as more authoritative than this skill's examples.

## Progressive disclosure

Do not preload the full documentation snapshot.

1. Start with this `SKILL.md`.
2. Load only the smallest reference file that covers the task.
3. Load another reference only when the first does not contain enough API or behavioral evidence.
4. For general Blazor platform behavior, use `blazor-webapp-offline` instead of loading unrelated MudBlazor references.

## Start by establishing the local baseline

Before changing code:

1. Read repository instructions such as `AGENTS.md`, `README.md`, `global.json`, `Directory.Build.*`, and `Directory.Packages.props` when present.
2. Locate the relevant project and inspect its target framework, `PackageReference` items, nullable settings, imports, and Razor/component conventions.
3. Determine the effective MudBlazor version. Resolve central package management, MSBuild properties, and `project.assets.json` rather than reading only the literal `PackageReference`.
4. Inspect MudBlazor service registration and theme/popover/dialog/snackbar provider placement only when relevant to the requested feature.
5. Inspect nearby components and tests. Follow established namespace, partial-class, validation, localization, styling, and UI-state conventions unless the user asks to change them.

If the task is primarily about lifecycle, render modes, prerendering, application state, navigation, dependency injection, circuits, or JS interop, use the `blazor-webapp-offline` skill.

For commands and local evidence locations, read [references/local-evidence.md](references/local-evidence.md).

## Source-of-truth order

When an API or behavior is uncertain, use this order:

1. The repository's compiling code, generated NuGet assets, and tests.
2. The exact installed MudBlazor package: XML docs, reference assembly, bundled content, README, and source files if present.
3. Locally available MudBlazor source matching the installed version.
4. The focused MudBlazor documentation snapshot bundled with this skill.
5. General model knowledge only for a hypothesis that will be checked by compilation or local API evidence.

Bundled documentation is a convenience index, not an API authority. When exact signatures matter, prefer `project.assets.json`, installed package XML documentation, installed assemblies, reference assemblies, and locally available matching source.

Do not invent component parameters, enum members, event callback types, or generic arguments. Search the installed XML documentation by fully qualified member name or search existing usage in the repository. If evidence remains ambiguous, state the uncertainty and choose the smallest reversible implementation.

## Route the task

Read only the references needed for the request:

- Components, forms, validation, data display, dialogs, snackbars, layout, theming, CSS, accessibility, or responsive behavior: [references/mudblazor-patterns.md](references/mudblazor-patterns.md).
- Snapshot scope, provenance, version caveats, and the official page-to-file index: [references/documentation-snapshot.md](references/documentation-snapshot.md).
- Theme colors, typography, elevation, and icons: [references/catalog-foundation.md](references/catalog-foundation.md).
- App shell, containers, grid, drawer, responsive visibility, surfaces, dividers, stack, and toolbar: [references/catalog-layout.md](references/catalog-layout.md).
- Buttons, button groups, FAB, icon/toggle buttons, and scroll-to-top: [references/catalog-buttons.md](references/catalog-buttons.md).
- Autocomplete, checkbox, pickers, upload, form, typed fields, selection controls, slider, switch, and text input: [references/catalog-inputs.md](references/catalog-inputs.md).
- Avatar, card, carousel, chips, grids/tables, drag/drop, lists, paging, popover, stepper, tabs, timeline, tooltip, and tree view: [references/catalog-data-display.md](references/catalog-data-display.md).
- Breadcrumbs, links, menus, and navigation menu: [references/catalog-navigation.md](references/catalog-navigation.md).
- Alerts, badges, dialogs, message boxes, progress, skeletons, snackbars, and overlays: [references/catalog-feedback.md](references/catalog-feedback.md).
- Border radius, display, flex, and spacing utility classes: [references/catalog-utilities.md](references/catalog-utilities.md).
- `MudDataGrid`, typed columns, filtering, selection, editing, grouping, paging, server data, and virtualization: [references/components-datagrid.md](references/components-datagrid.md).
- `MudTable`, templates, responsive rows, sorting, selection, editing, server data, grouping, and virtualization: [references/components-table.md](references/components-table.md).
- `MudForm`, `EditForm`, validation, `MudSelect`, multi-selection, `MudTextField`, update timing, and input behavior: [references/components-forms-inputs.md](references/components-forms-inputs.md).
- `MudDialog`, typed dialog parameters/results, `MudButton`, loading/link behavior, `ISnackbar`, and snackbar configuration: [references/components-actions-feedback.md](references/components-actions-feedback.md).
- Build/runtime failures, hydration or interactivity problems, overlay issues, CSS isolation, validation failures, or performance investigation: [references/diagnostics.md](references/diagnostics.md).

## Implementation rules

- Preserve the project's architecture. Do not impose code-behind, inline `@code`, CQRS, state containers, or a component-library abstraction when the repository uses another coherent approach.
- Prefer MudBlazor component parameters, templates, theme tokens, and utility classes over brittle selectors or DOM-dependent CSS.
- Keep domain and application logic outside presentation components. UI-specific state and event handlers may remain in the component or its existing partial class.
- Keep component UI state explicit. Account for loading, empty, error, disabled, unauthorized, and cancellation states when relevant.
- Use typed models and expressions for forms and columns. Avoid reflection or string member names unless required by the verified local API.
- Respect nullable reference types and cancellation tokens used by the project.
- Avoid blocking calls, `async void`, and unobserved fire-and-forget UI work.
- Dispose resources owned by the component; use `blazor-webapp-offline` when lifecycle/disposal behavior is the task itself.
- Keep secrets, authorization checks, and trusted validation on the server. Client-side visibility or disabled state is not authorization.
- Prefer semantic markup, labels, keyboard access, focus management, and adequate contrast. Icon-only actions need an accessible name or tooltip appropriate to the verified component API.
- Do not edit generated `obj/` or `bin/` files.

## MudBlazor checks

Before considering a UI change complete, verify:

- If MudBlazor interaction does not work, first verify the component's interactive render boundary using `blazor-webapp-offline`. Static SSR can render a control without processing its events.
- MudBlazor services are registered once in the correct host project.
- Required theme, popover, dialog, and snackbar providers exist in a layout/root that participates in the correct render mode. Do not add duplicates without diagnosing placement first.
- Event callback signatures, two-way binding pairs, generic type parameters, and nullable values match the installed API.
- Provider placement, overlay stacking, and CSS overflow are checked before adding arbitrary z-index overrides.

## Verification

Use the narrowest offline verification that proves the change:

1. Inspect the diff and check affected Razor/C# syntax and namespaces.
2. Run a targeted build with `--no-restore`, for example `dotnet build <project> --no-restore`.
3. Run relevant tests with `--no-restore`; use `--no-build` only after a successful compatible build.
4. Run repository-provided formatters or analyzers only when already installed and configured locally.
5. For UI behavior that cannot be exercised locally, report the exact manual checks still needed; do not claim visual or interactive verification that was not performed.

If `project.assets.json`, a reference pack, workload, or package is missing, do not trigger a restore. Report the blocker and distinguish it from code failures.

## Completion report

Summarize:

- what changed and why;
- which local MudBlazor version and evidence governed the implementation;
- build/test commands run and their results;
- any unverified interaction, visual check, missing local artifact, or version-sensitive assumption.

