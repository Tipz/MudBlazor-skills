# Data Display catalog

Snapshot: official MudBlazor overview and component pages at commit `c0b219b`. Verify exact parameters against the installed package.

## Avatar — `MudAvatar`, `MudAvatarGroup`

Route: `/components/avatar`

Compact identity/media representation using initials, icons, or images, with sizes, shapes, grouping, outlined styling, and badges.

- Provide alternative identity text outside the image where needed.
- Use safe fallback initials/icons when images fail.

## Card — `MudCard` and card sections

Route: `/components/card`

Structured surface composed from header, media, content, and actions, with normal or outlined presentation.

- Use cards for independently meaningful grouped content, not every page section.
- Keep action order and heading semantics consistent.

## Carousel — `MudCarousel<T>`

Route: `/components/carousel`

Rotating/sliding content with data binding, item templates, navigation, and configurable transitions.

- Do not auto-advance critical content without pause/control.
- Preserve keyboard access and meaningful alternative text for media.
- Avoid loading all large slide assets eagerly.

## Chips — `MudChip<T>`

Route: `/components/chips`

Compact tags/actions with filled, text, or outlined variants; close/click behavior; icons; avatars; labels; sizes; and link rendering.

- Use closable chips for removable values and clickable chips only when the action is clear.
- For link chips, verify `Target`/`Rel` behavior as with buttons.

## Chip Set — `MudChipSet<T>`, `MudChip<T>`

Route: `/components/chipset`

Coordinates single or multiple chip selection, selected values, default/dynamic chips, variants, selected color, and accessibility.

- Give complex values stable equality.
- Choose single versus multiple selection explicitly and keep selection owned by the parent model.

## Data Grid — `MudDataGrid<T>` and columns

Route: `/components/datagrid`

Column-centric data grid with typed property/template columns, filtering, sorting, selection, editing, grouping, aggregation, server data, virtualization, resizing/reordering, context menus, and accessibility. Read `components-datagrid.md` for detailed patterns.

## Drop Zone — `MudDropContainer<T>`, `MudDropZone<T>`

Route: `/components/dropzone`

Drag/drop and reordering across one or more zones, with selectors, rules, styling, custom handles, disabled items, and persisted ordering scenarios.

- Provide a keyboard-accessible alternative to drag/drop.
- Validate allowed moves in application logic, not only with UI rules.
- Persist stable item IDs and explicit positions after reorder.

## Expansion Panels — `MudExpansionPanels`, `MudExpansionPanel`

Route: `/components/expansionpanels`

Collapsible sections supporting single/multiple expansion, async-loaded content, disabled state, padding/borders, and custom headers/icons.

- Keep headers descriptive and keyboard operable.
- Lazy-load only when expansion occurs and handle repeat/cancel behavior.
- Do not hide primary required content behind many nested panels.

## Image — `MudImage`

Route: `/components/image`

Image rendering with fallback, explicit/responsive sizing, fit, position, and standard image behavior.

- Set meaningful `Alt` text, or empty alt for purely decorative images.
- Reserve dimensions to reduce layout shift.
- Treat remote/user URLs according to the application's content-security policy.

## List — `MudList<T>`, `MudListItem<T>`

Route: `/components/list`

Simple/nested lists with single or multiple selection, interactive items, icons/avatars, binding, and accessibility.

- Set `T` explicitly and provide stable equality for selected complex values.
- Use navigation semantics for navigation lists and buttons for commands.
- Avoid deep nesting that obscures focus and hierarchy.

## Pagination — `MudPagination`

Route: `/components/pagination`

Page navigation with variants, shape, size, disabled state, control buttons, hidden-page behavior, and table integration.

- Translate between UI one-based pages and server zero-based indexes explicitly.
- Reset/clamp the current page when filtering changes the item count.
- Announce page changes and maintain sensible focus.

## Popover — `MudPopover`, `MudPopoverProvider`

Route: `/components/popover`

Anchored floating content with origin/placement, overflow behavior, relative width, nested popovers, complex/dynamic content, and individual settings.

- Ensure `MudPopoverProvider` is present in the correct interactive boundary.
- Choose flip/overflow behavior for viewport edges.
- Use dialog/drawer instead when content is large or modal.

## Simple Table — `MudSimpleTable`

Route: `/components/simpletable`

Styling wrapper for ordinary table markup, with hover, dense, and fixed-header options but without `MudTable` data logic.

- Use semantic `table`, header, body, row, and cell markup.
- Choose `MudTable<T>`/`MudDataGrid<T>` when sorting, paging, selection, templates, or server state is needed.

## Stepper — `MudStepper`, `MudStep`

Route: `/components/stepper`

Horizontal or vertical multi-step workflow with linear/non-linear navigation, labels, customization, active-step binding, navigation control, and dynamic steps.

- Validate before advancing in a linear workflow.
- Preserve entered state when moving backward.
- Make completion and error state visible in both content and step headers.

## Table — `MudTable<T>` and table helpers

Route: `/components/table`

Template-driven responsive data table with sorting, filtering, paging, selection, inline editing, cancellable server data, virtualization, grouping, fixed headers, and accessibility. Read `components-table.md` for detailed patterns.

## Tabs — `MudTabs`, `MudTabPanel`

Route: `/components/tabs`

Tabbed content with icons, positioning, centered/scrolling layouts, ordering/dragging, tooltips, badges, active-panel binding, dynamic panels, and keep-alive behavior.

- Tabs represent peer views, not sequential steps.
- Keep labels short and keyboard navigation intact.
- Choose keep-alive only when retaining component state outweighs memory/work cost.

## Timeline — `MudTimeline`, `MudTimelineItem`

Route: `/components/timeline`

Chronological/event display with orientation, position, alignment, opposite content, dot styling/icons, and per-item modifiers.

- Keep chronological order and readable date/time labels explicit.
- Provide a linear semantic reading order independent of visual side placement.

## Tooltip — `MudTooltip`

Route: `/components/tooltip`

Short contextual hint with arrow, color, rich content, transitions, and configurable activation events.

- Do not put essential instructions only in a tooltip.
- Ensure focus/touch users can access the information.
- Avoid interactive complex content; prefer popover/menu/dialog where appropriate.

## Tree View — `MudTreeView<T>`, `MudTreeViewItem<T>`

Route: `/components/treeview`

Hierarchical display with icons, single/multiple selection, item binding/templates, auto-expand, server-loaded children, filtering, and custom body/content.

- Give nodes stable identity and equality.
- Lazy-load children with cancellation and visible loading/error state.
- Preserve expected arrow-key and expand/collapse behavior.

