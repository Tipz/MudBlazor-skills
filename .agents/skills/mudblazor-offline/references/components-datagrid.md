# MudDataGrid

Snapshot source: official `/components/datagrid` documentation at repository commit `c0b219b`. Verify all signatures against the installed package.

## Choose and declare columns

Use `MudDataGrid<T>` when the UI needs grid behavior such as column filtering, grouping, aggregation, reordering, resizing, rich editing, or server-driven grid state. For a simpler template-driven responsive table, consider `MudTable<T>`.

`PropertyColumn` binds a typed expression and can infer property metadata. `TemplateColumn` is appropriate for actions or computed content; it cannot infer all title/sort behavior, so specify what the scenario needs.

```razor
<MudDataGrid T="Product" Items="@_products" Hover="true">
    <Columns>
        <PropertyColumn Property="x => x.Id" Title="ID" />
        <PropertyColumn Property="x => x.Name" Title="Name" />
        <PropertyColumn Property="x => x.Price" Title="Price" Format="C2" />
        <TemplateColumn Title="Actions" Sortable="false" Filterable="false">
            <CellTemplate>
                <MudIconButton Icon="@Icons.Material.Filled.Edit"
                               aria-label="Edit product"
                               OnClick="@(() => EditAsync(context.Item))" />
            </CellTemplate>
        </TemplateColumn>
    </Columns>
</MudDataGrid>
```

Confirm whether arbitrary attributes such as `aria-label` are captured by the locally installed component; the current snapshot also documents table-level accessibility attributes.

## Sorting and filtering

- Grid `SortMode` controls none, single-column, or multi-column sorting. Individual columns can opt out with `Sortable="false"`.
- `QuickFilter` performs a global in-memory predicate over items.
- Column filtering supports multiple filter modes and templates in the current snapshot.
- A `TemplateColumn` generally needs an explicit `SortBy` to become meaningfully sortable.
- For a complex `Property` expression, server-side sort identity may not be a simple model property name. Map accepted identifiers explicitly rather than reflecting arbitrary client input.
- Changing sort mode at runtime may reset existing sort order in the snapshot behavior.

## Selection

Single and multi-selection can be bound through the API exposed by the installed version. For custom objects in multi-selection, equality must be stable: override `Equals`/`GetHashCode` or provide the supported comparer. Do not assume reference equality will survive reloads.

## Editing

The snapshot documents `ReadOnly="false"` plus three `DataGridEditMode` values:

- `Form`: edits a copy in a dialog-like form.
- `Cell`: keeps cells directly editable.
- `Inline`: manually starts one editable row at a time.

Version-sensitive callbacks in the snapshot include `StartedEditingItem`, `FormFieldChanged`, `CommittedItemChanges`, `CommittedItemChanged`, and `CanceledEditingItem`. Verify their exact delegate types locally.

Use `EditTemplate` for custom editors. A failed field validation should keep the row/form open. Perform uniqueness or server validation before accepting a commit. Use an edit copy when cancellation must restore the original item.

Do not persist directly from an unguarded UI callback. Disable or serialize duplicate commits, authorize the operation server-side, and handle optimistic concurrency.

## Server data

In the snapshot, `ServerData` receives `GridState<T>` and `CancellationToken`, and returns `Task<GridData<T>>`.

```razor
<MudDataGrid T="Product" @ref="_grid"
             ServerData="LoadProductsAsync"
             Filterable="false">
    <ToolBarContent>
        <MudText Typo="Typo.h6">Products</MudText>
        <MudSpacer />
        <MudTextField T="string"
                      ValueChanged="SearchAsync"
                      Placeholder="Search"
                      Adornment="Adornment.Start"
                      AdornmentIcon="@Icons.Material.Filled.Search" />
    </ToolBarContent>
    <Columns>
        <PropertyColumn Property="x => x.Id" Title="ID" />
        <PropertyColumn Property="x => x.Name" Title="Name" />
        <PropertyColumn Property="x => x.Price" Title="Price" Format="C2" />
    </Columns>
    <PagerContent>
        <MudDataGridPager T="Product" />
    </PagerContent>
</MudDataGrid>

@code {
    private MudDataGrid<Product>? _grid;
    private string? _search;

    private async Task<GridData<Product>> LoadProductsAsync(
        GridState<Product> state,
        CancellationToken cancellationToken)
    {
        var request = new ProductQuery(
            Search: _search,
            Page: state.Page,
            PageSize: state.PageSize,
            Sorts: MapAllowedSorts(state.SortDefinitions));

        var result = await ProductService.QueryAsync(request, cancellationToken);
        return new GridData<Product>
        {
            Items = result.Items,
            TotalItems = result.TotalCount
        };
    }

    private async Task SearchAsync(string? value)
    {
        _search = value;
        if (_grid is not null)
            await _grid.ReloadServerData();
    }
}
```

Treat `state.Page` as zero-based in this snapshot. Apply filter before calculating `TotalItems`, then page the filtered query. Whitelist sort mappings; never concatenate an untrusted sort name into SQL. Pass the cancellation token through every supported async operation.

## Virtualization and large data

The snapshot documents both local virtualization and virtualized server data. Virtualization is not interchangeable with paging: it assumes layout/item-size behavior and requests ranges as the user scrolls. Verify constraints in the installed version, use stable item identity, and do not combine features that local docs/API mark incompatible.

## Styling and accessibility

Prefer grid/column style hooks such as row, cell, header, and footer class/style functions over selectors tied to internal markup. Keep functions cheap because they run during rendering. Supply a meaningful table label and preserve keyboard behavior for interactive cell content.

