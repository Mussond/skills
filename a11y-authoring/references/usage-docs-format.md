# Usage Documentation Format

> **Status: Ready** — Format spec for consumer-facing accessibility usage documentation.
> Referenced by Step 2B of the `a11y-authoring` skill.
> Cross-reference `references/ds-references.md` for style conventions.

---

## Audience and purpose

These docs are for **DS consumers** — designers and engineers using the design system's components.
They are not internal accessibility audit records. The audience knows how to code;
they need to know what to do, not why WCAG exists.

Suitable delivery format: Markdown or MDX (Storybook, Notion, Confluence, GitHub).
Never Word or PDF — these docs need to live alongside the component.

---

## Required sections (in order)

### 1. Header block
Four metadata fields, always present:
- **Component:** `ComponentName`
- **Package:** `@your-org/your-package` (or relevant package)
- **WCAG target:** 2.2 AA (or the standard in scope from Step 0)
- **Last reviewed:** Month Year

### 2. Overview
1–3 sentences: what the component is, and what makes its accessibility requirements
non-obvious. Lead with the thing consumers are most likely to get wrong.
Do not repeat the component description from Storybook — add something.

### 3. Usage context / when to use each mode
Only needed when accessibility behaviour varies by usage. If the component has one
correct implementation, skip this section. Include when:
- Rendering context changes the correct implementation (static vs dynamic)
- Component has variants with different accessibility implications
- Props interact in ways that can produce incorrect results if misused
Include a code example for each mode. Use a lookup table when 3+ modes exist.

### 4. Consumer responsibilities
What the component does NOT handle automatically, and what the consumer must provide.
Examples: accessible names, focus management, label text quality, ARIA attributes
that depend on context. Show correct and incorrect code side by side where useful.
Each responsibility is a named subsection with a code example.

### 5. Usage constraints
Things consumers must NOT do. One constraint per subsection. Each one must explain
the impact, not just state the rule. If there is a correct alternative, name it.
Example: "Do not auto-dismiss — use Toast for transient messages instead."

### 6. Focus management
Only required when the component has open/close/dismiss behaviour. Document:
- Where focus goes when the component opens (if applicable)
- Where focus returns when the component closes or is dismissed
- What the consumer is responsible for vs what the component handles
Include a code example for focus return pattern.

### 7. Known screen reader quirks
Only include when real, verified AT behaviour must be accounted for in implementation.
Do not speculate. Each quirk needs: the AT affected, the behaviour, and the workaround.
Keep this section short — if there are no real quirks, omit it entirely.

### 8. Testing checklist
Split into three groups — always in this order:
- **Screen reader** (NVDA, JAWS, VoiceOver)
- **Keyboard**
- **Visual**
Use checkbox list format (`- [ ]`). Each item is one testable assertion.
This is the last thing the engineer checks before marking a story done.

### 9. Props reference (accessibility-relevant only)
Table with columns: Prop | Type | Required | Notes.
Only include props that have accessibility implications. Skip purely visual props
unless they affect AT output. The Notes column is where the important guidance lives.

### 10. Footer citation
Always end with a single italicised line:
  *Reviewed against [standard] and [source(s)]. [Month Year].*
Example: *Reviewed against WCAG 2.2 AA and Atomica11y Alert criteria. March 2026.*

---

## Optional sections

Include when applicable. These are not required for every component.

- **Contrast requirements** — when the component uses tinted backgrounds or sentiment
  colour variants that carry contrast risk. Include a table of min ratios by text size.
- **Resize and reflow** — when the component has complex layout likely to break at
  200% zoom or 320px viewport. List the specific conditions to test.
- **Variant / state checklist** — when the component has multiple sentiment or state
  variants with distinct accessibility requirements per variant. Use a table.

---

## Tone rules

- Sentence case throughout. No Title Case headings.
- Directive without being prescriptive. Say what to do; don't lecture about why
  accessibility matters.
- No hedging. "Must" means must. "Should" means recommended. Be clear which is which.
- Code examples for every consumer responsibility. Do not describe without showing.
- No marketing language. Do not say "powerful", "robust", or "accessible by default"
  unless it's precisely true and you can back it up.
- Keep prose tight. One idea per paragraph.
