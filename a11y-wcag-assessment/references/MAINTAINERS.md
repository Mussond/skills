---
name: a11y-wcag-assessment-maintainers
metadata:
  version: 1.0.0
description: >
  Maintainer-facing notes for the a11y-wcag-assessment skill. Not loaded during an assessment run.
  Holds the reference file status table, source-addition procedure, and curated external URLs.
---

# Maintainers — a11y-wcag-assessment

Off-load-path reference material. SKILL.md doesn't load this; only consult when extending or auditing the skill itself.

## Reference files

Reference files live in `references/`. Current state:

| File | Status | Purpose |
|------|--------|---------|
| `references/atomica11y.md` | Ready | Full Atomica11y component index + URL patterns |
| `references/wcag-criteria-by-type.md` | Ready | Step 2 criteria tables, expandable over time |
| `references/en301549-delta.md` | Planned | EN 301 549 clauses beyond WCAG 2.1 AA |
| `references/best-practice-sources.md` | Planned | Curated articles and test guides |
| `references/component-patterns.md` | Planned | ARIA APG patterns per component |
| `references/axe-rules.json` | Ready | axe-core 4.11 rule index — id, description, impact, WCAG SC mapping, EN 301 549 refs, issue type, enabled_default. Web only. Refresh on each axe-core minor release (~every 3–5 months). |
| `references/changelog.json` | Ready | Full version history for SKILL.md. |

Historical note: `ac-format.md`, `usage-docs-format.md`, `ds-references.md` moved to `a11y-authoring` skill. `axe-rules-v2.json` idea retired — folded into Step 3b.2 execution against existing `axe-rules.json` catalogue.

## Adding a new source

1. Create the file in `references/`.
2. Add a row to the table above.
3. Reference it from the relevant step in SKILL.md.

## Key external references

- WCAG 2.2 full spec: https://www.w3.org/TR/WCAG22/
- WCAG 2.2 Quick Reference: https://www.w3.org/WAI/WCAG22/quickref/
- Understanding WCAG 2.2: https://www.w3.org/WAI/WCAG22/Understanding/
- ARIA Authoring Practices Guide: https://www.w3.org/WAI/ARIA/apg/
- Atomica11y: https://www.atomica11y.com/
- A11Y Project Checklist: https://www.a11yproject.com/checklist/
- axe Rules: https://dequeuniversity.com/rules/axe/
- EN 301 549 (2021): https://www.etsi.org/deliver/etsi_en/301500_302000/301549/03.02.01_60/en_301549v030201p.pdf
