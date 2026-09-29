# Application states, feedback, and long-running operations

Every asynchronous or stateful interaction needs a visible, recoverable model. Do not reduce all feedback to a spinner or snackbar.

## State inventory

Consider only states relevant to the task:

- initial or not started;
- loading with no prior content;
- refreshing with usable prior content;
- partial result;
- empty;
- ready;
- disabled or read-only;
- processing;
- success;
- recoverable error;
- terminal error;
- cancelled;
- stale, disconnected, or reconnecting.

Define allowed actions and preserved data for each state. Avoid contradictory combinations such as enabled submit plus an active duplicate operation.

## Loading and progress

- Use a local indicator near the affected region for local work; do not block the whole page unnecessarily.
- Preserve prior content during refresh when it remains safe to use, and mark it as updating.
- Use determinate progress only when the measure is meaningful and reasonably accurate.
- For indeterminate work, say what is happening without inventing a percentage.
- After a short delay, provide more context for unusually long operations and expose cancellation when supported.
- Avoid layout shifts caused by indicators appearing and disappearing.

## Empty states

Distinguish first use, no matching results, and removed/unavailable content. Explain the condition and offer the next relevant action. Avoid decorative empty-state copy that hides useful filters or consumes a desktop workspace.

## Errors

- Put a correctable error near the cause.
- Keep blocking or durable errors visible until resolved.
- State what failed, what was preserved, and what the user can do next.
- Offer retry only when retry is safe and likely to help.
- Preserve diagnostic identifiers when useful, without exposing sensitive internals.
- Do not use a transient notification as the only presentation of an actionable failure.

## Disabled and read-only states

Prefer hiding actions users can never perform and disabling temporarily unavailable actions when their existence is useful context. Explain a non-obvious disabled state through nearby text or an accessible description; do not rely on a hover-only tooltip.

## Dialogs and confirmations

Use a dialog for a bounded decision requiring attention. Do not use one for long, deeply nested work.

A confirmation should name the object, consequence, reversibility, and primary action. Require stronger friction only for exceptional harm, such as entering a name for irreversible deletion. Do not confirm routine saves or actions with a reliable immediate undo.

After close, return focus to the trigger or a logical successor if the trigger disappeared.

## Notifications

- Use inline status for information needed to continue.
- Use a transient notification for brief confirmation of a completed action.
- Avoid duplicate feedback such as dialog, banner, and snackbar all reporting the same success.
- Make notification action labels specific and keep them keyboard accessible.

## Long-running operations

For work such as creating a large ZIP:

1. Prevent duplicate starts at both UI and operation boundaries.
2. Name the operation and affected scope.
3. Show queued/preparing/running/finalizing phases when they are real and helpful.
4. Use determinate bytes/items only when the denominator is trustworthy; otherwise use indeterminate progress with current phase.
5. Allow cancellation only when the backend honors it, and distinguish “cancelling” from “cancelled.”
6. Decide what happens if the user navigates away or the Interactive Server circuit disconnects.
7. On success, present the resulting artifact or next action where it remains discoverable.
8. On failure, preserve inputs, identify completed cleanup or partial output, and offer safe retry.

Retry must not accidentally create duplicate artifacts or repeat a non-idempotent side effect. If recovery requires starting over, say so.
