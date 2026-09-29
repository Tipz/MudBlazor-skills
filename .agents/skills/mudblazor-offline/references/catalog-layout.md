# Layout catalog

Snapshot: official MudBlazor overview and component pages at commit `c0b219b`. Verify exact parameters against the installed package.

## App Bar — `MudAppBar`

Route: `/components/appbar`

Top or bottom application bar for branding, navigation triggers, and contextual actions. It commonly lives inside `MudLayout` and coordinates with drawers.

- Use `MudSpacer` to separate leading and trailing groups.
- Keep app-bar actions focused; move overflow actions to a menu.
- Verify fixed/bottom positioning, elevation, color, dense mode, and drawer clipping locally.

## Container — `MudContainer`

Route: `/components/container`

Centers page content and constrains its maximum width. Use fluid mode when content should occupy available width and fixed/max-width behavior for readable application pages.

- Put page padding at the container/shell level rather than repeating it in every child.
- Choose a `MaxWidth` appropriate to the content, not merely the largest available value.

## Drawer — `MudDrawer`, `MudDrawerContainer`

Route: `/components/drawer`

Side navigation or contextual panel with temporary, persistent, responsive, and mini variants. Anchor, overlay, breakpoint, clipping, width, and open state are configurable in the documented versions.

- Use temporary drawers on narrow screens and a persistent/mini pattern only when content width supports it.
- Bind open state deliberately and close temporary navigation after selection where appropriate.
- Diagnose overlay/provider/layout placement before adding z-index CSS.

## Grid — `MudGrid`, `MudItem`

Route: `/components/grid`

Responsive 12-column layout. Put `MudItem` children inside `MudGrid` and assign widths per breakpoint (`xs`, `sm`, `md`, `lg`, `xl`, and version-specific larger breakpoints).

- Specify `xs` when the mobile width should be explicit.
- Use grid spacing for gutters instead of margins on every item.
- Use `MudStack` for one-dimensional layouts; use `MudGrid` for two-dimensional responsive columns.

## Hidden — `MudHidden`

Route: `/components/hidden`

Conditionally renders or hides content based on breakpoints and listens to viewport changes through MudBlazor's browser viewport service.

- Do not use visibility as authorization; hidden client content is not protected.
- Prefer CSS responsive utilities when only presentation changes and component lifecycle/state need not change.
- Avoid duplicating expensive interactive subtrees for desktop and mobile without measuring the cost.

## Paper — `MudPaper`

Route: `/components/paper`

General surface/container with elevation, outline, square/rounded shape, size, and normal HTML attributes. It is the basic building block for panels and grouped content.

- Use `MudCard` when content has card semantics/sections; use `MudPaper` for generic surfaces.
- Prefer theme spacing and elevation over custom surface CSS.

## Divider — `MudDivider`

Route: `/components/divider`

Horizontal or vertical visual separator, including inset and middle variants. Use it to separate related regions, not as a substitute for spacing or headings.

- Ensure a vertical divider has a parent layout that gives it height.
- If separation is semantic, preserve meaningful structure in addition to the visual line.

## Stack — `MudStack`

Route: `/components/stack`

Flex-based one-dimensional layout supporting row/column direction, responsive direction, spacing, wrapping, line breaks, justification, alignment, stretching, and configurable HTML tag.

- Prefer `MudStack` to repeated `d-flex`/margin combinations for component groups.
- Enable wrapping for action rows that must survive narrow widths.
- Use semantic tags when the stack represents a list, navigation region, or other meaningful structure.

## ToolBar — `MudToolBar`

Route: `/components/toolbar`

Horizontal command/content container commonly used in app bars, tables, and data grids. It supports content wrapping in the documented snapshot.

- Group related actions and provide accessible labels for icon actions.
- Use `MudSpacer` for alignment, but allow wrapping or overflow behavior on narrow screens.

