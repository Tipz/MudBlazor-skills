# CSS Utilities catalog

Snapshot: official MudBlazor overview and CSS utility pages at commit `c0b219b`. Utility names and breakpoint suffixes are version-sensitive; verify them against locally installed MudBlazor CSS.

## Border Radius

Route: `/utilities/border-radius`

Classes control default rounding, pill/circle shapes, removal, strength, individual sides, and individual corners.

- Prefer component `Square`, shape, or theme options when available.
- Use utilities for small layout-specific adjustments rather than duplicating CSS.
- Keep radius consistent with the design system.

Common families in documented MudBlazor versions include `rounded`, `rounded-0`, strength variants, side/corner variants, `rounded-circle`, and `rounded-pill`; inspect local CSS for exact spellings.

## Display

Route: `/utilities/display`

Responsive display classes control values such as none, block, inline, inline-block, flex, and inline-flex, including breakpoint-specific variants.

- Use display utilities for presentation, never authorization.
- Hiding with CSS can leave content in the DOM/accessibility tree depending on technique; verify behavior.
- Prefer one responsive subtree over duplicated interactive desktop/mobile trees.

Common class patterns use `d-*` and breakpoint infixes, for example `d-none`, `d-flex`, or version-supported `d-sm-*` forms.

## Flex

Route: `/utilities/flex`

Flex utilities cover enabling flex, direction, wrapping, grow/shrink, basis presets, gap, order, justify-content, align-items/content/self, and responsive variants.

- Prefer `MudStack` when a component-level one-dimensional layout is clearer.
- Use utilities for localized alignment within existing markup.
- Add wrapping and gap deliberately for responsive action groups.

Typical documented families include `d-flex`, `flex-row`, `flex-column`, `flex-wrap`, `flex-grow-*`, `justify-*`, and `align-*`; confirm exact local classes.

## Spacing

Route: `/utilities/spacing`

Margin/padding utilities encode property, side, breakpoint, and size; the docs also cover horizontal centering and negative margins.

- Prefer parent `Spacing`/grid gutter parameters where they express the layout.
- Use logical start/end forms (`ms`, `me`) instead of left/right when RTL support matters.
- Apply negative margins sparingly; they can hide overflow and focus indicators.

Common patterns include `ma-*`, `mx-*`, `my-*`, `mt-*`, `me-*`, `mb-*`, `ms-*` and corresponding `p*` forms, with breakpoint variants. Verify the installed scale and maximum value.

