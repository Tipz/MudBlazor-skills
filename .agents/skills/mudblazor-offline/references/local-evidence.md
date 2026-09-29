# Local evidence and API discovery

Use these techniques without contacting the network. Adapt commands to the available shell and repository conventions.

## Discover projects and versions

Useful files:

- `*.sln`, `*.slnx`, and `*.csproj`
- `Directory.Build.props`, `Directory.Build.targets`, and `Directory.Packages.props`
- `packages.lock.json`
- `obj/project.assets.json` and `obj/*.nuget.g.props`
- `Program.cs`, `_Imports.razor`, root/layout components, and affected Razor components

Prefer fast repository search:

```text
rg --files -g "*.sln" -g "*.slnx" -g "*.csproj" -g "Directory.*.*"
rg -n "MudBlazor|AddMudServices|MudThemeProvider|MudPopoverProvider|MudDialogProvider|MudSnackbarProvider" .
```

Read effective package versions from `Directory.Packages.props` or referenced MSBuild properties. When available, `obj/project.assets.json` shows the resolved version actually used by the last successful restore.

Local-only commands:

```text
dotnet --info
dotnet --list-sdks
dotnet --list-runtimes
dotnet nuget locals global-packages --list
dotnet list <project.csproj> package --no-restore
```

Do not use `dotnet list package --outdated`, vulnerability/audit queries, or other commands that consult remote feeds.

## Inspect the installed MudBlazor package

The global packages folder is commonly:

- Windows: `%USERPROFILE%\.nuget\packages\mudblazor\<version>\`
- Linux/macOS: `~/.nuget/packages/mudblazor/<version>/`
- Custom: the `NUGET_PACKAGES` environment variable or the path printed by `dotnet nuget locals global-packages --list`

Look for:

- `lib/<tfm>/MudBlazor.xml`: documented types, parameters, methods, and enum members.
- `lib/<tfm>/MudBlazor.dll`: the exact compiled API.
- `build`, `buildTransitive`, `content`, `contentFiles`, and `staticwebassets`: package integration details.
- package README, license, source link metadata, or source files when included.

Search XML docs rather than relying on a remembered online example:

```text
rg -n "MudDataGrid|PropertyColumn|ServerData|MudDialog|DialogOptions" <package-folder>
```

XML member prefixes are useful:

- `T:` type
- `P:` property
- `M:` method
- `F:` field or enum member
- `E:` event

When XML docs are insufficient, inspect the assembly with an already-installed local tool or a tiny temporary reflection program that references the existing DLL. Do not add or download a decompiler. Keep temporary inspection artifacts outside production source and remove only artifacts you created.

For ASP.NET Core reference packs, render modes, lifecycle, platform forms, navigation, circuits, or JS interop, use `blazor-webapp-offline`.

## Evidence discipline

- Record the exact MudBlazor version and target framework used for decisions.
- Distinguish an unresolved API from a missing local package.
- A successful compilation is necessary evidence, not proof of visual behavior or correct user experience.
- Do not cite online version behavior as though it applies to the installed package.

