# Offline diagnostics

Diagnose from the first failing layer. Avoid broad rewrites until the failure is localized.

## Build and Razor errors

1. Confirm the target project and target framework.
2. Inspect `project.assets.json` for the resolved MudBlazor version and compatible assets.
3. Build the smallest affected project with `--no-restore`.
4. Address the first actionable compiler/Razor error before downstream errors.
5. Verify MudBlazor namespace imports, generic types, binding pairs, callback signatures, parameters, and enum members against local package XML docs.

If assets are missing and `--no-restore` fails, report that separately. It does not establish that the source change is invalid.

## UI renders but is not interactive

Use `blazor-webapp-offline` to verify the render boundary, event processing, prerendering, and circuit/client startup. Do not rewrite a MudBlazor event handler until platform interactivity is proven.

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

## Lifecycle, circuit, navigation, or JS interop failures

Use `blazor-webapp-offline`. Keep this diagnostic focused on MudBlazor services, providers, component contracts, generated markup, theme/CSS behavior, and library-specific state.

## Completion threshold

A diagnostic conclusion should identify evidence, failure layer, and a focused corrective action. If the exact cause cannot be proven offline, give the strongest supported hypothesis and the smallest next local experiment rather than claiming certainty.

