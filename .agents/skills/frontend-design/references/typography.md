# Typography for application UI

Typography establishes hierarchy and scanning speed. Reuse locally available typefaces and the application's existing typography before proposing a new family.

## Define roles, not one-off styles

Use a restrained set of roles such as:

- page title;
- section heading;
- body and field value;
- label;
- helper or metadata text;
- table header;
- status or annotation;
- numeric emphasis where the content warrants it.

Each role should have a stable size, weight, line height, and color treatment. Avoid tiny differences that cannot be perceived reliably.

## Hierarchy

- Use size sparingly; weight, spacing, and placement can establish hierarchy without oversized headings.
- Keep business-application page titles proportionate to the working area.
- Sentence case is the default for labels and actions unless the product language requires otherwise.
- Avoid repeated all-caps eyebrow labels, decorative monospace metadata, and arbitrary highlighted words.
- Do not use muted text for content users must read to complete the task.

## Readability

- Keep prose line length bounded; do not stretch instructions across a wide desktop workspace.
- Give wrapped text enough line height, especially errors, help, and long item names.
- Prevent labels and units from appearing to belong to the wrong value.
- Use truncation only when the full value remains accessible through expansion, detail, or another reliable mechanism.
- Never hide the meaningful end of a filename or identifier merely to preserve symmetry.

## Data-heavy screens

- Use consistent number, date, time, unit, and status formats.
- Align comparable numeric values and preserve signs, decimals, and units.
- Distinguish headers from values without making every header high-contrast.
- Use tabular numerals only if the available local font supports them and comparison materially benefits.
- Keep row typography compact but readable; avoid bolding every value.

## Forms

- Keep labels visible; placeholders are examples or hints, not replacements for labels.
- Place helper and error text where its ownership is unambiguous.
- Use consistent required/optional notation defined by the UX plan.
- Keep action names specific and stable through the flow: the visual treatment must not obscure the verb.

## Review

Test with long localized strings, a two-line validation error, long filenames, large numbers, and mixed enabled/disabled states. Verify that hierarchy survives wrapping and that secondary text remains legible.
