# Blazor offline diagnostics

Diagnose the first failing platform layer before changing application logic.

## Build or Razor compilation

1. Confirm SDK selection, target framework, and project.
2. Inspect restored assets and reference-pack availability.
3. Build the smallest affected project with `--no-restore`.
4. Fix the first actionable compiler/Razor diagnostic before downstream errors.
5. Verify namespaces, generic types, nullable values, callback signatures, and local framework XML docs.

Missing assets/reference packs are an environment blocker, not proof of a source defect.

## Markup renders but events do not fire

1. Determine whether the component is static SSR.
2. Locate its actual interactive boundary.
3. Verify interactive services and endpoint modes.
4. Inspect browser and server startup/circuit errors.
5. Verify parameters crossing the render boundary are supported.

Do not rewrite the handler until interactivity is proven.

## Duplicate initialization or data loading

Check prerendering, multiple component instances, parameter changes, reconnect/navigation behavior, and non-idempotent initialization. Record instance/request identity before adding global flags.

## Render loop or stale UI

Check after-render state changes, parameter mutation, external callbacks outside the renderer context, stale async results, unstable keys, and unnecessary `StateHasChanged`. Prove state ownership before adding forced renders.

## Circuit failure

Capture the earliest server exception and browser connection error. Check blocking work, unhandled event exceptions, disposal races, authentication expiry, proxy transport support, payload size, and server memory pressure.

## JS interop failure

Check render mode/prerender timing, module path and static asset availability, element presence, serialization, disposed references, enhanced navigation, and disconnect conditions. Distinguish “JavaScript unavailable yet” from a missing function/module.

## Forms or navigation failure

For forms, inspect the active model/`EditContext`, field expressions, validation providers/stores, submit path, antiforgery, and server error mapping. For navigation, inspect route ambiguity, parameter parsing, URI encoding, enhanced navigation, and lingering location-change subscriptions.

## Completion threshold

A conclusion names the evidence, failing layer, and smallest corrective action. If exact behavior cannot be proven offline, report the strongest hypothesis and the next local experiment.

