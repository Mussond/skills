# Function-tripling patterns

The functions rule answers: *"what does this component do when the next team needs one more action?"* Tripling forces a redesign decision early, while it's cheap.

## Counting

An "action" is anything the user can interact with that triggers behaviour:

- Buttons (primary, secondary, tertiary, ghost, icon-only)
- Links
- Menu triggers
- Toggle controls (switches, segmented controls) — each option counts as one action
- Inline form controls (inputs with submit-on-blur, dropdowns)

Don't count the component itself when it's a single interactive (e.g. a card-as-link); count the *internal* actions.

## Tripling rules

| Original count | Tripled target | Pattern |
|---------------:|---------------:|---------|
| 1 | 3 | 3 inline actions, equal weight or a clear primary + 2 secondaries |
| 2 | 6 | 3 inline visible + 1 "More" menu containing the remaining 3 |
| 3 | 9 | 3 inline visible + 1 "More" menu containing 6 — or split into primary cluster + secondary cluster |
| 4+ | 3× | Keep 3 visible inline, push the rest into "More" / overflow menu / dropdown. The right answer is often: *we don't need to display all of them inline ever* |

## Common breakage to record

- **No "More" affordance exists yet** — the component has no overflow strategy. Findings entry: *"add overflow menu pattern at width ≤ X"*.
- **Inline alignment breaks** — the action row was hand-spaced rather than using a layout primitive (group + gap). Findings entry: *"convert to flex/auto-layout with wrap or overflow"*.
- **Primary/secondary hierarchy collapses** — once 3 buttons sit together, the visual weight stops reading. Findings entry: *"strengthen primary differentiation, or demote two to text-links"*.
- **Card-as-link contains a button** — nested interactives. Tripling surfaces it immediately. Findings entry: *"split the card affordance; the whole card cannot be a link if it must also contain actions"*.

## Decision prompts to surface to the user

When recording findings, frame them as questions the design team will need to answer, not just bug reports:

- *"At what action count does this component switch from inline to overflow?"*
- *"Is there an accepted 'More' pattern in the system, or does this trigger a new one?"*
- *"Should secondary actions live in the component, or be hoisted to the parent layout?"*
