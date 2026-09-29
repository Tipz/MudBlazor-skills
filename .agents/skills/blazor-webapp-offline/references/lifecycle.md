# Component lifecycle

Use the lifecycle method whose contract matches the work; verify overrides against the installed framework.

## Initialization and parameters

- Initialization is for instance setup not dependent on later parameter changes.
- Parameter-set logic can run repeatedly. Recompute only state derived from current parameters and avoid overwriting user edits accidentally.
- Avoid long synchronous work in lifecycle methods.
- For asynchronous loads, track cancellation/request identity so older completion cannot replace newer parameter state.

Do not mutate parent-owned parameters as local state. Copy into explicit local/edit state when ownership must diverge.

## Rendering

- Rendering should be deterministic from current state and free of external side effects.
- Event callbacks and awaited lifecycle work normally trigger rendering; do not add `StateHasChanged` reflexively.
- External callbacks may need dispatch through the renderer using the locally established invocation pattern.
- Use `ShouldRender` only for a measured problem and preserve correctness when it returns false.
- Use stable `@key` values when identity matters for mutable repeated subtrees.

## After render

Use `OnAfterRender{Async}` for work requiring rendered elements or browser DOM.

- Guard one-time work with `firstRender` only when it is truly once per component instance.
- Updating state after render can create a render loop; change state only when needed.
- During prerendering, browser interop is unavailable and after-render behavior differs by framework/render mode. Verify locally.
- Element references are meaningful only after their element rendered and become invalid when that element is removed/replaced.

## Disposal

Implement the appropriate disposal interface for owned resources.

- Unsubscribe events and observables.
- Stop timers and cancel outstanding work.
- Dispose async JS modules/references with expected disconnect handling.
- Avoid updating component state after disposal.
- Do not dispose injected services unless the component created/owns them.

## Error handling

Use an error boundary where a subtree can recover or present a controlled failure. Log the original exception. Do not use a boundary to suppress repeated deterministic errors without correcting state or recovery behavior.

