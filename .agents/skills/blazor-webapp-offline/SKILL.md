---
name: blazor-webapp-offline
description: Build, modify, review, and troubleshoot .NET Blazor Web App applications without network access. Use for Razor component lifecycle, render modes, Interactive Server, prerendering, state, navigation, dependency injection, forms infrastructure, JS interop, circuits, disposal, and Blazor-specific runtime or build problems. Do not use for component-library-specific APIs unless the task is primarily a Blazor platform issue.
metadata:
  domain: dotnet-blazor-webapp
  network: offline
  compatibility: Codex, OpenCode, and Cursor with local filesystem and shell access; no network required
---

# Blazor Web App Offline Development

Work from the repository, resolved build assets, and installed .NET reference packs. Match the project's target framework and hosting/rendering architecture rather than a remembered template.

## Offline contract

- Do not browse, fetch URLs, call remote MCP servers, or run commands that may download SDKs, workloads, templates, or packages.
- Do not run `dotnet restore`, `dotnet add package`, workload installation, or package update commands unless the user explicitly allows network access.
- If a required SDK, workload, reference pack, or restored asset is missing, continue with locally supported work and identify the exact missing artifact.
- Never invent lifecycle, render-mode, forms, routing, authentication, or interop APIs. Verify exact signatures locally when they matter.

## Progressive disclosure

Do not preload all references.

1. Start with this `SKILL.md`.
2. Load only the smallest reference that covers the request.
3. Load another reference only when the first does not contain enough behavioral or API evidence.
4. Do not load component-library documentation for a platform-only Blazor task.

## Establish the local baseline

Before changing code:

1. Read applicable repository instructions and nearby implementation patterns.
2. Inspect `global.json`, `Directory.Build.*`, project files, target frameworks, nullable settings, and `obj/project.assets.json` when present.
3. Identify the actual app model from `Program.cs`, `App.razor`, `Routes.razor`, imports, endpoint mapping, and `@rendermode` placement.
4. Distinguish static SSR, Interactive Server, Interactive WebAssembly, and Interactive Auto. Do not infer the render mode from the project name.
5. Identify prerendering, authentication, enhanced navigation, streaming rendering, and any client project only when relevant.

For commands and installed reference-pack locations, read [references/local-evidence.md](references/local-evidence.md).

## Source-of-truth order

1. Compiling project code, generated assets, tests, and observable local behavior.
2. The exact installed ASP.NET Core and .NET reference packs, XML docs, and assemblies.
3. Locally available framework source for the matching version.
4. Focused references bundled with this skill.
5. Model knowledge only as a hypothesis checked against local evidence.

Bundled references are a convenience guide, not an API authority. Prefer `project.assets.json`, reference-pack XML documentation, installed assemblies, and locally available matching source when exact signatures or version behavior matter.

## Route the task

- Static SSR, Interactive Server/WebAssembly/Auto, prerendering, endpoint/service setup, or render boundaries: [references/render-modes.md](references/render-modes.md).
- Component initialization, parameters, rendering, `StateHasChanged`, async work, disposal, and error boundaries: [references/lifecycle.md](references/lifecycle.md).
- Circuits, reconnects, scoped services, concurrency, latency, and server resource behavior: [references/interactive-server.md](references/interactive-server.md).
- Component/application state, persistence, serialization boundaries, and cancellation of stale work: [references/state.md](references/state.md).
- `EditForm`, `EditContext`, validation stores, submit behavior, and server validation: [references/forms.md](references/forms.md).
- Routing, `NavigationManager`, route/query parameters, enhanced navigation, and navigation interception: [references/navigation.md](references/navigation.md).
- `IJSRuntime`, element/module references, prerendering-safe calls, callbacks, and cleanup: [references/js-interop.md](references/js-interop.md).
- Build, rendering, event, circuit, forms, routing, or interop failures: [references/diagnostics.md](references/diagnostics.md).

## Implementation rules

- Preserve the repository's hosting model, render-mode boundaries, component organization, and state-management conventions unless the user asks to change them.
- Keep render methods and parameter setters free of avoidable side effects.
- Avoid blocking calls, `async void`, unobserved fire-and-forget work, and unnecessary `StateHasChanged` calls.
- Pass cancellation tokens through supported operations and prevent stale results from replacing newer state.
- Dispose subscriptions, timers, cancellation sources, JS modules/references, and other owned resources using the lifecycle supported by the component.
- Treat browser/client state as untrusted. Authorization and trusted validation belong on the server operation or endpoint.
- Do not place secrets in code or state that may execute, download, or serialize to the client.
- Do not edit generated `obj/` or `bin/` files.

## Verification

1. Inspect the diff and affected Razor/C# syntax.
2. Build the smallest relevant project with `dotnet build <project> --no-restore`.
3. Run relevant tests with `--no-restore`; use `--no-build` only after a compatible successful build.
4. Verify behavior in each affected render mode; compilation alone does not prove interactivity, navigation, reconnect, or browser interop.
5. Report any manual browser/circuit check that was not performed.

If restored assets or reference packs are absent, report that separately from source failures and do not trigger a restore.

## Completion report

State the target framework and render mode that governed the change, the local evidence used, build/test results, and any unverified browser, prerender, reconnect, or version-sensitive behavior.

