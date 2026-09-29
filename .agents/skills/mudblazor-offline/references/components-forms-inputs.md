# Forms, Select, and TextField

Snapshot sources: official `/components/form`, `/components/select`, and `/components/textfield` documentation at repository commit `c0b219b`. Verify all signatures against the installed package.

## Choose one form model

MudBlazor supports both `MudForm` validation and standard Blazor `EditForm`/`EditContext` integration. Use one coherent owner of validation state per form.

Choose `EditForm` when the application already uses DataAnnotations, custom `ValidationMessageStore`, or a standard `EditContext`. Choose `MudForm` when component-level validation delegates and `MudForm` lifecycle methods match the project.

## MudForm

The snapshot documents `IsValid`, `Errors`, `ValidateAsync`, `ResetAsync`, `ResetValidationAsync`, enter-key validation, validation delegates, dirty-only validation, readonly/disabled form states, and form customization.

```razor
<MudForm @ref="_form" @bind-IsValid="_isValid" @bind-Errors="_errors">
    <MudTextField T="string"
                  @bind-Value="_model.Name"
                  Label="Name"
                  Required="true"
                  RequiredError="Name is required." />

    <MudTextField T="string"
                  @bind-Value="_model.Email"
                  Label="Email"
                  Required="true"
                  Validation="@ValidateEmail" />

    <MudButton ButtonType="ButtonType.Button"
               Variant="Variant.Filled"
               Color="Color.Primary"
               Disabled="@(!_isValid || _saving)"
               OnClick="SaveAsync">
        Save
    </MudButton>
</MudForm>

@code {
    private MudForm? _form;
    private bool _isValid;
    private bool _saving;
    private string[] _errors = [];
    private readonly ProductInput _model = new();

    private static string? ValidateEmail(string? value) =>
        string.IsNullOrWhiteSpace(value) || !value.Contains('@')
            ? "Enter a valid email address."
            : null;

    private async Task SaveAsync()
    {
        if (_form is null) return;
        await _form.ValidateAsync();
        if (!_form.IsValid) return;

        _saving = true;
        try { await ProductService.SaveAsync(_model); }
        finally { _saving = false; }
    }
}
```

The precise accepted validation delegate shapes are version-sensitive. Prefer an existing project pattern or inspect `MudFormComponent<T, string>` and the installed input XML docs.

## EditForm with MudBlazor inputs

Provide `For` expressions so inputs associate with the correct field and validation messages.

```razor
<EditForm Model="@_model" OnValidSubmit="SaveAsync">
    <DataAnnotationsValidator />

    <MudTextField @bind-Value="_model.Name"
                  For="@(() => _model.Name)"
                  Label="Name" />

    <MudTextField @bind-Value="_model.Email"
                  For="@(() => _model.Email)"
                  Label="Email" />

    <ValidationSummary />
    <MudButton ButtonType="ButtonType.Submit"
               Variant="Variant.Filled"
               Color="Color.Primary">
        Save
    </MudButton>
</EditForm>
```

Server validation is still authoritative. Map server errors back into the form state instead of discarding user input.

## MudSelect

Set `T` explicitly for nullable, enum, complex, or multi-select values.

```razor
<MudSelect T="Category?" @bind-Value="_category" Label="Category" Clearable="true">
    @foreach (var category in _categories)
    {
        <MudSelectItem T="Category?" Value="@category">@category.Name</MudSelectItem>
    }
</MudSelect>
```

For complex objects, equality and display conversion must be stable. Prefer binding an identifier when object instances may be reloaded. If binding the object, provide the supported comparer and `ToStringFunc`/converter pattern verified locally.

The snapshot's multi-select example uses `MultiSelection="true"` and binds `SelectedValues` as `IReadOnlyCollection<T>`:

```razor
<MudSelect T="string"
           Label="Regions"
           MultiSelection="true"
           @bind-SelectedValues="_regions">
    @foreach (var region in AllRegions)
    {
        <MudSelectItem T="string" Value="@region">@region</MudSelectItem>
    }
</MudSelect>

@code {
    private IReadOnlyCollection<string> _regions = ["North"];
}
```

Collection type and binding behavior are version-sensitive. Verify the installed `SelectedValues` and `SelectedValuesChanged` signatures. The official page also documents select-all behavior, custom selection text, custom conversion, dynamic sizing, numeric collections, popover placement, and keyboard navigation.

## MudTextField

The page documents text/filled/outlined variants, helper text, disabled/read-only states, clear button, styling, adornments, character counter, binding, nullables, input types, multiline fields, masks, programmatic control, and the lower-level `MudInput` building block.

```razor
<MudTextField T="string"
              @bind-Value="_query"
              Label="Search"
              Variant="Variant.Outlined"
              Immediate="true"
              DebounceInterval="300"
              OnDebounceIntervalElapsed="SearchAsync"
              Adornment="Adornment.End"
              AdornmentIcon="@Icons.Material.Filled.Search"
              Clearable="true" />
```

Update timing in the snapshot:

- With `Immediate="false"` and no debounce, the value normally updates on change/blur or Enter.
- With `Immediate="true"` and no debounce, it updates on input.
- A positive `DebounceInterval` delays notification until typing pauses and implies input-style updates in the snapshot.

Use cancellation or a monotonically increasing request identity for asynchronous search so stale results cannot replace newer results. For passwords, set the verified password `InputType`; never log or echo values. For numeric/date data, prefer the corresponding typed MudBlazor field rather than manually parsing a text field.

