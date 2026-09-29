# Navigation catalog

Snapshot: official MudBlazor overview and component pages at commit `c0b219b`. Verify exact parameters against the installed package.

## Breadcrumbs — `MudBreadcrumbs`, `BreadcrumbItem`

Route: `/components/breadcrumbs`

Hierarchical location trail with custom separator, icons, templates, and collapsing behavior.

- Make all ancestors links and represent the current page as non-navigating/current where the API permits.
- Derive entries from route/application hierarchy instead of hand-maintaining contradictory trails.

## Link — `MudLink`

Route: `/components/link`

Styled navigation link supporting inline use, underline modes, icons, href navigation, and click handling.

- Use a link for navigation and a button for commands.
- For external new-tab links, preserve safe `rel` behavior and communicate the new context when appropriate.

## Menu — `MudMenu`, `MudMenuItem`

Route: `/components/menu`

Popup command/navigation list with button/icon/custom activators, dense mode, icons, dividers, max height, nesting, open-state binding, mouse/context-menu activation, placement, and modal/non-modal behavior.

- Keep nesting shallow and commands keyboard accessible.
- Use context menus only as an enhancement; expose important actions elsewhere.
- Ensure popover provider/interactivity prerequisites are met.

## Nav Menu — `MudNavMenu`, `MudNavLink`, `MudNavGroup`

Route: `/components/navmenu`

Application navigation tree with active links, groups, icons, density, color, borders/rounding, group-title customization, click handling, and single/multiple group expansion.

- Use route-aware `MudNavLink` for navigation.
- Keep information architecture stable and group labels concise.
- Combine with responsive drawer behavior for narrow screens.

