# Component and application state

Choose state lifetime deliberately.

## State scopes

- Local component state: transient UI details owned by one component instance.
- Cascading state: shared by a known subtree; avoid turning it into an implicit global store.
- Scoped application service: shared according to runtime DI semantics; circuit-scoped on Interactive Server and client-app-scoped in WebAssembly.
- URL state: navigation/filter/page state that should be linkable or survive refresh.
- Browser storage: client-controlled persistence; never trusted authorization or secret storage.
- Server persistence: durable/trusted state with explicit user/tenant ownership.

## Async state

Represent loading, empty, error, success, cancellation, and retry separately when the UI needs them. For replaceable work such as search:

1. cancel or supersede the prior request;
2. capture the request identity/input;
3. apply the result only if still current;
4. avoid showing cancellation as a user-facing error unless meaningful.

## Prerender and serialization

State crossing prerender/interactive or server/client boundaries must follow the target framework's supported persistence/serialization mechanism. Do not serialize secrets, service objects, open streams, database entities with unintended graphs, or user state without ownership checks.

## Updates and ownership

- Prefer a single owner and explicit callbacks/actions over shared mutable collections.
- When collection identity matters, replace or notify according to the repository's pattern.
- Do not call `StateHasChanged` from arbitrary services; notify components and let them marshal/render safely.
- Dispose state-service subscriptions.

