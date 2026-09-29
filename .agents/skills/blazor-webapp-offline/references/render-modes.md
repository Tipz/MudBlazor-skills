# Render modes and prerendering

Determine render mode from actual service registration, endpoint mapping, `@rendermode` directives/attributes, and component placement.

## Modes

- Static SSR renders HTML per request. Component event handlers do not remain active after the response.
- Interactive Server maintains component state on the server over a circuit.
- Interactive WebAssembly runs the interactive component in the browser after client assets load.
- Interactive Auto can choose server interactivity initially and WebAssembly on later visits; code must tolerate either configured execution location.

Do not add interactivity globally merely to fix one control. Choose the smallest boundary consistent with application architecture and library/provider requirements.

## Startup evidence

Inspect, rather than paste from a generic template:

- Razor component registration.
- Interactive Server and/or WebAssembly registration.
- Endpoint mapping and configured interactive render modes.
- Additional assemblies containing routable components.
- static files, antiforgery, authentication, authorization, and project-version middleware.
- whether a separate client project supplies WebAssembly components.

## Prerendering

Prerendering creates initial HTML before browser interactivity. Initialization may therefore occur in more than one execution phase or instance.

- Make externally visible initialization idempotent where duplicate work matters.
- Persist/transfer initial state using the project's framework-version pattern rather than static mutable state.
- Browser APIs and DOM-dependent JS are unavailable while prerendering.
- Do not assume an element reference is usable until an interactive render has completed.
- A correct initial HTML render does not prove that events are wired.

## Boundaries and serialization

Crossing a server/client render boundary can require serializable parameters and changes dependency availability. Avoid passing callbacks, service instances, or non-serializable state across a boundary unless the exact framework contract supports it.

If rendered markup appears but events do nothing, prove the component is interactive before changing its event handler.

