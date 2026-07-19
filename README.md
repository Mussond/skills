# skills

Repo for my skills that I'm testing or have created.

## Included skills

- **[rule-of-3](rule-of-3/)** — stress-tests a Figma component by tripling copy, functions, and content to surface translation, zoom, viewport, and use-case fragility before it ships.
- **[a11y-wcag-assessment](a11y-wcag-assessment/)** — diagnostic skill for assessing whether a component, pattern, or feature meets WCAG / EN 301 549 conformance.
- **[a11y-authoring](a11y-authoring/)** — takes a conformance verdict and produces Jira-ready acceptance criteria or consumer-facing usage documentation.

## Sources & citations

`a11y-wcag-assessment` bundles reference data derived from third-party sources:

- **AtomicA11y** (`references/atomica11y.md`, `criteria-web.json`, `criteria-ios.json`, `criteria-android.json`) — component-level accessibility checklists and test scenarios sourced from [atomica11y.com](https://www.atomica11y.com/). Content and software released under the [Apache License 2.0](https://www.atomica11y.com/about/), which permits reuse, modification, and redistribution.
- **axe-core** (`references/axe-rules.json`) — rule metadata (id, description, impact, WCAG/EN 301 549 mapping) derived from [axe-core](https://github.com/dequelabs/axe-core) by Deque Systems, Inc., licensed under [MPL-2.0](https://github.com/dequelabs/axe-core/blob/develop/LICENSE).

All other content (steps, formats, source hierarchy) is original.
