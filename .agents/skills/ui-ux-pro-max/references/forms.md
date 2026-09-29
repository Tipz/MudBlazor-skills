# Forms and validation

Design forms around successful correction and preservation of work. Concrete form and field APIs belong to `mudblazor-offline` and Blazor form infrastructure belongs to `blazor-webapp-offline`.

## Field structure

- Use persistent visible labels. Placeholder text may show an example but is not a label.
- Mark required fields consistently. If most fields are required, consider marking optional fields instead, but explain the convention.
- Group fields by user intent and task sequence, not storage schema.
- Choose control type from the allowed values and input task, not from visual preference.
- Provide examples or constraints before input when users need them to succeed.
- Preserve meaningful whitespace and characters; do not silently normalize identifiers or filenames without a domain rule.

## Validation timing

Choose timing by error type:

- Validate format or simple local constraints after the user has interacted, commonly on blur or after a value becomes plausibly complete.
- Validate the full form on submit even if fields were checked earlier.
- Run server/domain validation when local rules cannot be authoritative.
- Avoid showing errors on untouched fields at initial render.
- Avoid expensive server checks on every keystroke unless deliberately debounced, cancellable, and useful.

Do not disable submit merely because untouched required fields are empty if that makes errors undiscoverable. It is acceptable to disable while a valid submission is actively processing or when a clear prerequisite is unmet and explained.

## Error placement

- Put a field-level error adjacent to its field and associate it programmatically.
- Use a form-level summary for cross-field, server, permission, or concurrency errors and link/focus to fields when possible.
- Keep user-entered values after recoverable failure.
- Clear an error when the relevant value changes or the condition is revalidated, not merely after a timeout.
- Name the problem and correction. Avoid vague messages such as “Invalid input” or “Something went wrong.”

For server validation, map known member errors to fields and retain unmatched errors at form level. Client validation is feedback; the server remains authoritative.

## Save and cancel

Define the outcome before styling actions:

- Save commits once, prevents duplicate submission, and communicates in-place progress.
- After success, either remain with an explicit saved state or navigate predictably; do not do both unexpectedly.
- Cancel means discard edits made in this editing context, not delete the underlying object.
- If cancel or navigation would lose meaningful changes, use dirty-state handling. Avoid prompts when nothing changed or immediately after a successful save.
- If draft persistence exists, distinguish “Save draft,” “Publish,” and “Discard” by actual consequences.

## Disabled and processing states

When saving:

- preserve the entered values;
- prevent another commit at the handler/service boundary;
- show progress in or near the initiating action;
- decide whether other fields may still change and make the state consistent;
- keep server errors durable until corrected or dismissed deliberately.

If the whole form becomes read-only due to permission or status, state why and keep values readable.

## Form review matrix

Verify:

- untouched initial form;
- missing required data;
- malformed local value;
- cross-field conflict;
- server validation failure;
- permission or concurrency failure;
- slow save and double activation;
- successful save;
- cancel with and without changes;
- navigation with unsaved changes;
- keyboard order, error focus, and long/localized text.
