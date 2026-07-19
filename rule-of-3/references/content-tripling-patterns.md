# Content-tripling patterns

Content tripling is the rule that most often surfaces a *limit* rather than a *fix*. Some content slots should triple gracefully; others should be capped. The skill's job is to make the decision explicit.

## What counts as content

- Images (cover, thumbnail, gallery)
- Tags / chips / pills
- Paragraph text (description, body, helper)
- Repeating icons (status indicators, social links)
- Stats / metrics
- Repeating child instances (list rows, card grids inside a section)

Headings and CTAs count as **copy** and **functions** respectively — not content.

## Tripling strategies per slot type

| Slot type | Tripling outcome | Likely design response |
|-----------|------------------|------------------------|
| **Tags** | 3× tags wrap to multiple rows; one tag's copy might also be long | Wrap row, decide max rows before truncate / "+N more" |
| **Images** | 3× images break the layout — there's usually no room | Set a hard limit (often 1 hero, or N thumbnails), or convert to a gallery affordance |
| **Paragraphs** | 3× paragraphs blow vertical height | Decide line-clamp + "read more", or accept the height |
| **Icons (repeating)** | 3× icons crowd | Inline group with max + overflow, or scrollable row |
| **Stats** | 3× stats break the row | Wrap, or cap at N and surface the rest elsewhere |
| **Child instances** | 3× children expose grid/list behaviour | Confirm the wrap, gap, and empty/end states |

## When to set a hard limit

Limits are a legitimate output of this rule. Set one when:

- More instances of a slot reduce usability (e.g. a card with 5 thumbnails is harder to scan than one with 1).
- The slot exists to anchor the user (e.g. a single primary image).
- The slot has a semantic ceiling in the broader pattern (e.g. breadcrumbs shouldn't be 30 levels deep).

Record the limit explicitly in findings: *"cap tags at 5, show '+N more' beyond"* — not just *"tags break"*.

## Common breakage to record

- **No wrap behaviour** — the row clips. Findings entry: *"add wrap to tag list"*.
- **Image aspect ratio collapses** — multiple images sized for "the one image" case. Findings entry: *"decide gallery sizing or limit to 1"*.
- **No empty / overflow states** — what does "no tags" or "+12 more" look like? Findings entry: *"design the empty and overflow states for this slot"*.
- **Hardcoded count** — the component assumes exactly 2 or 3 of something. Findings entry: *"loosen to 1..N with defined limit"*.
