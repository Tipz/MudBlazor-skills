# Tables, data grids, and large lists

Use a table or grid when users compare repeated records across attributes. Use a list when each item has a variable content structure or comparison by column is unimportant.

## Query behavior

- Make sorting direction and priority visible. Provide a stable default that matches the task.
- Distinguish quick search, structured filters, and column filters. Show active constraints and make reset predictable.
- Decide whether filtering is immediate, debounced, or explicitly applied based on query cost and user need.
- For large or server-backed data, keep sorting, filtering, totals, and paging consistent on the same authoritative result set.
- Cancel or ignore stale responses so older results cannot replace newer intent.

## Paging, virtualization, and scrolling

Choose deliberately:

- **Paging** supports known position, totals, return to a page, and bounded requests.
- **Virtualization** supports scanning long homogeneous data but complicates position, dynamic heights, and some interactions.
- **Incremental loading** is suitable when continuous discovery matters more than exact position.

Do not combine patterns without a clear model. Preserve filters, sort, page/position, and selection when users return if doing so is reliable.

## Selection and bulk actions

- Make selected rows distinguishable without color alone.
- State whether selection applies only to visible rows, the current filtered result, or all matching records.
- Keep bulk actions hidden or disabled until meaningful, but make selection capability discoverable.
- Show count and scope before a destructive batch action.
- Reconcile selection when data refreshes or filters change; never act on invisible stale selection silently.

## Row actions

Keep frequent, low-risk actions visible when space permits. Put rare actions in a consistently placed menu. Icon-only actions require clear accessible names and tooltips when the icon's meaning is not universal.

Do not make the whole row clickable if it contains other interactive controls unless keyboard and pointer behavior are unambiguous. Separate navigation from selection.

## Empty, loading, and error behavior

Distinguish:

- no data exists yet;
- no results match current filters;
- access is restricted;
- data failed to load;
- the next page or range is loading.

Keep table structure stable during ordinary reloads when possible. Provide retry near a load failure. Clearing filters is appropriate only for “no matches,” not an actually empty data set.

## Long values and overflow

- Assign width priority by task importance, not equal columns.
- Wrap human-readable descriptions when row-height growth is acceptable.
- Truncate scannable secondary text only when the full value is accessible.
- Preserve meaningful filename extensions and distinguishing suffixes.
- Use horizontal scrolling for essential wide comparison rather than hiding required columns.
- Keep frozen/sticky regions limited so they do not consume the viewport.
- Format numbers consistently and align them for comparison.

## Destructive actions

Name the affected row/object in confirmation when the action is consequential. After deletion, maintain a stable viewport, announce the result, and move focus predictably. For batch deletion, show the count and whether hidden selected rows are included.

## Review matrix

Test zero, one, and many rows; long/localized values; slow and failed queries; rapid filter changes; selection across paging/filtering; keyboard interaction; narrow width; destructive row and bulk actions; and return navigation with restored context.
