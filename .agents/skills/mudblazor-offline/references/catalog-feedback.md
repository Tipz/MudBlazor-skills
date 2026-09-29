# Feedback catalog

Snapshot: official MudBlazor overview and component pages at commit `c0b219b`. Verify exact parameters against the installed package.

## Alert — `MudAlert`

Route: `/components/alert`

Persistent in-page status/message with severity, filled/outlined/text variants, density, icon control, shape, elevation, alignment, and close event.

- Match severity to meaning, not decoration.
- Use for durable information; use a snackbar for transient confirmation.
- Ensure closable critical information remains recoverable.

## Badge — `MudBadge`

Route: `/components/badge`

Small status/count marker attached to child content. The snapshot page includes basic and interactive configuration.

- Keep counts short; use a bounded display such as `99+` when appropriate.
- Do not make color the only indication of status.
- Provide an accessible text equivalent when the badge changes meaning.

## Dialog — `MudDialog`, `IDialogService`, `MudDialogProvider`

Route: `/components/dialog`

Modal/inline interaction with global and per-dialog options, typed data passing, async result, scroll behavior, nesting, keyboard/focus handling, and custom styling. Read `components-actions-feedback.md` for detailed patterns.

## Message Box — `MudMessageBox`, `IDialogService`

Route: `/components/messagebox`

Convenience confirmation/message dialog supporting custom and multiline messages, dialog options, and button order.

- Use for simple confirmation; use a custom dialog for forms or complex decisions.
- Make destructive action text explicit and handle cancel/dismiss separately.

## Progress — `MudProgressCircular`, `MudProgressLinear`

Route: `/components/progress`

Circular or linear progress in determinate/indeterminate modes, with sizes, custom content, bounds, buffer, rounded/striped/background/label options, and vertical linear presentation.

- Use determinate progress only when a meaningful fraction is known.
- Provide adjacent status text and accessible progress semantics.
- Do not leave indefinite progress without timeout, cancellation, or error handling for long operations.

## Skeleton — `MudSkeleton`

Route: `/components/skeleton`

Layout placeholder with text/rectangle/circle-like variants and pulse or wave animations.

- Match the approximate final layout to reduce shift.
- Mark placeholders as non-content and expose a loading status.
- Respect reduced-motion preferences where supported.

## Snackbar — `ISnackbar`, `MudSnackbarProvider`

Route: `/components/snackbar`

Transient notification service with severity, variants, position, actions, close/navigation behavior, custom content/icons, removal, and duplicate prevention. Read `components-actions-feedback.md` for detailed patterns.

## Overlay — `MudOverlay`

Route: `/components/overlay`

Visual layer for blocking/dimming/loader scenarios with auto-close, absolute/fixed positioning, color, z-index, and child content.

- Use absolute mode only inside a correctly positioned ancestor.
- If interaction is blocked, expose busy state and protect against duplicate commands.
- An overlay alone is not a fully accessible modal; use a dialog for modal interaction and focus management.

