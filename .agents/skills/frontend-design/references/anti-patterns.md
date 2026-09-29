# Visual anti-patterns and critique

Use this as a diagnostic checklist. A listed treatment is not forbidden when the product context gives it a clear purpose; unexplained repetition is the problem.

## Container inflation

Symptoms:

- every section is a card or `MudPaper`;
- card inside card inside a page surface;
- border, shadow, and tinted background all express the same boundary;
- a dashboard is a uniform grid of unrelated tiles.

Correction: remove one layer at a time. Rebuild grouping with proximity, alignment, headings, and a single meaningful boundary.

## Competing emphasis

Symptoms:

- several filled primary buttons in one decision area;
- accent color applied to headings, icons, badges, links, and decoration alike;
- every number is oversized;
- destructive and routine actions have equal visual weight.

Correction: name the primary task and reserve the strongest treatment for it. Assign distinct, restrained treatments to selection, status, navigation, and danger.

## Generic AI dashboard appearance

Common tells:

- interchangeable rounded statistic cards;
- gratuitous gradient washes or glowing accents;
- oversized welcome or hero copy above operational data;
- excessive pills, rounded rectangles, and soft shadows;
- icon bubbles attached to every heading;
- decorative charts without comparison or action value;
- equal spacing and weight for content of unequal importance.

Correction: use the application's domain, actual decisions, and real data shape. Let content determine composition. Remove styling that could be pasted unchanged into an unrelated product.

## Density mismatch

Symptoms:

- large vertical gaps in a frequent desktop workflow;
- narrow centered content surrounded by unused workspace;
- tiny crowded targets in an occasional high-risk task;
- tables padded like marketing cards;
- explanatory copy repeated beside familiar controls.

Correction: choose density from frequency, risk, expertise, and data volume. Preserve minimum readability and interaction targets while removing redundant chrome.

## Alignment and rhythm drift

Symptoms:

- headings, fields, and tables start on almost—but not exactly—the same edge;
- toolbars mix baselines and control heights;
- spacing values change without meaning;
- wrapped content breaks row or card rhythm;
- controls appear centered between groups.

Correction: identify dominant edges and a spacing scale. Test with the longest realistic values rather than only ideal sample content.

## Decorative semantics

Symptoms:

- icons without a recognizable meaning or accessible name;
- borders or colors that look like status but carry no status;
- numbered labels on content that is not sequential;
- disabled-looking muted text that is actually interactive;
- gradients or animation used to make ordinary content seem important.

Correction: every strong visual device should explain structure, state, affordance, or priority. Remove it if it does not.

## Final critique pass

1. Describe the page's visual hierarchy in one sentence. If that is difficult, simplify it.
2. Count the distinct surface, radius, shadow, accent, and heading treatments. Merge unexplained variants.
3. Remove one decorative layer and check whether comprehension worsens. Keep it removed if not.
4. Check realistic empty, loading, error, long-text, and selected states.
5. Compare with adjacent application screens; preserve deliberate differences and fix accidental ones.
6. Verify narrow-width reflow, keyboard focus visibility, and readable contrast.
7. Record any rendered visual review that could not be performed.
