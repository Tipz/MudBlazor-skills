# MudBlazor implementation patterns

These are decision guidelines, not an API catalog. Verify exact names and signatures against the installed package.

## Components and binding

- Set generic type parameters explicitly when inference is ambiguous, nullable values are involved, or column/form expressions require a stable type.
- For two-way binding, verify the component's value/value-changed pair and expression parameter. Do not mix `@bind-*` with a duplicate explicit changed callback unless the local API supports the intended pattern.
- Prefer component parameters and typed templates over querying rendered DOM.
- Use stable keys for repeated mutable UI when item identity matters.
- Avoid mutating a parameter-owned collection in place unless the component contract and application ownership make that intentional.

## Forms

- Bind controls to a dedicated input model rather than directly to persistence entities when validation or overposting matters.
- Use expression-based validation where supported, and keep error messages near their fields plus an optional summary for form-level errors.
- Disable submission while processing and show progress without destroying form state.
- Preserve user input after recoverable server errors.
- Explicitly handle nullable selections, clear behavior, culture-sensitive numeric/date parsing, and default enum values.
- For dynamic forms or model replacement, verify whether the form/edit context must be recreated.

## Data display and grids

Choose the simplest component that satisfies behavior already expected by the project. Do not enforce `MudDataGrid` merely because data is tabular; compare required sorting, filtering, paging, editing, virtualization, selection, hierarchy, and templating with the locally available components.

For server-backed grids:

- Translate the verified grid state into a typed application query.
- Keep paging, sorting, and filtering on the server when the full data set is not loaded.
- Return total-count and page data consistently.
- Cancel superseded loads and ignore stale results.
- Handle zero rows, errors, and retry separately from loading.
- Never trust client-provided sort/filter identifiers without mapping them to allowed server expressions.

For editable rows:

- Use an edit copy when cancellation must restore original values.
- Validate before persistence.
- Define concurrency behavior and show conflicts instead of overwriting silently.

## Dialogs, snackbars, menus, and popovers

- Verify both service registration and provider placement.
- Treat dialog completion as asynchronous and handle cancel/dismiss distinctly from a confirmed result.
- Pass small typed parameters; load sensitive or large state through application services.
- Avoid opening repeated dialogs/snackbars from rerendering lifecycle code.
- If an overlay is clipped or misplaced, inspect provider placement and ancestor overflow/stacking contexts before adding arbitrary z-index values.
- Use snackbars for transient feedback, not durable errors the user must act on.

## Layout and responsive UI

- Start with MudBlazor layout primitives, breakpoints, spacing utilities, and theme values verified in the installed version.
- Design for narrow layouts deliberately: stacking, drawer behavior, grid column priority, action wrapping, and touch targets.
- Avoid viewport checks via JS when CSS or built-in breakpoint services solve the problem.
- Keep main content landmarks and heading hierarchy semantic even when components generate most markup.

## Theme and CSS

- Centralize palette, typography, spacing, and component defaults when they are application-wide.
- Prefer semantic theme tokens over repeated literal colors.
- Use CSS isolation for component-owned styling, but remember that isolated selectors may not naturally match descendant markup rendered by child components.
- Use `::deep` narrowly from an owned wrapper, and verify generated markup locally. Avoid selectors tied to undocumented internal class structure.
- Use global CSS only for genuinely global behavior such as application shell, theme-level overrides, or third-party markup that cannot be scoped reliably.
- Do not use CSS to imitate a supported component parameter.

## Accessibility and localization

- Every input needs a programmatic label; placeholder text alone is not a label.
- Icon-only controls need an accessible name. Preserve visible focus and keyboard operation.
- Use appropriate button/link semantics and avoid clickable non-interactive containers.
- Announce meaningful async status changes when the application accessibility pattern supports it.
- Localize user-facing strings through the project's existing localization system.
- Respect the active culture for formatting and parsing; do not hard-code separators or date formats.
- Check RTL layout when the application supports RTL cultures.

## Performance

- Measure or identify a concrete rerender/data-loading problem before adding complexity.
- Avoid expensive enumeration, allocation, or service calls during rendering.
- Use virtualization only when item count and layout constraints justify it and the installed component API supports the scenario.
- Keep event handlers and parameters stable enough to avoid avoidable child work, but do not trade clarity for speculative micro-optimizations.
- For Interactive Server, consider circuit memory and payload frequency; for WebAssembly, consider download size and client CPU.

