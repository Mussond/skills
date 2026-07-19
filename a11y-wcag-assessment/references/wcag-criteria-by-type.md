# WCAG Criteria by Component Type

> **Status: Ready** — Type-to-criteria mapping tables for Step 2 of the conformance framework.
> These tables operate at one level of abstraction above the Quick Lookup table in SKILL.md.
> Use them to identify applicable criteria before knowing the exact component.
> Components can span multiple types — apply all relevant tables.

---

## How to use this file

1. Classify the component using Step 1 (interactive / informational / container / stateful) — a component may span multiple types
2. Load the table(s) for each type that applies
3. Every criterion in the table is applicable — none are conditional at this level
4. Proceed to Step 3 (Atomica11y) for component-level test checklists

Multi-type example: a Toggle is **interactive** (keyboard, focus, name) +
**stateful** (state must be programmatically exposed). Apply both tables.

---

## Interactive

Applies to: buttons, links, form fields, toggles, tabs, modals, menus, sliders,
accordions, date pickers, and any component the user operates.

| SC | Name | Level | Why it applies |
|----|------|-------|----------------|
| 1.4.3 | Contrast (Minimum) | AA | Text labels and visible names must meet contrast ratios |
| 1.4.11 | Non-text Contrast | AA | UI component boundaries must have 3:1 contrast against adjacent colours |
| 2.1.1 | Keyboard | A | All functionality must be operable by keyboard alone |
| 2.1.2 | No Keyboard Trap | A | Focus must not become trapped; user must be able to move away |
| 2.4.3 | Focus Order | A | Focus sequence must be logical and preserve meaning |
| 2.4.7 | Focus Visible | AA | Keyboard focus indicator must be visible |
| 2.4.11 | Focus Not Obscured (Minimum) | AA | Focused component must not be entirely hidden by sticky content |
| 2.5.3 | Label in Name | A | Visible label text must be contained in the accessible name |
| 2.5.8 | Target Size (Minimum) | AA | Touch/click target must be at least 24×24 CSS px |
| 3.2.1 | On Focus | A | Focus alone must not trigger unexpected context change |
| 3.2.2 | On Input | A | Input alone must not trigger unexpected context change |
| 4.1.2 | Name, Role, Value | A | All interactive elements need accessible name, role, and state exposed to AT |

**AAA worth surfacing:**
| 2.4.12 | Focus Not Obscured (Enhanced) | AAA | Focused component must not be partially hidden by sticky content |
| 2.4.13 | Focus Appearance | AAA | Focus indicator area, contrast, and thickness — strongly recommended |
| 2.5.5 | Target Size (Enhanced) | AAA | 44×44 CSS px — recommend for all touch targets |

---

## Informational

Applies to: headings, body text, images, icons, badges, tags, labels, status messages,
tooltips, and any component whose primary purpose is to convey information.

| SC | Name | Level | Why it applies |
|----|------|-------|----------------|
| 1.1.1 | Non-text Content | A | Images, icons, and non-text elements need text alternatives |
| 1.3.1 | Info and Relationships | A | Structure and relationships conveyed visually must be programmatically determinable |
| 1.3.3 | Sensory Characteristics | A | Instructions must not rely solely on shape, colour, size, or position |
| 1.4.1 | Use of Colour | A | Colour must not be the only means of conveying information |
| 1.4.3 | Contrast (Minimum) | AA | Text must meet minimum contrast ratios against its background |
| 1.4.4 | Resize Text | AA | Text must remain readable when resized to 200% without assistive tech |
| 1.4.5 | Images of Text | AA | Avoid images of text; use real text where possible |
| 1.4.10 | Reflow | AA | Content must not require horizontal scrolling at 320px viewport width |
| 1.4.12 | Text Spacing | AA | Content must not be lost when letter/word/line spacing is overridden |
| 4.1.3 | Status Messages | AA | Status messages must be programmatically determinable without receiving focus |

**AAA worth surfacing:**
| 1.4.6 | Contrast (Enhanced) | AAA | 7:1 ratio for normal text, 4.5:1 for large text |
| 1.4.9 | Images of Text (No Exception) | AAA | No images of text except for logos |

---

## Container

Applies to: cards, lists, navigation, tables, dialogs, panels, page regions, and any
component whose primary role is to group, organise, or provide structure for other content.

| SC | Name | Level | Why it applies |
|----|------|-------|----------------|
| 1.3.1 | Info and Relationships | A | Structural relationships (lists, tables, headings) must be programmatically exposed |
| 1.3.2 | Meaningful Sequence | A | Reading order must be logical when structure is linearised |
| 1.4.10 | Reflow | AA | Container must not break or lose content at 320px viewport width |
| 2.4.1 | Bypass Blocks | A | Repeated blocks of content must have a skip mechanism |
| 2.4.6 | Headings and Labels | AA | Headings and labels must be descriptive |
| 3.2.3 | Consistent Navigation | AA | Navigation repeated across pages must appear in the same order |
| 3.2.4 | Consistent Identification | AA | Components with the same function must be identified consistently |
| 4.1.2 | Name, Role, Value | A | Landmark regions, tables, and lists need appropriate roles exposed to AT |

**Note:** 2.4.1 (Bypass Blocks) applies at the page level; not relevant for individual
DS components unless they render a full navigation region.

---

## Stateful

Applies to: toggles, checkboxes, radio buttons, tabs, accordions, progress indicators,
loaders, steppers, and any component that has more than one programmatic state that
changes in response to user action or system events.

| SC | Name | Level | Why it applies |
|----|------|-------|----------------|
| 1.3.1 | Info and Relationships | A | State conveyed visually (e.g. checked, selected) must be programmatically determinable |
| 1.4.1 | Use of Colour | A | State changes must not be communicated by colour alone |
| 1.4.3 | Contrast (Minimum) | AA | Text in all states (default, hover, disabled, error) must meet contrast |
| 1.4.11 | Non-text Contrast | AA | State indicators (checkbox tick, toggle knob) must have 3:1 contrast |
| 3.3.1 | Error Identification | A | Error state must be described in text, not just by colour or icon |
| 3.3.2 | Labels or Instructions | A | Components requiring input must have visible labels or instructions |
| 4.1.2 | Name, Role, Value | A | Current state (aria-checked, aria-expanded, aria-selected, aria-pressed) must be programmatically exposed and updated when state changes |
| 4.1.3 | Status Messages | AA | Dynamic state changes that don't move focus must be announced via live region |

**Note:** The accessible name for a stateful component must reflect or not contradict
the current state. A toggle labelled "Dark mode" is fine; one labelled "On" is not —
the name changes when the state changes, which violates 4.1.2.

---

## Cross-type notes

Most DS components span multiple types. Common combinations:

| Component | Types |
|-----------|-------|
| Toggle / Switch | Interactive + Stateful |
| Checkbox / Radio | Interactive + Stateful |
| Tabs | Interactive + Stateful + Container |
| Accordion | Interactive + Stateful + Container |
| Modal / Dialog | Interactive + Container |
| Card | Informational + Container (+ Interactive if clickable) |
| Text Input | Interactive + Stateful (error, disabled, focused) |
| Alert / Toast | Informational + Stateful (live region, dynamic injection) |
| Navigation | Container + Interactive |
| Data Table | Container + Informational (+ Interactive if sortable) |
