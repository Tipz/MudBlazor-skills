# MudTable

Snapshot source: official `/components/table` documentation at repository commit `c0b219b`. Verify all signatures against the installed package.

## When to use

Use `MudTable<T>` for a template-driven table with explicit header and row markup, responsive breakpoint behavior, paging, sorting, selection, grouping, or server loading. Use `MudDataGrid<T>` when column-centric filtering/editing/grouping and richer grid state are the primary requirement. Use a plain/simple table when no component logic is needed.

## Basic responsive table

```razor
<MudTable T="Product"
          Items="@_products"
          Hover="true"
          Breakpoint="Breakpoint.Sm"
          Loading="@_loading"
          LoadingProgressColor="Color.Info">
    <HeaderContent>
        <MudTh>Name</MudTh>
        <MudTh>Price</MudTh>
        <MudTh>Stock</MudTh>
    </HeaderContent>
    <RowTemplate>
        <MudTd DataLabel="Name">@context.Name</MudTd>
        <MudTd DataLabel="Price">@context.Price.ToString("C2")</MudTd>
        <MudTd DataLabel="Stock">@context.Stock</MudTd>
    </RowTemplate>
    <NoRecordsContent>
        <MudText>No products found.</MudText>
    </NoRecordsContent>
    <LoadingContent>
        <MudText>Loading products…</MudText>
    </LoadingContent>
</MudTable>
```

`DataLabel` supplies the responsive label used when rows collapse at the configured breakpoint. Keep it aligned with the visible column heading.

## Sorting, paging, and selection

- Put `MudTableSortLabel` in header cells and give server-backed columns stable, explicitly mapped `SortLabel` values.
- Add `MudTablePager` in `PagerContent` for paging.
- For multi-selection of custom records, use stable equality or the comparer supported by the local version.
- Row click/hover callbacks can support selection or secondary UI, but preserve keyboard-accessible actions; do not make the row the only way to invoke a critical operation.

## Server data with cancellation

The snapshot's cancellable overload accepts `TableState` and `CancellationToken` and returns `Task<TableData<T>>`.

```razor
<MudTable T="Product" ServerData="LoadProductsAsync" Dense="true" Hover="true">
    <HeaderContent>
        <MudTh><MudTableSortLabel T="Product" SortLabel="name">Name</MudTableSortLabel></MudTh>
        <MudTh><MudTableSortLabel T="Product" SortLabel="price">Price</MudTableSortLabel></MudTh>
    </HeaderContent>
    <RowTemplate>
        <MudTd DataLabel="Name">@context.Name</MudTd>
        <MudTd DataLabel="Price">@context.Price.ToString("C2")</MudTd>
    </RowTemplate>
    <NoRecordsContent><MudText>No matching records.</MudText></NoRecordsContent>
    <LoadingContent><MudText>Loading…</MudText></LoadingContent>
    <PagerContent><MudTablePager /></PagerContent>
</MudTable>

@code {
    private async Task<TableData<Product>> LoadProductsAsync(
        TableState state,
        CancellationToken cancellationToken)
    {
        var request = new ProductQuery(
            Page: state.Page,
            PageSize: state.PageSize,
            Sort: MapAllowedSort(state.SortLabel, state.SortDirection));

        var result = await ProductService.QueryAsync(request, cancellationToken);
        return new TableData<Product>
        {
            Items = result.Items,
            TotalItems = result.TotalCount
        };
    }
}
```

The page index is zero-based in the snapshot examples. Filter before counting; return the filtered total, not page length. Pass the cancellation token through to database/HTTP operations.

## Editing and grouping

The snapshot includes inline edit mode, basic and multi-level grouping, and initially collapsed groups. Verify edit trigger, commit/cancel callbacks, and group definition types locally. Edit an isolated copy when cancel must be lossless, validate before persistence, and handle concurrency conflicts explicitly.

## Fixed layout, horizontal scrolling, and virtualization

Fixed headers/footers require a constrained scrolling container. Horizontal scrolling and fixed/sticky behavior interact with width and ancestor overflow. Virtualization requires stable row sizing and is useful only for sufficiently large collections. Inspect the generated UI locally before adding CSS overrides.

## Accessibility

Give the table an accessible label using the locally supported attributes. Keep header meaning, row actions, focus behavior, and responsive `DataLabel` text coherent. The snapshot includes a dedicated ARIA-label example and programmatic scroll/focus behavior; verify the exact API before using them.

