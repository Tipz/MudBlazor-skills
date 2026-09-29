# Inputs catalog

Snapshot: official MudBlazor overview and component pages at commit `c0b219b`. Typed input and validation APIs are version-sensitive; verify them against the installed package.

## Autocomplete — `MudAutocomplete<T>`

Route: `/components/autocomplete`

Search-driven typed selection for large or dynamic option sets. The documentation covers presentation, validation, keyboard navigation, progress, strict/coercion behavior, and cancellable search.

- Pass the provided cancellation token through remote/database searches.
- Debounce expensive searches and ignore stale responses.
- Decide explicitly whether arbitrary text is allowed or selection must match an item.
- Provide stable display and equality logic for complex values.

## Check Box — `MudCheckBox<T>`

Route: `/components/checkbox`

Boolean or converted-value input with labels, custom icons, density/size, readonly mode, keyboard navigation, content placement, and optional indeterminate state.

- Use `bool?` only when a meaningful third state exists.
- Keep label text clickable and descriptive.
- Verify converters when binding types other than `bool`.

## Color Picker — `MudColorPicker`

Route: `/components/colorpicker`

Color selection using supported views/modes, palette, alpha channel, drag interaction, dialog/inline/static presentation, elevation, and `MudColor` values.

- Decide whether alpha is allowed and normalize stored formats.
- Validate contrast if users configure foreground/background colors.
- Use a bounded custom palette when unrestricted brand colors are undesirable.

## Date Picker — `MudDatePicker`

Route: `/components/datepicker`

Date input supporting masks/parsing, readonly mode, disabled/custom days, action buttons, culture, dialog/static presentation, views, colors, elevation, navigation to a date, fixed values, and accessibility.

- Use a date-only domain type where the project and installed API support it; otherwise define time-zone conversion explicitly.
- Set culture/format deliberately and distinguish empty from default dates.
- Disable invalid dates in UI and validate again on the server.

## Field — `MudField`

Route: `/components/field`

Field-style visual wrapper for custom content that should resemble MudBlazor inputs, including label/helper/adornment/layout and padding behavior.

- Use a typed input component when actual input behavior and validation are required.
- When composing a custom field, connect label, description, errors, focus, and keyboard behavior explicitly.

## File Upload — `MudFileUpload<T>`

Route: `/components/fileupload`

File selection and drag/drop with custom activator/content, selected-file templates, multiple/accept filters, validation, append behavior, and event options.

- Treat file name, extension, MIME type, and client-reported size as untrusted.
- Enforce server-side size/content limits, safe storage names, authorization, and malware policy.
- Stream uploads; do not read unbounded files into memory.
- Surface per-file progress, failure, cancellation, and retry when uploads are nontrivial.

## Form — `MudForm`

Route: `/components/form`

Coordinates MudBlazor input validation, validity/errors, validation/reset methods, delegate validation, FluentValidation patterns, dirty-only validation, labels, and readonly/disabled states. Standard `EditForm` integration is also documented. Read `components-forms-inputs.md` for patterns.

## Focus Trap — `MudFocusTrap`

Route: `/components/focustrap`

Constrains keyboard focus within a subtree, typically for modal or transient UI.

- Use only while the region is active.
- Ensure Escape/cancel behavior and restore focus to the invoking control.
- Do not trap focus in ordinary page content.

## Highlighter — `MudHighlighter`

Route: `/components/highlighter`

Highlights one or multiple text fragments, with case sensitivity, boundary behavior, markup/styling options, and examples inside lists/tables.

- Preserve original text and use highlighting only as presentation.
- Treat markup-enabled input as potentially unsafe; do not render unsanitized user HTML.
- Define case/culture expectations for search results.

## Numeric Field — `MudNumericField<T>`

Route: `/components/numericfield`

Typed numeric input with min/max, step/spin buttons, nullable types, immediate/debounced updates, localization, formatting, validation, and common field properties.

- Pick the precise numeric `T`; do not round money through binary floating point.
- Align UI bounds with server/domain validation.
- Verify culture-specific decimal parsing and empty/null behavior.

## Radio — `MudRadioGroup<T>`, `MudRadio<T>`

Route: `/components/radio`

Single selection from a small visible option set, with color, density, size, placement, readonly/disabled states, and accessibility support.

- Use a select/autocomplete for long lists.
- Give the group a meaningful label and preserve arrow-key navigation.
- Make enum/default/null behavior explicit.

## Rating — `MudRating`

Route: `/components/rating`

Rating input/display with value binding, max value, icons, color, sizes, readonly/disabled modes, events, and accessibility options.

- Distinguish “not rated” from the minimum rating.
- Use readonly mode for display and an accessible textual equivalent where context requires it.

## Select — `MudSelect<T>`, `MudSelectItem<T>`

Route: `/components/select`

Typed single or multiple selection with custom selection text, select-all, complex objects, converters, dynamic sizing, placement, and keyboard navigation. Read `components-forms-inputs.md` for binding patterns.

## Slider — `MudSlider<T>`

Route: `/components/slider`

Numeric/range-style input with min/max/step, filled track, ticks and labels, nullable values, value label, size, and vertical orientation.

- Use only when approximate relative choice is natural; use `MudNumericField<T>` for precise entry.
- Give the slider an accessible label and expose current value.
- Validate bounds server-side.

## Switch — `MudSwitch<T>`

Route: `/components/switch`

Immediate on/off setting with labels, colors, thumb icons, alternate converted types, content placement, readonly mode, keyboard navigation, and size.

- Use for a setting that takes effect immediately; use a checkbox for selection in a form/list.
- Avoid ambiguous negative labels.

## Text Field — `MudTextField<T>`

Route: `/components/textfield`

Typed text-like input supporting variants, helper/error text, disabled/readonly, clear button, adornments, counters, nullables, immediate/debounced updates, input types, multiline, masks, and programmatic control. Read `components-forms-inputs.md` for patterns.

## Time Picker — `MudTimePicker`

Route: `/components/timepicker`

Time selection with readonly mode, action buttons, dialog/static presentation, initial hour/minute view, edit mode, color/elevation, minute step, and keyboard navigation.

- Define whether the value is local wall-clock time, duration, or part of a zoned timestamp.
- Apply minute-step constraints in trusted validation as well as UI.
- Verify nullable/empty behavior and culture formatting locally.

