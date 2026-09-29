# Visual hierarchy and grouping

Use this reference to turn an inventory of UI content into a readable page structure. It covers presentation, not workflow behavior.

## Start from the task

Write one sentence that names the user's primary task on the screen. Then classify visible content:

- **Primary:** content and action required to complete that task.
- **Secondary:** context, filters, or supporting actions used regularly.
- **Tertiary:** metadata, rare actions, help, and diagnostics.

If everything appears primary, nothing is. Demote content before inventing more emphasis styles.

## Define the scanning path

For desktop business UI, a common path is page identity -> status/context -> working region -> primary action -> supporting detail. Use the actual task rather than forcing this pattern.

- Put page identity and current scope where they are found quickly.
- Keep the working region visually dominant through space and placement, not decoration alone.
- Place actions near the object they affect.
- Keep durable errors and blockers in the path between intent and action.
- Put metadata where it can be found without interrupting routine work.

Test by squinting at a screenshot or mentally removing the text. The largest, darkest, or most isolated shapes should correspond to real importance.

## Grouping tools, in preferred order

1. Proximity.
2. Shared alignment.
3. Whitespace.
4. Typography.
5. Subtle surface or divider.
6. Border or strong contrast only when a boundary is meaningful.

Avoid using a card as the default grouping primitive. A card is useful when a region is an independent object, has its own actions, or must remain distinct while rearranged. A section in a continuous form or detail page usually needs a heading and spacing, not another container.

## Emphasis budget

Reserve strong color and high contrast for a small number of meanings. Distinguish:

- page-level primary action;
- selected or current location;
- status or severity;
- interactive affordance;
- informational accent.

Do not use the same accent treatment for all five. Never rely on color alone to carry selection, error, or status.

## Actions

- Keep one obvious page-level primary action when the workflow has one.
- Style secondary actions with less weight but keep them discoverable.
- Place destructive actions away from routine confirmation paths.
- Group row actions consistently and keep the highest-frequency action easiest to reach.
- Do not turn every text link into a filled button.

## Review questions

- Can a first-time user identify the page, current scope, and main task in a few seconds?
- Does visual prominence match business importance rather than implementation order?
- Are related items closer to each other than to unrelated items?
- Can repeated objects be compared without decorative noise?
- Does the layout still make sense with a long title, a validation error, and an empty or loading region?
