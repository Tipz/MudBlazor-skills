# Layout and composition patterns

Choose a composition from task structure, not from a component gallery. These are starting points, not templates.

## Operational list or data page

Typical visual order:

1. compact page identity and current scope;
2. primary action and frequent filters;
3. active-filter or selection context;
4. dominant list/grid region;
5. paging, totals, or batch feedback.

Let the data region use the available workspace. Keep rare filters in a secondary area if the always-visible toolbar becomes crowded. Avoid surrounding the grid with multiple nested surfaces.

## Form or editor

Use one strong reading direction. Group fields by meaning and task sequence, not by database table. A desktop form may use columns for short independent fields, but preserve a predictable order when it reflows.

- Keep labels and controls aligned.
- Constrain fields to sensible widths.
- Use section headings and whitespace before cards.
- Keep save/cancel placement stable and visible without duplicating competing action bars.
- Reserve side panels for context that benefits from staying visible.

Interaction details such as validation and unsaved changes belong to `ui-ux-pro-max`.

## Detail page

Put identity, status, and frequent actions first. Separate summary facts from history, related entities, and diagnostics. Use definition-like alignment for comparable facts. Do not render each fact as a metric card.

## Dashboard

A dashboard is a decision surface, not a collection of equal tiles.

- Start with the decisions or exceptions the user must act on.
- Give the most consequential region more space.
- Group related measures and provide comparison context.
- Prefer a useful table or trend over decorative summary cards when detail drives action.
- Vary composition only when importance or content type varies; avoid arbitrary masonry.

## Master-detail and hierarchical workspace

Keep location and selection visible. The navigation/list pane should be wide enough for realistic names but must not consume the working area. Use a clear divider or surface change at the pane boundary, not a card around every node and panel.

When narrow, decide which region becomes primary, how the user returns, and what context remains visible. Do not simply squeeze both panes.

## Dialog composition

Use dialogs for bounded decisions or focused short tasks, not as a default page container. Keep title, consequence, content, and actions visually distinct. Long or deeply nested work usually deserves a page or side workspace.

## Responsive considerations

Plan responsive behavior by priority:

- what must remain visible;
- what may wrap;
- what may move below;
- what may collapse behind a labeled control;
- what needs horizontal scrolling rather than destructive truncation;
- what becomes a different navigation step.

Test at least a wide desktop, constrained desktop/tablet width, and the narrowest supported width. Preserve logical reading and keyboard order when regions move. Do not require identical composition at every width.
