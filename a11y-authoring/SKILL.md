---
name: a11y-authoring
metadata:
  version: 1.0.1
description: >
  Use this skill whenever the user wants to produce accessibility deliverables — Jira-ready
  acceptance criteria or consumer-facing usage documentation — for a component, pattern, or
  feature. Triggers on: "write ACs for…", "draft acceptance criteria for…", "format these as
  ACs", "Jira-ready ACs", "write usage docs for…", "draft accessibility usage documentation for…",
  "write a11y docs for [component]". Also triggers as the downstream handoff from
  `a11y-wcag-assessment` Step 5 — picks up the verdict and criteria from conversation context and
  produces the deliverable. Works standalone when the user already knows the applicable criteria and
  just wants the format applied. Do NOT trigger for: open-ended conformance assessment or "is this
  accessible?" questions (→ a11y-wcag-assessment), general comms or message drafting that mentions
  accessibility, design system strategy or roadmap planning,
  or building components in Figma.
---

# Accessibility Authoring

Production skill: turn a known conformance picture (verdict + applicable criteria) into a
deliverable — Jira-ready ACs or consumer-facing usage documentation. For assessing conformance
in the first place, see `a11y-wcag-assessment`.

---

## Steps

| Step | What it does | References used |
|------|-------------|-----------------|
| **0** | Confirm inputs: verdict + criteria from prior `a11y-wcag-assessment` run, or a user-supplied list. Ask if unclear. | — |
| **1** | Confirm which deliverable(s): ACs, usage docs, or both. | — |
| **2A** | *(if ACs requested)* Write Jira-ready ACs. Confirm HTML or Markdown output. | `references/ac-format.md` |
| **2B** | *(if usage docs requested)* Write consumer-facing accessibility usage documentation. | `references/usage-docs-format.md`, `references/ds-references.md` |

---

## Step 0 — Confirm inputs

Before writing anything, confirm the source of the criteria. Two paths:

**Handoff path (preferred).** If this skill was loaded after an `a11y-wcag-assessment` run in
the same conversation, pull the verdict + criteria + findings from earlier turns.

**Standalone path.** If invoked cold without a prior assessment, ask the user to provide:

- Component / pattern name and brief description
- Applicable WCAG criteria (SC numbers, with level)
- Platform(s) — Web / iOS / Android / cross-platform
- Standard — WCAG 2.2 AA (default) or AA + AAA
- Package / DS context if writing usage docs (e.g. the consuming package name, org, or product)

---

## Step 1 — Choose deliverable(s)

Ask the user which of:

- **Acceptance criteria** — Jira-ready, one AC per finding (Step 2A)
- **Usage documentation** — consumer-facing, component-level (Step 2B)
- **Both** — produce ACs first, then usage docs

---

## Step 2A — Acceptance criteria

Load `references/ac-format.md` and follow it. Key rules from that file:

- Three groups: **Critical** (Level A) / **High** (AA) / **Recommended** (AAA)
- Each AC has five elements in fixed order: badges, title, body, Gherkin, optional developer note
- Tags: `screenreader` | `keyboard` | `visual` — drive the filter bar in HTML output
- One AC per finding. Don't bundle multiple SCs into one AC.

After drafting the ACs, ask the user for output format:

- **HTML** — interactive widget with filter bar and per-AC copy-to-clipboard. Self-contained `.html` file.
- **Markdown** — flat `.md` file suitable for Notion, Confluence, or GitHub.

---

## Step 2B — Usage documentation

Load `references/usage-docs-format.md` and follow it. Cross-reference `references/ds-references.md`
for style conventions — match what the target design system expects, currently informed by GOV.UK and Carbon.

---

## When to push back

Do not produce deliverables when the upstream picture is unclear. Specifically:

- Vague criteria ("make sure it's accessible") — push for SC numbers
- No platform specified — ask, or default to Web with a note
- Missing component context for usage docs (no package, no consumer audience) — ask
- Findings that contradict each other from different sources — route back to `a11y-wcag-assessment`

---

## Reference files

| File | Status | Purpose |
|------|--------|---------|
| `references/ac-format.md` | Ready | AC format spec: structure, badges, Gherkin pattern, HTML/MD output rules |
| `references/usage-docs-format.md` | Ready | Usage documentation format and section structure |
| `references/ds-references.md` | Ready | Design systems to reference for documentation style and conventions |

---

## Changelog

### 1.0.1
- Pruned 28 lines of redundancy and reactive guardrails.
- Cut reference-file duplication in Step 2B (section list, output format rule already in `usage-docs-format.md`).
- Cut trailing reference-file restatements in Step 2A and Step 2B.
- Cut reactive coordination notes in Step 0 and Step 1.
- Cut justification prose from "When to push back".
- Cut "Source Hierarchy" section — duplicated "Reference files" table.

### 1.0.0
- Initial release. Split from `wcag-conformance` v2.0.0 (now `a11y-wcag-assessment` v3.0.0).
- Step 5 Option A (AC authoring) promoted to primary flow (Step 2A).
- Step 5 Option B (usage docs) promoted to primary flow (Step 2B).
- Inputs (Step 0) handles both handoff and standalone paths.
- Reference files `ac-format.md`, `usage-docs-format.md`, `ds-references.md` moved from `wcag-conformance/references/`.
- Added "When to push back" section — explicit guard against producing deliverables from thin or contradictory inputs.
