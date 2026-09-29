# Navigation and hierarchical information

Navigation should answer three questions: where am I, what is nearby, and how do I return or move onward?

## Information architecture

- Organize around user concepts and tasks rather than service, database, or code boundaries.
- Keep labels stable across navigation, page titles, dialogs, and action feedback.
- Separate global destinations, contextual destinations, and actions. Do not disguise an action as navigation.
- Avoid duplicate paths to the same concept unless each path reflects a real user context.
- Keep depth proportional to the domain. Do not flatten a meaningful hierarchy merely to reduce clicks.

## Current location

Show the selected destination and page identity. For deep hierarchy, expose enough ancestry to orient the user without repeating the entire tree. Preserve useful return context such as the previous filter or selected parent when navigation semantics allow it.

Browser back/forward and direct links should behave predictably for durable locations. Temporary UI such as an open menu usually should not become a route; a selected entity or tab may deserve one when users need sharing or restoration.

## Tree navigation

Define these behaviors before choosing a tree component:

- whether selection navigates, previews, or merely marks a node;
- whether expansion and selection are independent;
- whether a parent is selectable;
- initial expansion and restoration rules;
- keyboard movement, expansion, collapse, and activation;
- loading and failure of lazy children;
- behavior after rename, move, or deletion.

Keep the selected node visible. After deletion, choose a predictable adjacent or parent node and move focus there. Do not collapse unrelated branches after refresh.

## Deep nesting and long names

- Indentation must show depth without consuming the entire label width.
- Provide access to the full node name; a tooltip alone is insufficient for frequently needed values or touch use.
- Keep action controls from covering the label.
- Consider search/filter that reveals matching nodes with ancestry when the tree is large.
- For extreme depth, supplement the tree with breadcrumbs, a path display, or a focused drill-down view.

## Nested sections within a page

Use headings and a local navigation mechanism only when the page is genuinely long or structurally complex. Keep section names synchronized with headings. When content is loaded or validation jumps to a section, place focus and scroll position deliberately.

## Navigation review

Test direct entry, refresh, back/forward, deep links, permission changes, long labels, empty branches, lazy-load failure, keyboard-only traversal, and restoration after returning from a detail/edit screen.
