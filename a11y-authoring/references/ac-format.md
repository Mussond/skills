# Acceptance Criteria Format

> **Status: Ready** — Format spec for Jira-ready accessibility acceptance criteria.
> Referenced by Step 2A of the `a11y-authoring` skill.
> Derived from real NotificationCard AC output (March 2026).

---

## Grouping

Always three groups, in this order:
1. **Critical** — Level A failures if not met
2. **High** — Level AA requirements
3. **Recommended** — AAA / usage constraints worth surfacing

Group labels in output:
- "Critical — Level A failures if not met"
- "High — Level AA requirements"
- "Recommended — AAA / usage constraints"

---

## Per-AC structure

Each AC has five elements. Order is fixed:

### 1. Badges (header row)
Always in this order: Level badge | WCAG SC badge | Priority badge

Level badge values and colours:
- "Level A"   → red bg  (#fdecea) / red text  (#9b2c2c)
- "Level AA"  → amber bg (#fef3e2) / amber text (#92400e)
- "AAA rec"   → green bg (#eaf5ea) / green text (#276221)

WCAG SC badge: always grey (#f0efe9 / #5a5a55). Format: SC number only, e.g. "4.1.2".
Do not include the SC name in the badge — it goes in the title or body.

Priority badge values and colours (matches Level badge colour for Critical/High):
- "Critical" → red   (#fdecea / #9b2c2c)
- "High"     → amber (#fef3e2 / #92400e)
AAA recs omit the priority badge — the Level badge ("AAA rec") is sufficient.

### 2. Title
Short imperative statement of the requirement. Sentence case. No full stop.
Examples: "Close button has an accessible name" / "Alert role only fires on dynamic injection"
Aim for under 10 words. The title is what appears in the copy-to-clipboard output.

### 3. Body
Plain English. Explains what the requirement is and what fails if not met.
Include inline `code` for ARIA attributes, role names, and prop values.
Multiple `<p>` elements are fine for complex ACs. Keep it tight — 3–5 sentences max.
No bullet lists in the body — use em-dash (—) for inline lists if needed.

### 4. Gherkin
GIVEN / WHEN / THEN / AND format. Keywords are bold and muted (#5a5a55).
One scenario per AC. Do not write multiple scenarios — keep it to the primary test path.

Language conventions:
- Use "I HEAR" for screen reader assertions
- Use "I SEE" for visual and keyboard assertions
- Specify the AT in the WHEN clause when relevant: "WHEN I use a screen reader (NVDA, JAWS, VoiceOver)"
- AAA recs may omit Gherkin if the requirement is a usage constraint rather than a testable behaviour

### 5. Developer note (optional)
Include when there are known screen reader quirks, timing issues, or non-obvious
implementation requirements. Rendered as a muted left-bordered callout below the Gherkin.
Prefix with "Developer note:". Keep to 1–2 sentences.
Example: "Developer note: NVDA needs a ~100ms setTimeout before the element is injected."

---

## Tags

Each AC must have one or more tags. These drive the filter bar in the HTML output.
Tag values: `screenreader` | `keyboard` | `visual`
Multiple tags are space-separated in the `data-tags` attribute, e.g. `data-tags="critical keyboard screenreader"`
The group tag (critical / high / recommended) is always included alongside the modality tag(s).

---

## Output formats

### HTML (default for Option A)
Fully self-contained `.html` file. Must include:
- Page header: component name + "Accessibility acceptance criteria" as h1,
  WCAG target + package + reviewed date as subtitle
- Filter bar: All | Critical (Level A) | High (AA) | Recommended | Screen reader | Keyboard | Visual
- Three AC groups with uppercase section labels
- Per-card copy button: copies badges + title + body as plain text to clipboard
  Copy format: `{badges newline-joined}\n\n{title}\n\n{body plaintext}`
- Button shows "Copied ✓" for 1.5s then reverts
- Background: #f5f4f0. Cards: white with #e0dfd8 border. Font: system-ui stack.
- Gherkin block: monospace, #f7f6f2 bg, left border 3px #d4d3cc
- Developer note block: muted, #f7f6f2 bg, left border 2px #c8c7c0

### Markdown (flat, for Notion / Confluence / GitHub)
Structure mirrors the HTML but rendered as plain Markdown:
- H1: component name + "— Accessibility acceptance criteria"
- H2 per group: "Critical — Level A", "High — Level AA", "Recommended — AAA"
- Per AC: bold title, badges inline as `[Level A]` `[4.1.2]` `[Critical]`,
  body as prose, Gherkin in a fenced code block, developer note as blockquote
- No copy buttons or filter bar — this format is for reading, not tooling

---

## Writing rules

- One AC per finding from the conformance review. Don't bundle multiple SCs into one AC.
- The title must be passable as a Jira story title. Keep it under ~60 characters.
- Body describes what to implement, not why WCAG exists. Assume the engineer knows
  what accessibility is — just tell them what to build.
- Gherkin must be testable by a QA engineer without specialist AT knowledge.
  If it requires specialist knowledge, add a developer note explaining the test setup.
- AAA recs without a clear testable behaviour (e.g. usage constraints) may omit Gherkin.
- Sentence case throughout. No full stops on titles. Full stops on body sentences.
