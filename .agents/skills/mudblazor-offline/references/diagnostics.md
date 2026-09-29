# Offline diagnostics

Diagnose from the first failing layer. Avoid broad rewrites until the failure is localized.

## Build and Razor errors

1. Confirm the selected SDK from `global.json` and `dotnet --info`.
2. Confirm the target project and target framework.
3. Inspect `project.assets.json` for the resolved MudBlazor version and compatible assets.
4. Build the smallest affected project with `--no-restore`.
5. Address the first actionable compiler/Razor error before downstream errors.
6. Verify component namespace imports, generic types, binding pairs, callback signatures, and enum members against local XML docs.

If assets are missing and `--no-restore` fails, report that separately. It does not establish that the source change is invalid.

## UI renders but is not interactive

Check, in order:

1. Whether the component is static SSR or inside an interactive render boundary.
2. Whether the required interactive services and endpoints are registered/mapped.
3. Browser/runtime logs available locally.
4. Server circuit or WebAssembly startup failures.
5. Whether prerendering created a misleading initial HTML state.

Do not repeatedly rewrite the event handler until interactivity is proven.

## Dialog, menu, select, tooltip, or snackbar fails

Check:

1. MudBlazor service registration.
2. The relevant provider exists exactly where needed.
3. Provider and consumer share a compatible interactive renderer.
4. Ancestor `overflow`, transforms, stacking contexts, and layout clipping.
5. Verified service method, options, and result APIs for the installed version.

## Styling does not apply

Check:

1. Whether the stylesheet is loaded.
2. CSS isolation scope attributes and whether the target markup belongs to a child component.
3. Selector specificity and cascade order.
4. Theme/provider values and supported component parameters.
5. Generated markup in a local browser, if available.

Prefer a component parameter or theme value. If deep styling is necessary, wrap the component in an owned class and scope `::deep` beneath it. Document dependency on generated markup when unavoidable.

## Form does not validate or update

Check:

1. The form owns the expected model/edit context and it was not replaced silently.
2. The field expression points to the intended property.
3. The value type, nullable type, generic component type, and converter agree.
4. The application is not mixing incompatible validation flows.
5. Async validation and submit paths are awaited and exceptions are visible.
6. Server errors are mapped back to durable form state.

## Grid loads wrong or stale data

Check:

1. Page index conventions and page-size calculation.
2. Sort direction and allowed property mapping.
3. Filter normalization and active culture.
4. Total count corresponds to the filtered query.
5. Superseded requests are canceled or their results ignored.
6. The UI is not mutating the same collection while rendering.

## Runtime or circuit failures

- Capture the earliest server and browser exception available locally.
- Treat disposal races and cancellation as expected lifecycle conditions where appropriate.
- Look for non-serializable state crossing render boundaries.
- Avoid long blocking work on the renderer context.
- Confirm scoped service assumptions under Interactive Server circuits.
- Reproduce with the smallest affected route/component before changing global configuration.

## Completion threshold

A diagnostic conclusion should identify evidence, failure layer, and a focused corrective action. If the exact cause cannot be proven offline, give the strongest supported hypothesis and the smallest next local experiment rather than claiming certainty.

