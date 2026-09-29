# Blazor Web App guidance

Apply this guidance only after identifying the target framework and the repository's render-mode architecture.

## Hosting and render modes

A Blazor Web App can combine static SSR and interactive components. Determine the actual mode from registrations, endpoint mapping, `@rendermode`, imports, and component placement; do not infer it from the project name.

- Static SSR renders HTML but does not provide persistent component event handling.
- Interactive Server executes component logic on the server and maintains a circuit. Design for disconnects, latency, disposal, and server resource usage.
- Interactive WebAssembly executes client-side after required assets load. Browser-visible code and state are untrusted.
- Interactive Auto may use different modes across visits. Do not depend on a single execution location unless the app deliberately constrains it.

Place interactive controls and MudBlazor providers inside compatible interactive boundaries. If an event handler renders but never fires, establish interactivity before debugging the handler.

## Startup inspection

Verify locally rather than pasting a generic `Program.cs`:

- Razor component service registration.
- Interactive server and/or WebAssembly component registration.
- MudBlazor service registration in the host that constructs the relevant service provider.
- Authentication and authorization registrations used by components.
- Endpoint mapping and additional assemblies for routable components.
- Static files and antiforgery middleware required by the project template/version.

Add only missing registrations. Preserve repository ordering when middleware order is meaningful.

## Providers and root layout

MudBlazor features commonly rely on theme, popover, dialog, and snackbar providers. Inspect the installed version and existing root layout before editing.

- Put providers high enough to serve all consumers, but within the correct render boundary.
- Avoid duplicate providers because they can create conflicting overlay hosts or inconsistent state.
- Diagnose missing popovers, dialogs, and snackbars by checking registration, provider presence, render mode, and z-index/overflow in that order.
- Keep application-wide theme configuration centralized unless per-section themes are intentional.

## Lifecycle and prerendering

- Initialization can run in prerendered and interactive phases. Make data loading idempotent or persist state when duplicate work would be harmful.
- Browser JS is unavailable during prerendering. Perform DOM-dependent interop after render when the component is interactive, using a first-render guard only when the operation truly runs once per component instance.
- Cancel outstanding work and release resources during disposal.
- Do not assume an element reference is usable before it has rendered.
- Marshal external callbacks to the renderer with the project's established pattern when callbacks originate outside the component synchronization context.

## State and data access

- Keep durable/trusted state on the server or in an appropriate application service.
- Treat scoped services differently in server circuits and WebAssembly; verify lifetime implications before storing mutable user state.
- Avoid direct long-lived database contexts in interactive components. Prefer the repository's service/factory pattern and short operations.
- Represent loading, empty, failure, cancellation, and retry states explicitly.
- Debounce or cancel superseded searches and server-data requests when users can trigger them rapidly.
- Make submit commands idempotent or guard against duplicate submission when server latency or reconnects can repeat actions.

## Forms and validation

Choose one coherent validation flow per form:

- Standard `EditForm`/`EditContext` integration when application validation is based on Blazor forms.
- MudBlazor form validation when the project deliberately uses `MudForm` and its verified validation contract.

Do not combine both casually. Verify how validation messages, touched state, model replacement, and async validation behave in the installed versions. Server validation remains authoritative even when client/UI validation provides immediate feedback.

## Navigation, authorization, and security

- UI authorization controls visibility; server endpoints and operations must independently authorize access.
- Do not put secrets in components that can execute or serialize on the client.
- Preserve return URLs safely and avoid open redirects.
- Account for enhanced navigation or streaming rendering only when enabled in the target framework/project.
- Do not disable antiforgery or weaken cookie/authentication settings to fix a UI symptom.

