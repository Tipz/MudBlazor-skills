# Dialog, Button, and Snackbar

Snapshot sources: official `/components/dialog`, `/components/button`, and `/components/snackbar` documentation at repository commit `c0b219b`. Verify all signatures against the installed package.

## Dialog prerequisites

Dialogs require MudBlazor service registration and `MudDialogProvider` inside the correct interactive render boundary. If a dialog does not appear, check registration, provider placement, interactivity, and overlay/stacking contexts before changing dialog code.

## Open and implement a dialog

The snapshot uses async dialog APIs:

```razor
@inject IDialogService DialogService

<MudButton Variant="Variant.Filled" Color="Color.Primary" OnClick="OpenAsync">
    Edit product
</MudButton>

@code {
    private async Task OpenAsync()
    {
        var parameters = new DialogParameters<EditProductDialog>
        {
            { x => x.ProductId, ProductId }
        };

        var options = new DialogOptions { CloseOnEscapeKey = true };
        var reference = await DialogService.ShowAsync<EditProductDialog>(
            "Edit product", parameters, options);
        var result = await reference.Result;

        if (result is { Canceled: false })
            await ReloadAsync();
    }
}
```

Dialog component:

```razor
<MudDialog>
    <TitleContent>Edit product</TitleContent>
    <DialogContent>
        <MudTextField @bind-Value="_name" Label="Name" Required="true" />
    </DialogContent>
    <DialogActions>
        <MudButton OnClick="Cancel">Cancel</MudButton>
        <MudButton Color="Color.Primary" OnClick="SaveAsync">Save</MudButton>
    </DialogActions>
</MudDialog>

@code {
    [CascadingParameter]
    private IMudDialogInstance Dialog { get; set; } = default!;

    [Parameter]
    public Guid ProductId { get; set; }

    private string? _name;

    private void Cancel() => Dialog.Cancel();

    private async Task SaveAsync()
    {
        await ProductService.UpdateNameAsync(ProductId, _name!);
        Dialog.Close(DialogResult.Ok(ProductId));
    }
}
```

Typed `DialogParameters<TDialog>` provides expression-based parameter names in the snapshot. Verify `Result` nullability and `DialogResult` API for the installed version. Treat cancel/dismiss separately from confirmation. Keep persistence errors visible and keep the dialog open when the user can correct them.

The official page also documents global and per-dialog options, changing options from inside a dialog, templating and data passing, scrolling, inline and nested dialogs, cancel-all behavior, focus trap, keyboard accessibility, blurry background, and custom styling.

## Buttons

The page documents `Filled`, `Text`, and `Outlined` variants, elevation/drop shadow, size, full width, start/end icons, icon sizing, loading composition, split buttons, styling, and link buttons.

For an asynchronous command, disable repeated submission and expose progress:

```razor
<MudButton Variant="Variant.Filled"
           Color="Color.Primary"
           Disabled="@_processing"
           OnClick="ProcessAsync">
    @if (_processing)
    {
        <MudProgressCircular Size="Size.Small" Indeterminate="true" Class="me-2" />
        <span>Processing…</span>
    }
    else
    {
        <span>Process</span>
    }
</MudButton>
```

Use `ButtonType.Submit` inside a form only for actual submission; use `ButtonType.Button` for other actions where the installed version requires an explicit type. Icon-only actions should normally use the appropriate icon button with an accessible name.

When `Href` is set, `MudButton` renders link behavior. In the snapshot, `Target="_blank"` automatically adds `rel="noopener"`; an explicit `Rel` overrides automatic content, so include `noopener` yourself if still required. A disabled link button renders without `href` in the documented behavior.

## Snackbar prerequisites and usage

Snackbars require `ISnackbar` and `MudSnackbarProvider`.

```razor
@inject ISnackbar Snackbar

<MudButton OnClick="SaveAsync">Save</MudButton>

@code {
    private async Task SaveAsync()
    {
        await ProductService.SaveAsync();
        Snackbar.Add("Product saved.", Severity.Success);
    }
}
```

Use snackbars for transient status. Use an alert or persistent page/form message when the user must read, copy, or act on the error.

## Snackbar configuration and actions

The snapshot allows global configuration during `AddMudServices` and per-snackbar options:

```csharp
builder.Services.AddMudServices(configuration =>
{
    configuration.SnackbarConfiguration.PositionClass =
        Defaults.Classes.Position.BottomRight;
    configuration.SnackbarConfiguration.ShowCloseIcon = true;
    configuration.SnackbarConfiguration.PreventDuplicates = true;
    configuration.SnackbarConfiguration.NewestOnTop = true;
    configuration.SnackbarConfiguration.VisibleStateDuration = 5000;
    configuration.SnackbarConfiguration.SnackbarVariant = Variant.Filled;
});
```

```csharp
Snackbar.Add("Connection lost.", Severity.Warning, options =>
{
    options.Action = "Retry";
    options.RequireInteraction = true;
    options.OnClick = async _ => await RetryAsync();
});
```

Verify callback and option types locally. The page also documents position, variants, close-after-navigation, close callbacks, icons, programmatic `Remove`, `RemoveByKey`, render-fragment/custom-component messages, and duplicate prevention by message or explicit key.

Rendering a `MarkupString` as snackbar content bypasses normal HTML encoding. Use it only with trusted, sanitized markup; never insert raw user or server-provided HTML.

