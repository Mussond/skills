# Design System References

> **Status: Ready** — Active reference list for usage documentation style.
> Referenced by Step 2B of the `a11y-authoring` skill alongside `references/usage-docs-format.md`.
> This is a curated shortlist — not a completeness exercise.
> Add new entries when a system's documentation style is genuinely worth referencing.

---

## GOV.UK Design System

**URL:** https://design-system.service.gov.uk/
**Accessibility docs:** https://design-system.service.gov.uk/accessibility/

### What to reference
- **Section structure:** Leads with what the component handles automatically, then what the
  consumer must provide. Clean separation of built-in vs consumer responsibility.
- **Tone:** Plain language, directive without being prescriptive. Instructions are short and
  scannable. No hedging.
- **Research evidence:** Usage guidance is grounded in user research. Worth noting where
  recommendations are evidence-based vs convention.
- **Known limitations:** GOV.UK documents where components don't meet their own standard
  and why. Good model for honest known-limitations sections.

### What to avoid from this system
- Some component pages mix design rationale with usage guidance — keep those concerns separate
  in your own docs.

---

## Carbon (IBM)

**URL:** https://carbondesignsystem.com/
**Accessibility docs:** https://carbondesignsystem.com/guidelines/accessibility/overview/

### What to reference
- **Keyboard interaction tables:** Carbon documents focus order, keyboard shortcuts, and
  expected behaviour in compact, scannable tables. Good model for that section.
- **Accessibility section structure:** Separates keyboard, screen reader, and ARIA attribute
  guidance into distinct subsections. Avoids conflating input modality with output behaviour.
- **Related WCAG criteria listing:** Carbon links applicable SCs at the end of component
  pages — good placement and level of detail.

### What to avoid from this system
- Accessibility guidance is sometimes buried several clicks from the component overview.
  In the audit docs, accessibility content should be a first-class section, not a sub-tab.

---

## Adding entries

Each entry needs:
- System name + URL + direct link to accessibility/usage docs
- What to reference from it (specific, not generic — e.g. "keyboard tables" not "good docs")
- What to avoid from it (anti-patterns or structural choices not to replicate)
