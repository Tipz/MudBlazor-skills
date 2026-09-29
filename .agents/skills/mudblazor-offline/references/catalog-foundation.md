# Foundation catalog

Snapshot: official MudBlazor overview and documentation source at commit `c0b219b`. Verify exact APIs against the installed package.

## Colors — `Color`, `Colors`, theme palettes

Route: `/features/colors`

Use semantic component colors such as `Color.Primary`, `Color.Secondary`, `Color.Success`, `Color.Warning`, `Color.Error`, `Color.Info`, `Color.Dark`, and `Color.Inherit` when a component exposes `Color`. Use theme palette values or MudBlazor CSS variables for custom CSS so light/dark themes remain coherent. Material color constants are available for deliberately fixed colors.

- Prefer a theme token over a literal hex value for application-wide semantics.
- Configure light and dark palettes centrally through the project's `MudTheme`.
- In CSS, prefer documented `--mud-palette-*` variables; confirm the variable exists in the installed version.
- Do not communicate state by color alone.

## Typography — `MudText`, `Typo`, `Align`

Route: `/components/typography`

`MudText` applies theme typography presets and semantic text behavior. Choose `Typo` for visual hierarchy, `Align` for alignment, and the verified HTML-tag option when document semantics need a specific element.

- Keep one logical page heading and a consistent heading hierarchy.
- `Typo.overline` is intentionally uppercase; select a different preset rather than undoing it with CSS.
- Use inline rendering only when the text belongs in an inline flow.
- Put application-wide font family, weights, and sizes in the theme instead of repeating styles.

## Shadows — elevation

Route: `/features/elevation`

Elevation represents surface depth. Components such as `MudPaper`, `MudCard`, `MudAppBar`, and overlays expose an `Elevation` parameter; utility classes follow the installed MudBlazor elevation scale.

- Use a small, consistent set of levels; higher is not automatically more important.
- Set elevation to zero for flat surfaces and use `Outlined` where supported when a border is the intended distinction.
- Avoid custom `box-shadow` values unless the theme/component cannot express the design.
- Check contrast and boundaries in both light and dark palettes.

## Icons — `MudIcon`, `Icons`

Route: `/features/icons`

Use `MudIcon` for standalone icons and component icon parameters for built-in adornments/actions. Built-in names are exposed through groups such as `Icons.Material.Filled`, `Outlined`, `Rounded`, `Sharp`, and `TwoTone`; availability is version-dependent.

- Prefer symbolic constants to copied SVG path strings.
- An icon-only action needs an accessible name and usually a tooltip.
- Decorative icons should not introduce redundant accessible text.
- Set icon color and size through component parameters when possible.
- Verify custom icon font/SVG setup locally before relying on it.

