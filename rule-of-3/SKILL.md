---
name: rule-of-3
description: >
  Stress-test a Figma component using the Rule of 3 — triple the copy,
  triple the functions, triple the content — to surface translation, zoom,
  viewport and use-case fragility before the component ships.
  Trigger when:
  * The user asks to "run rule of 3" / "stress test" / "QA" a component in Figma
  * The user mentions "triple the copy / functions / content" or "Rule of 3"
  * The user wants to check a component for translation, zoom, accessibility text scaling, or unknown future use cases
  * The user pastes a Figma component URL / selects a component and asks to harden it
  Always confirm the Figma connection is live before any write.
---

# Version
**version**: 0.1.0
Always use Semantic Versioning 2.0.0 (https://semver.org/) with this skill. Given a version number MAJOR.MINOR.PATCH, increment the:
- MAJOR version when you make incompatible API changes
- MINOR version when you add functionality in a backwards-compatible manner
- PATCH version when you make backwards-compatible bug fixes

# Rule of 3 — Component stress test in Figma

A cheap, repeatable QA method. Given a component, the skill produces three Sections in the same Figma file — one per rule — populated with stressed instances drawn from a user-curated variant subset. The source component is never modified; everything the skill creates lives inside the three Sections so it's trivially deletable.

The three rules:
1. **Three times the copy** — replace each text layer with `W × (3×count + 2)` (capital W is the widest Latin glyph; +2 is insurance).
2. **Three times the functions** — triple every action/button/link in the component and design the overflow.
3. **Three times the content** — triple every content slot (image, tag, paragraph, icon) and decide wrap/limit/show-more behaviour.

References live in `references/`:
- `w-string-formula.md` — the tripled-W algorithm with worked numbers
- `function-tripling-patterns.md` — how to absorb action explosion (visible group + overflow menu)
- `content-tripling-patterns.md` — wrap vs. view-more vs. hard limit
- `section-naming.md` — Section naming + layout convention so runs are repeatable

---

## Runtime checklist

At the start of the run, print the checklist below to the user verbatim. After each step, re-print it with that step's box ticked. At the end, print the final state alongside the findings summary.

Status markers:
- `- [ ]` not started
- `- [x]` complete
- `- [!]` skipped or failed — append a one-line reason

```
Rule of 3 — run checklist
- [ ] 0a. Figma connection check (figma_get_status)
- [ ] 0b. Confirm component input
- [ ] 1.  Pull component details (variants, booleans, slots)
- [ ] 2.  User curates variant × boolean subset
- [ ] 3.  Draft test plan, await go-ahead
- [ ] 4.  Create three Sections in Figma
- [ ] 5.  Copy rule — tripled-W instances placed + screenshotted
- [ ] 6.  Functions rule — tripled-action instances placed
- [ ] 7.  Content rule — tripled-content instances placed
- [ ] 8.  Auto-arrange + findings summary
```

---

## Steps table

| Step | What it does | MCP tools used |
|------|--------------|----------------|
| 0a | Check Figma connection. Pause if not connected. | `figma_get_status` |
| 0b | Confirm component input (URL, selection, or name). | `figma_get_selection`, `figma_search_components` |
| 1  | Pull component details. | `figma_get_component_details`, `figma_analyze_component_set` |
| 2  | User curates the variant × boolean matrix. | — (AskUserQuestion) |
| 3  | Draft per-rule test plan; wait for go-ahead. | — |
| 4  | Create three Sections next to the component. | `figma_create_child`, `figma_move_node` |
| 5  | Copy rule. | `figma_instantiate_component`, `figma_set_text`, `figma_capture_screenshot` |
| 6  | Functions rule. | `figma_instantiate_component`, `figma_set_instance_properties`, `figma_clone_node`, `figma_create_child` |
| 7  | Content rule. | `figma_instantiate_component`, `figma_clone_node`, `figma_set_instance_properties` |
| 8  | Auto-arrange + findings summary. | `figma_arrange_component_set`, `figma_capture_screenshot` |

---

## Step 0a — Check the Figma connection

Before any other action, call `figma_get_status`.

- If the response indicates the plugin/console is **connected and a file is open**, tick `0a` and proceed.
- If **not connected** (no plugin, no open file, or status reports an error): print this message and stop work until the user confirms:

  > Figma isn't connected. Please open the figma-console-local plugin in your Figma file, then reply "ready" and I'll resume.

  When the user replies, call `figma_get_status` again. Repeat until healthy. Mark `0a` complete only after a healthy status response.

## Step 0b — Confirm component input

Resolve the component in this priority order:

1. **Explicit input** — the user supplied a Figma URL, node ID, or component name. Use it.
2. **Active selection** — call `figma_get_selection`. If a component or instance is selected, confirm with the user: *"Run Rule of 3 on `<component name>`?"*
3. **Search** — if neither, ask the user for the component name and call `figma_search_components`.

If the resolved node is an **instance**, walk up to the main component or component set. The skill always operates on the source component definition, never on a placed instance.

## Step 1 — Pull component details

Call `figma_get_component_details` on the component. If it's a component set, also call `figma_analyze_component_set`.

Capture and hold in working memory:
- **Variants** — every property name and its values (e.g. `size: [sm, md, lg]`, `state: [default, hover, pressed, disabled]`).
- **Boolean props** — every boolean property (e.g. `hasIcon`, `showStats`).
- **Text layers** — every visible text layer with its current string and node ID.
- **Action slots** — instances of buttons, links, icon-buttons, or menus inside the component.
- **Content slots** — image fills, tag lists, paragraph text, icons, repeating children.

Print a one-paragraph summary so the user can sanity-check it before step 2.

## Step 2 — User curates the variant × boolean matrix

Combinatorial blow-up is real. Do **not** build for every combination. Present the full matrix as a checklist and ask the user to tick the subset that matters.

Use `AskUserQuestion` with `multiSelect: true` if the count is small (≤ 4 options total). For larger matrices, print the matrix as a markdown checklist and ask the user to paste back the rows they want.

Reasonable defaults to suggest:
- One row per top-level variant value (e.g. one per `size`).
- The most error-prone state (`disabled`, `error`, or `selected`).
- Every boolean toggled both ways at least once.

Do not write to Figma yet.

## Step 3 — Draft the test plan

For each rule that's in scope (default: all three; the user may scope down with "skip content" etc.), write a short plan in chat:

- **Copy** — list every text layer per chosen variant and the tripled-W string it will receive.
- **Functions** — list every action slot per variant and what tripling means (e.g. "1 primary → 1 primary + 1 secondary + 1 tertiary, with a More menu for overflow").
- **Content** — list every content slot per variant and what 3× looks like (e.g. "1 image → 3 images, wrapped row + view-more").

End with: *"Reply 'go' to build, or tell me what to change."* Wait for explicit go-ahead.

## Step 4 — Create the three Sections

Place three top-level Sections to the right of the source component, stacked vertically with a clear gap. Names exactly:

1. `Rule of 3 — Copy`
2. `Rule of 3 — Functions`
3. `Rule of 3 — Content`

Use `figma_create_child` to create each Section. See `references/section-naming.md` for the layout convention (width, gap, label colour).

If any of these Sections already exist from a prior run, **append a timestamp** to the new ones (`Rule of 3 — Copy (2026-05-17 14:32)`) rather than overwriting.

## Step 5 — Copy rule

For each curated variant:

1. Instantiate the component into the Copy section with `figma_instantiate_component`, applying the variant + boolean values.
2. For each visible text layer, apply the tripled-W formula (see `references/w-string-formula.md`):
   - `count = len(original_text)` (include spaces)
   - `w_count = (3 × count) + 2`
   - new string = `"W" × w_count` (preserve original spaces by inserting a space at the same proportional positions — `references/w-string-formula.md` covers this)
3. Call `figma_set_text` on each layer.
4. `figma_capture_screenshot` of the instance and hold the path for the summary.

Note anything that breaks: wrapping issues, alignment drift, overflow clipping, fixed-width containers. Record it for step 8.

## Step 6 — Functions rule

For each curated variant:

1. Instantiate the component into the Functions section.
2. Count action slots in the source component (`button`, `link`, `icon-button`, `menu` instances). Triple the count.
3. Apply the tripling pattern from `references/function-tripling-patterns.md`:
   - 1 action → 3 inline actions
   - 2 actions → 3 inline + a "More" menu placeholder
   - 3+ actions → 3 visible + remainder in a "More" menu
4. Where actions are properties (e.g. `secondaryAction` boolean), toggle them on via `figma_set_instance_properties`. Where slots accept child instances, clone an existing action node with `figma_clone_node` and place it adjacent.

Record any overflow, alignment, or stacking issue.

## Step 7 — Content rule

For each curated variant:

1. Instantiate the component into the Content section.
2. Count content slots: images, tag instances, paragraph text blocks, repeating icons. Triple each.
3. Apply patterns from `references/content-tripling-patterns.md`:
   - Tags → expect to wrap; record if the row blows the container width.
   - Images → expect to need a limit or a "view more" — record the redesign decision.
   - Paragraphs → expect to wrap; record any clipped height.
4. Use `figma_clone_node` for repeating children. Where the count is governed by a property, set it via `figma_set_instance_properties`.

Record breakage.

## Step 8 — Auto-arrange + findings summary

1. Auto-arrange each Section using `figma_arrange_component_set` (or manual grid layout if not applicable).
2. Take one `figma_capture_screenshot` per Section for the summary.
3. Emit the findings summary in chat:

   ```
   Rule of 3 — findings for <component>
   
   ✅ Passed
   - <variant + rule that held up cleanly>
   
   ⚠️ Issues found
   - Copy / <variant>: <one-line issue, e.g. "heading wraps under the icon, icon centres">
   - Functions / <variant>: <issue>
   - Content / <variant>: <issue>
   
   Recommended fixes
   - <one-line fix per issue, grouped by component layer>
   
   Run checklist (final)
   - [x] 0a. Figma connection check
   - [x] 0b. ...
   ```

End with: *"The three Sections are in the file. Delete them to clean up, or keep them as a regression reference."*

---

## Safety / scope guards

- **Never edit the source component.** Always operate on instances placed inside the three Sections.
- **All writes are scoped to the three Sections.** No nodes outside those Sections are created, moved, or modified.
- **Confirm before writing.** The Figma-mutating steps (4–7) run only after step 3 receives an explicit go-ahead.
- **Idempotent runs.** If a prior run's Sections exist, timestamp the new ones rather than overwriting.

---

## Optional scoping

The user can scope the run with phrases like:
- "just the copy rule" — run steps 0–5, 8 only.
- "skip content" — run steps 0–6, 8 only.
- "functions and content" — run steps 0–4, 6, 7, 8 only.

Mark out-of-scope rule steps as `- [!] skipped on request` in the final checklist.
