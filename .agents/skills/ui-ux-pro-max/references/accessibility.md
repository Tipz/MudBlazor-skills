# Accessibility and interaction feedback

Accessibility is part of the interaction contract, not a final styling pass. Map these requirements to the verified local component APIs through `mudblazor-offline`.

## Semantics and names

- Use the native semantic role for links, buttons, headings, form fields, tables, and status whenever possible.
- Every control needs an accessible name that matches or includes its visible label.
- Icon-only controls need a specific name; tooltips may support comprehension but do not replace the name.
- Keep heading levels and landmarks aligned with information structure.
- Associate instructions and errors with their fields.
- Do not make a generic container clickable when a button or link expresses the action.

## Keyboard behavior

All actions must be reachable and operable without a pointer. Keep Tab order consistent with visual and reading order; do not add positive tab indexes to repair layout.

For composite widgets such as grids, trees, tabs, menus, and listboxes, follow the keyboard model supplied by the component when it is correct. Do not layer custom shortcuts that conflict with text editing or browser behavior. Document application-wide shortcuts and provide a way to discover them.

## Focus

- Keep focus visible in every theme and state.
- On validation failure, focus the summary or first invalid field according to the form pattern.
- On dialog open, focus a safe useful element; on close, restore the trigger or logical successor.
- After deletion, move focus to the next item, previous item, parent, or stable heading.
- When content loads asynchronously, do not steal focus unless the user's action specifically requested the new context.
- Do not trap focus outside a true modal interaction.

## Dynamic feedback

Announce meaningful status changes without flooding assistive technology:

- validation summary changes;
- operation started/completed/failed when not otherwise focused;
- item added or removed;
- loading completion when it changes available actions.

Progress indicators need a meaningful accessible label and state. Avoid continuously announcing rapidly changing percentages.

## Visual accessibility

- Never use color alone for error, selection, required state, or progress.
- Preserve readable contrast for text, icons, focus, and boundaries that communicate state.
- Disabled content should remain legible enough to understand context.
- Support text zoom and narrow reflow without clipping controls or hiding errors.
- Respect reduced-motion preferences and avoid motion that is required to understand state.

## Tooltips and affordance

Use tooltips for concise supplemental explanation, unfamiliar icons, or truncated secondary content. Do not place essential instructions, errors, or the only copy of a long value in a hover-only tooltip. Ensure the trigger is focusable when keyboard users need the information.

Interactive elements should look actionable through position, label, shape, or established application convention. Hover alone is not an affordance.

## Review

Perform a keyboard-only pass: enter the page, reach all controls, operate composite widgets, submit invalid data, open and close dialogs, complete or cancel the workflow, and verify focus after dynamic changes. When tooling is available locally, supplement manual review with existing checks, but do not make external tooling a prerequisite.
