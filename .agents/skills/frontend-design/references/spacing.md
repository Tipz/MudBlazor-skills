# Spacing, alignment, and density

Use spacing to communicate relationship. Do not treat it as empty decoration.

## Establish a rhythm

Derive a small spacing scale from the existing application or theme. Reuse a few steps for:

- inline icon/text gaps;
- label/control gaps;
- related control gaps;
- section-internal spacing;
- separation between major regions;
- page edges and shell gutters.

The exact unit matters less than repeatability. Avoid isolated values introduced to fix one screenshot unless the exception has a structural reason.

## Relationship rule

Space inside a group should normally be smaller than space between groups. Apply this recursively:

- label to field < field to next field group;
- heading to its content < one section to the next;
- value to its unit < one metric to another;
- row content gaps < separation between table and surrounding controls.

When the relationship is unclear, adjust spacing before adding a border or background.

## Alignment

- Choose a dominant alignment edge for each region and honor it.
- Align labels, values, and actions to support comparison.
- Keep toolbar controls on a shared baseline when their heights differ.
- Avoid controls that appear to float between two sections.
- Use numeric alignment and consistent formatting for comparable values.
- Center alignment is suitable for brief, exceptional states; it is usually poor for forms, dense lists, and long text.

## Density modes

Choose density from context rather than taste:

- **Compact:** repeated expert workflows, data comparison, large lists, constrained desktop workspaces.
- **Comfortable:** mixed-frequency business tasks, ordinary forms, settings, and detail views.
- **Spacious:** first-run guidance, small decision sets, or content intended for slower reading.

Do not make touch targets or focus indicators unusably small in compact layouts. Compact means reducing redundant chrome and whitespace, not hiding labels or merging unrelated controls.

## Whitespace

Whitespace should clarify the structure or give a dominant region room. Large unused areas are suspicious in a desktop application when the user needs more rows, columns, or context. Conversely, edge-to-edge density without section breaks increases search cost.

Use available width intentionally:

- constrain long-form reading and forms that become hard to scan when stretched;
- allow data grids, comparison views, and editors to use width;
- avoid a narrow centered column for a desktop workflow with abundant horizontal information;
- do not stretch short controls merely because the container is wide.

## Review

Inspect repeated gaps rather than individual coordinates. Look for near-matches that feel accidental, uneven page gutters, headings detached from their content, wrapped actions, and sudden density changes between adjacent regions.
