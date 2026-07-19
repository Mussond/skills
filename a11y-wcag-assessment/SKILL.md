---
name: a11y-wcag-assessment
metadata:
  version: 3.2.0
description: >
  Use this skill whenever the user asks whether something is accessible, conformant, or meets WCAG
  criteria — diagnostic only. Accepts code (HTML snippets, component source), screenshots, or
  descriptive input. Triggers on: "is this button accessible?", "does this component pass WCAG?",
  "what criteria apply to [component/pattern]?", "check this against WCAG", "what do I need for a
  conformant [component]?", "accessibility requirements for X", or EN 301 549 questions. Always load
  before answering — even brief questions — it contains a curated source hierarchy and reasoning
  framework. Do NOT trigger for: writing ACs or usage documentation (→ a11y-authoring), general comms
  or message drafting that mentions accessibility, design system strategy or
  roadmap planning, or building components in Figma.
---

# WCAG Conformance Assessment

Diagnostic skill: evaluate whether a component, pattern, or feature meets WCAG / EN 301 549
conformance. For producing ACs or usage docs from this verdict, see `a11y-authoring`.

---

## Steps

- [ ] Step 0: Confirm platform(s), assets, and standard in scope
- [ ] Step 1: Identify what kind of thing it is
- [ ] Step 2: Map to applicable WCAG criteria
- [ ] Step 3: Pull component-level checklists and Gherkin from Atomica11y
- [ ] Step 3b.0: Environment check *(web Code pathway only)*
- [ ] Step 3b.1: Static cross-reference *(web only)*
- [ ] Step 3b.2: Execute axe-core *(web Code pathway, env check passed)*
- [ ] Step 4: State the verdict
- [ ] Step 5: Handoff prompt

---

## Step 0 — Ask these questions first

Before answering any conformance question, confirm the following if not already clear
from context.

**1. Platform(s) in scope?**
- Web
- iOS
- Android
- All three / cross-platform

**2. Assets(s) in scope?**
- Designs
- Code
- Both

