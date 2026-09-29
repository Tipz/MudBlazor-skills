# Local Blazor evidence

Use local evidence without contacting package feeds or documentation sites.

## Project and app-model files

- `*.sln`, `*.slnx`, `*.csproj`, `global.json`
- `Directory.Build.props`, `Directory.Build.targets`, `Directory.Packages.props`
- `obj/project.assets.json`, `obj/*.nuget.g.props`, `packages.lock.json`
- `Program.cs`, `App.razor`, `Routes.razor`, `_Imports.razor`
- layouts, routable components, authentication state setup, and client project when present

Useful searches:

```text
rg --files -g "*.sln" -g "*.slnx" -g "*.csproj" -g "global.json" -g "Directory.*.*"
rg -n "AddRazorComponents|AddInteractive|MapRazorComponents|AddAdditionalAssemblies|@rendermode|IComponentRenderMode" .
rg -n "OnInitialized|OnParametersSet|OnAfterRender|ShouldRender|StateHasChanged|IJSRuntime|NavigationManager" .
```

Local-only commands:

```text
dotnet --info
dotnet --list-sdks
dotnet --list-runtimes
dotnet list <project.csproj> package --no-restore
dotnet build <project.csproj> --no-restore
```

Avoid commands that query outdated/vulnerable packages or feeds.

## Installed framework contracts

Locate the dotnet root from `dotnet --info`. Compile-time contracts normally live under:

```text
<dotnet-root>/packs/Microsoft.AspNetCore.App.Ref/<version>/ref/<tfm>/
<dotnet-root>/packs/Microsoft.NETCore.App.Ref/<version>/ref/<tfm>/
```

Search matching XML docs for exact types/members. Shared runtime implementations live under `<dotnet-root>/shared`, but reference packs define what the project can compile against.

When local framework source exists, confirm it matches the target/runtime version before using implementation details. Do not treat a newer SDK's docs or source as authoritative for an older target framework.

## Evidence discipline

- Record the effective SDK, target framework, and render mode.
- Separate missing restored assets from compiler/source failures.
- A successful build does not prove interactive browser behavior.
- A server log and browser log can describe different halves of one failure; inspect both when available.

