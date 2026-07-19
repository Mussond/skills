# skills

Repo for my skills that I'm testing or have created.

## Included skills

- **[rule-of-3](rule-of-3/)** — stress-tests a Figma component by tripling copy, functions, and content to surface translation, zoom, viewport, and use-case fragility before it ships.
- **[a11y-wcag-assessment](a11y-wcag-assessment/)** — diagnostic skill for assessing whether a component, pattern, or feature meets WCAG / EN 301 549 conformance.
- **[a11y-authoring](a11y-authoring/)** — takes a conformance verdict and produces Jira-ready acceptance criteria or consumer-facing usage documentation.

## License

Original content in this repo (skill steps, formats, source hierarchy, etc.) is licensed under the [Apache License 2.0](LICENSE). Third-party reference data bundled inside `a11y-wcag-assessment` retains its own original license, cited below, and is not covered by this repo's LICENSE.

## Sources & citations

`a11y-wcag-assessment` bundles reference data derived from third-party sources:

- **AtomicA11y** by [Charlie Triplett](https://www.atomica11y.com/about/) — component-level accessibility checklists and test scenarios sourced from [atomica11y.com](https://www.atomica11y.com/). Content and software released under the Apache License 2.0, which permits reuse, modification, and redistribution.
  - `references/criteria-web.json`, `criteria-ios.json`, `criteria-android.json` — used unmodified.
  - `references/atomica11y.md` — adapted from the source structure and lookup guidance; wording changed to remove personal references.
- **axe-core** by [Deque Systems, Inc.](https://github.com/dequelabs/axe-core) — rule metadata (id, description, impact, WCAG/EN 301 549 mapping) derived from `doc/rule-descriptions.md` in the axe-core repo, licensed under [MPL-2.0](https://github.com/dequelabs/axe-core/blob/develop/LICENSE).
  - `references/axe-rules.json` — restructured into a lookup table; values sourced from axe-core's rule documentation, not modified in meaning.

All other content (steps, formats, source hierarchy) is original.