**3. Standard in scope?**
- WCAG 2.2 AA *(default — use this if the user doesn't specify)*
- WCAG 2.2 AA + AAA *(when the user wants to go beyond the baseline)*

---

## Step 1 — Identify what kind of thing it is

Classify the component by type. A component may span multiple types — apply every
type table that fits.

Types: **interactive**, **informational**, **container**, **stateful**. See
`references/wcag-criteria-by-type.md` for definitions, examples, and cross-type combinations.

## Step 2 — Map to applicable WCAG criteria

Load `references/wcag-criteria-by-type.md` and apply every type table that matched
in Step 1. Default target is **WCAG 2.2 AA** (Level A + AA).

If Step 0's standard includes AAA, surface the "AAA worth surfacing" rows from each table.

## Step 3 — Check component-level guidance (Atomica11y)

Load `references/atomica11y.md` and follow the lookup procedure there.

**Pre-processing (required for whole-page or multi-component inputs):**
If the input is a URL, screenshot, or other multi-component surface rather than a
named component, first enumerate every discrete component type present on the page
(e.g. skip link, dialog modal, radio button, nav landmark, heading). Then look up
each one individually in the Component Index. Do not wait for a single component name
to be supplied — derive the list from the content itself.

Use the platform answer from Step 0 to pick the right JSON file.

**Code (or Both):** extract `compact` and `gherkin` from the JSON entry. The `compact`
field is the test checklist; `gherkin` is scenario language for ACs (handed off to `a11y-authoring`).

**Design (or Both):** ask the user for a screenshot of the design page
(`atomica11y.com/accessible-design/[slug]/`). Walk through the same `compact` checklist
asking *does the design enable each test to pass?* — no code to verify, just visual conformance.

## Step 3b — Axe-core layer (web only)

**Only run this step when platform is Web.** Skip entirely for iOS, Android, or Design-only reviews.

**Step 3 must complete before Step 3b begins.** Do not proceed to axe-core until all
applicable components have been looked up in the Atomica11y Component Index and their
`compact` checklists extracted. Step 3b supplements Step 3 — it does not replace it.

Three sub-steps. Which run depends on Step 0's asset answer:

- **Design only** → run 3b.1 only (static cross-reference).
- **Code or Both** → run 3b.0, then 3b.1, then 3b.2 if env check passed.

### Step 3b.0 — Environment check (Code pathway only)

Before running axe-core, verify the execution environment:

- Node.js available
- `axe-core` installed or installable
- `jsdom` installed or installable

If any are missing, **stop**. Report which dependencies are missing and ask the user whether to:

- **(a)** fall back to static cross-reference only (3b.1), or
- **(b)** abort and resolve the environment first.

### Step 3b.1 — Static cross-reference

Use the standard answered at Step 0 to filter `references/axe-rules.json`:
- **WCAG 2.2 AA** → `wcag20aa` + `wcag21aa` + `wcag22aa` groups
- **WCAG 2.2 AA + AAA** → above + `wcag_aaa` rules

For each rule that maps to a WCAG criterion already identified in Step 2, surface in your findings:

- `id` — the axe rule ID (e.g. `button-name`)
- `description` — what the rule checks
- `impact` — critical / serious / moderate / minor
- `issue_type` — whether it returns `failure` (definitive) or `needs review` (requires manual confirmation)
- `enabled_default` — flag if `false`; rules disabled by default (wcag22aa `target-size`, all wcag_aaa, all experimental) require explicit axe configuration to run
- `help_url` — link to the Deque rule documentation

**Group findings into two buckets:**

1. **Automatically detectable** — `issue_type` includes `failure`; axe will flag these in CI
2. **Requires manual review** — `issue_type` is `needs review` only; axe surfaces incomplete results, engineer must confirm

### Step 3b.2 — Execute axe-core against supplied code

**Preconditions:** Code pathway, env check (3b.0) passed, the user has provided an HTML snippet or component source.

Run axe-core via jsdom against the snippet, configured with the same WCAG tags from Step 0:

- **WCAG 2.2 AA** → `{ runOnly: { type: 'tag', values: ['wcag2a','wcag2aa','wcag21a','wcag21aa','wcag22aa'] } }`
- **WCAG 2.2 AA + AAA** → above + `wcag2aaa`

Return three sets, mapped back to the Step 2 criteria where possible:

1. **Violations** — rules that fired. Include rule id, impact, target selector, failure summary, help_url.
2. **Incomplete** — rules that need manual confirmation. Same fields.
3. **Passes** — rules that ran cleanly. Summarise rather than list in full.

Note rules from 3b.1 that **did not fire** because the snippet didn't contain the relevant patterns —
those still need manual review against the full component, not just the snippet.

## Step 4 — State your verdict

Structure answers as:
1. **Applicable criteria** — which ones matter and why
2. **Automated test coverage** (web only) — report which 3b path ran:
   - **3b.1 only** (Design or env check failed/declined): static cross-reference buckets (auto-detectable / manual review)
   - **3b.1 + 3b.2** (Code, env check passed): actual axe violations + incomplete + passes, plus 3b.1 rules that didn't fire on the snippet
   - When 3b.2 ran, append two reminders to the verdict: (a) jsdom is not a real browser — rules depending on computed layout, real rendering, or focus management may produce false negatives; (b) snippets without surrounding document context miss landmark and region rules — wrap the snippet or note the gap.
3. **What conformance requires** — design, HTML/ARIA or native semantics, behaviour
4. **Platform-specific notes** — if cross-platform, call out where requirements diverge
5. **Common failure patterns** — what typically goes wrong
6. **AAA notes** — flag any AAA criteria worth pursuing even if not required

---

## Step 5 — Handoff

After delivering the verdict, ask the user if they want either:

- **Formal acceptance criteria** for the findings (Jira-ready, HTML or Markdown output)
- **Consumer-facing usage documentation** for the component

Both deliverables are produced by the **`a11y-authoring`** skill. If the user wants either, route there;
that skill picks up the verdict and criteria from this conversation's context.

If the user declines both, the review ends here.

---

## Source Hierarchy

Active sources, in order of authority:

1. **WCAG 2.2 Quick Reference** — canonical baseline for all criteria.
   https://www.w3.org/WAI/WCAG22/quickref/ · Understanding: https://www.w3.org/WAI/WCAG22/Understanding/
2. **Atomica11y** — component-level checklists across Web, iOS, Android. See `references/atomica11y.md`.
3. **Axe-core** — web-only automated checks. See `references/axe-rules.json`.

---

## Changelog

See `references/changelog.json`.
