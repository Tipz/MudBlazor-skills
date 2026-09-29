# MudBlazor documentation snapshot

This skill contains a curated offline snapshot of the official MudBlazor component documentation requested by the user. It is a task-oriented summary, not a replacement for the complete API surface.

## Provenance

- Retrieved: 2026-09-29
- Official documentation site: `https://mudblazor.com`
- Official source repository: `https://github.com/MudBlazor/MudBlazor`
- Source branch: `dev`
- Source commit: `c0b219bfdf8241f64d2b48c013403b8e42ac5dd2`
- Commit date: 2026-09-28
- Commit subject: `Build: Update AGENTS.md guidance (#13922)`

The public component pages require client-side Blazor execution and returned only the application error shell to a plain fetch. Content and examples were therefore read from the corresponding `src/MudBlazor.Docs/Pages/Components` files in the official repository.

The source is MIT licensed. The examples in this skill are shortened and adapted for agent guidance rather than copied as a complete documentation mirror.

## Reference layers

- `catalog-*` files provide broad discovery coverage across the 71-card component overview. Use them to find candidate component families, not as exact API documentation.
- `components-*` files provide task-focused implementation guidance for selected high-use components and include version-sensitive caveats. Confirm exact members against the installed package.
- `mudblazor-patterns.md` provides cross-cutting implementation decisions shared by multiple components. It does not define UX flows, visual composition, or exact component signatures.

This separation is a maintenance contract: add broad inventory to a catalog, component-specific implementation depth to a `components-*` guide, and reusable engineering guidance to the patterns file. Avoid duplicating the same guidance across layers.

## Version rule

The snapshot tracks the documentation source above, not necessarily the MudBlazor version installed in the user's project. Before emitting code:

1. Determine the project's resolved MudBlazor version.
2. Search the installed package XML documentation for every version-sensitive parameter or method.
3. Prefer existing compiling project usage.
4. Treat a construct shown here as a candidate until the local build succeeds with `--no-restore`.

Pay particular attention to dialog APIs, data-grid editing modes and callbacks, collection types used by multi-select, and server-data delegate signatures; these have changed across MudBlazor releases.

## Page index

| Public page | Offline reference | Main documented topics |
|---|---|---|
| `/components/datagrid` | `components-datagrid.md` | Typed columns, sorting, filters, editing, grouping, selection, aggregation, server data, virtualization |
| `/components/table` | `components-table.md` | Templates, responsive data labels, paging, sorting, selection, inline edit, server data, grouping |
| `/components/form` | `components-forms-inputs.md` | MudForm, EditForm, DataAnnotations, FluentValidation, dirty-only validation, readonly/disabled |
| `/components/select` | `components-forms-inputs.md` | Typed values, multi-select, custom display/conversion, placement, keyboard navigation |
| `/components/textfield` | `components-forms-inputs.md` | Variants, helper text, adornments, binding, debounce, input type, multiline, masks |
| `/components/dialog` | `components-actions-feedback.md` | Service and inline dialogs, options, typed parameters, results, nesting, focus, keyboard use |
| `/components/button` | `components-actions-feedback.md` | Variants, size, icons, loading, full width, links, rel behavior |
| `/components/snackbar` | `components-actions-feedback.md` | Severity, global/per-item options, actions, lifecycle, custom content, de-duplication |

## Features visible in the source snapshot

The DataGrid page includes basic and advanced grids, property/template columns, styling, form/cell/inline editing, multi-level grouping, single/multiple sorting, custom comparers, simple/column/custom filtering, row selection and detail views, sizing/resizing, aggregation, sticky columns, server data, virtualization, observability, culture, column reordering/panel, context menus, validation, and accessibility.

The Table page includes templated rows, selected-row and hover events, filtering/paging, sorting, multi-selection, fixed header/footer, column groups, inline editing, cancellable server data, loading/empty content, record comparers, related rows, horizontal scrolling, virtualization, programmatic scroll/focus, grouping, and accessibility.

The Form, Select, TextField, Dialog, Button, and Snackbar pages cover the focused cases summarized in their routed references. For a feature listed here but not demonstrated in the summary, search the local package and repository before implementing it.

## Complete 71-card catalog

All entries displayed in the official overview are summarized locally:

- Foundation: `catalog-foundation.md` (4)
- Layout: `catalog-layout.md` (9)
- Buttons: `catalog-buttons.md` (6)
- Inputs: `catalog-inputs.md` (17)
- Data Display: `catalog-data-display.md` (19)
- Navigation: `catalog-navigation.md` (4)
- Feedback: `catalog-feedback.md` (8)
- Utilities: `catalog-utilities.md` (4)

Total: 71. Foundation and Utilities include design tokens/features rather than Razor components, but remain in the catalog because they materially affect correct MudBlazor implementation.


