# Section naming + layout convention

Keep runs predictable so anyone can spot a Rule-of-3 region in a file and clean it up without thinking.

## Section names

Exactly three top-level Figma Sections per run, in this order:

1. `Rule of 3 — Copy`
2. `Rule of 3 — Functions`
3. `Rule of 3 — Content`

Use the em-dash (`—`), not a hyphen. Match the casing.

If a prior run's Sections already exist in the file, **timestamp** the new run rather than overwriting:

```
Rule of 3 — Copy (2026-05-17 14:32)
Rule of 3 — Functions (2026-05-17 14:32)
Rule of 3 — Content (2026-05-17 14:32)
```

Timestamp format: `YYYY-MM-DD HH:mm` in the user's local time.

## Placement

- Position the three Sections **to the right of the source component**, stacked vertically.
- Leave a `200px` gap from the source component on the left edge.
- Leave a `120px` gap between each Section.
- Section width: enough to fit ~3 instances per row of the largest curated variant, with `64px` padding inside.

## Inside each Section

- Instances laid out in a wrap-friendly grid: `auto-layout`, horizontal, with wrap enabled, gap `48px`, padding `64px`.
- One instance per curated variant × boolean combo.
- Each instance gets a small label (text node above it) showing the variant + boolean values, e.g. `size=lg, state=disabled, hasIcon=true`.

## Visual styling

Don't restyle the Section background unless the file has a convention — Figma's default Section style is fine. The point is identifiability through name + position, not visual chrome.

## Cleanup contract

Because all writes live inside these three named Sections, the cleanup instruction is always the same one line:

> Select the three `Rule of 3 — …` Sections and delete them.

No residual nodes should exist anywhere else in the file.
