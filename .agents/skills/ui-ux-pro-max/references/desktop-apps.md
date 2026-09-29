# Desktop-oriented business applications

Desktop-first does not mean fixed-width or pointer-only. It means optimizing the primary wide-screen workflow while keeping constrained widths and keyboard operation coherent.

## Workspace design

- Give the main working object most of the viewport.
- Keep frequent controls available without forcing repeated modal trips.
- Use persistent context panes only when their information is needed during the task.
- Prefer predictable placement over novelty for repeated expert work.
- Preserve workspace state such as filters, selected item, expanded nodes, and pane size when doing so is reliable and not surprising.

Avoid marketing-page patterns—large hero areas, sparse centered columns, oversized headings—in operational screens where they displace useful content.

## Multi-pane workflows

For navigation/list/detail or tree/editor layouts, define:

- which pane owns selection;
- whether selecting changes route, preview, or edit context;
- how unsaved work behaves when selection changes;
- minimum useful pane sizes and overflow behavior;
- focus movement between panes;
- narrow-width fallback and return navigation.

Do not let resizing hide the only path to restore a pane. Keep current location and selected object visible.

## Information density

Increase density by removing redundant labels, chrome, and repeated explanations—not by shrinking text or targets beyond usability. Show more rows or fields only when users can still distinguish structure and state.

Offer a density preference only if users have materially different needs and the application can maintain both modes consistently. Do not add a setting to avoid making a sensible default.

## Large lists and long names

- Provide search/filter based on the way users identify objects.
- Preserve context when opening and returning from detail.
- Keep extensions, suffixes, versions, and identifiers visible when they disambiguate items.
- Let users inspect and copy full values.
- Avoid hover-only access to essential names.
- Use virtualization or paging only after choosing the navigation and selection model; performance mechanics must not erase context.

## Repeated expert work

- Keep action locations stable.
- Support efficient keyboard traversal and shortcuts when they do not conflict with standard behavior.
- Use safe defaults and remember low-risk preferences.
- Reduce confirmation fatigue; reserve blocking confirmation for real consequence.
- Allow batch operations with an explicit scope and result summary.
- Keep success feedback brief, but keep failures and partial results durable.

## Resilience in Interactive Server

The UX plan should account for latency, reconnect, and server-owned state without prescribing implementation:

- indicate when an action was accepted versus merely clicked;
- prevent duplicate execution across delayed feedback;
- preserve or restore the user's context after reconnect when supported;
- explain when an in-progress operation continues independently;
- do not promise offline editing unless the application actually supports it.

Use `blazor-webapp-offline` to implement circuit, cancellation, state, and reconnect behavior.

## Review

Test common workflows at normal desktop width and a constrained window, with long localized names, high data volume, keyboard-only input, slow responses, permission differences, and reconnect. Count avoidable modal transitions and repeated pointer travel in high-frequency tasks.
