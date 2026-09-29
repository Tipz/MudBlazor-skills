# JavaScript interop

## Call timing

Browser-dependent interop requires an interactive browser renderer. Do not call it during static SSR/prerender initialization. DOM or element-reference work belongs after the relevant element has rendered.

- Use `firstRender` only for per-instance one-time initialization.
- If the target element is conditional, initialize when it actually appears and clean up when it disappears.
- Avoid triggering an unconditional state update from every after-render call.

## Modules and references

Prefer scoped JS modules when supported by the project.

- Cache the module reference per owning component/service rather than importing on every event.
- Dispose owned module/object references asynchronously.
- Treat disconnect exceptions during Interactive Server cleanup as expected where the local runtime contract indicates.
- Do not retain stale `ElementReference` or .NET object references after the owning component is gone.

## Data boundary

- Pass small serializable DTOs, not service/domain graphs.
- Validate data returned from JavaScript.
- Do not send secrets or trusted authorization decisions to the browser.
- For large/high-frequency payloads, consider streaming or a less chatty design supported by the installed framework.

## JavaScript-to-.NET callbacks

Expose the smallest callback surface, validate inputs, and dispose the object reference. Avoid static globally reachable callbacks unless the scenario genuinely requires them. Marshal resulting UI updates through the renderer context.

## Navigation and DOM ownership

Do not let third-party JavaScript mutate DOM that Blazor assumes it owns without an explicit integration boundary. Account for enhanced navigation when initialization previously depended on full page loads.

