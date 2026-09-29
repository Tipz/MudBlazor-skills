# Buttons catalog

Snapshot: official MudBlazor overview and component pages at commit `c0b219b`. Verify exact parameters against the installed package.

## Button — `MudButton`

Route: `/components/button`

General text/action button with filled, text, and outlined variants, colors, sizes, start/end icons, loading composition, full width, and link behavior. Read `components-actions-feedback.md` for implementation patterns.

- Use `ButtonType.Submit` only for actual form submission.
- Disable duplicate asynchronous commands and show progress.
- `Href` changes the control to navigation semantics; verify `Target` and `Rel` behavior locally.

## Button Group — `MudButtonGroup`

Route: `/components/buttongroup`

Visually groups related buttons and can propagate orientation, size, color, variant, elevation, and styling. It also supports split-button composition with a menu.

- Group only actions of the same conceptual level.
- Do not rely solely on adjacency to explain destructive versus safe actions.
- Preserve keyboard order when vertical orientation is used.

## Button FAB — `MudFab`

Route: `/components/buttonfab`

Floating action button for a prominent primary action, with filled/text/outlined variants and multiple sizes.

- Normally expose at most one primary FAB per view.
- Use a recognizable icon and an accessible label; add visible text for an extended FAB when meaning is not obvious.
- Do not obscure content or mobile navigation.

## Icon Button — `MudIconButton`

Route: `/components/iconbutton`

Compact button whose visual content is an icon. Supports built-in or font icons, color, size, and variants.

- Always supply an accessible name; a tooltip improves discoverability but is not a substitute for naming.
- Use for conventional compact actions, not for unfamiliar workflows that need text.

## Toggle Icon Button — `MudToggleIconButton`

Route: `/components/toggleiconbutton`

Two-state icon button with bindable toggled state and separate icons/colors for each state. It can also be driven through callbacks without two-way binding.

- Make both states visually and programmatically understandable.
- Persist state in the owning model when it matters beyond the component instance.
- Do not use a toggle for a one-shot command.

## Scroll To Top — `MudScrollToTop`

Route: `/components/scrolltotop`

Shows a trigger after scrolling and returns a configured scroll container to the top. Default and custom trigger content are documented.

- Target the actual scrolling element; nested layouts often scroll somewhere other than `window`.
- Keep the control keyboard accessible and avoid covering important bottom-corner actions.

