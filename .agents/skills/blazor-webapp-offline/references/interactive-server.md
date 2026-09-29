# Interactive Server and circuits

Interactive Server keeps component state and rendering on the server. The browser sends events and receives UI diffs over a circuit.

## Design implications

- Network latency affects every interactive event; avoid chatty input handlers and batch/debounce work when appropriate.
- A circuit can disconnect and reconnect. Do not equate temporary connection loss with user logout or guaranteed component disposal.
- Server memory scales with active circuits and retained component/service state.
- Browser state is still untrusted even though component code runs on the server.

## Dependency injection lifetimes

Scoped services can live for the circuit rather than one HTTP request. Do not keep a request-oriented database context or other unsafe mutable resource alive merely because it is scoped.

- Prefer short operations and the repository's factory/service pattern.
- Do not store one user's mutable state in singleton services.
- Protect shared mutable state with an appropriate concurrency design.

## Concurrency and renderer context

Component callbacks are coordinated by the renderer, but background services/timers may call from outside its context. Marshal UI updates through the established renderer invocation pattern. Avoid blocking the circuit with synchronous I/O or `.Result`/`.Wait()`.

## Reconnect and duplicate work

- Make important commands idempotent or protect them with operation identity.
- Disable/serialize duplicate submissions, but enforce uniqueness on the trusted backend too.
- Persist only the state that must survive component/circuit loss and define expiry/user ownership.
- Treat cancellation/disposal races as expected lifecycle conditions.

## Diagnosis

For a non-interactive or disconnected UI, inspect endpoint/service configuration, server logs, browser connection errors, authentication expiry, proxy WebSocket/long-polling behavior, and resource pressure before rewriting components.

