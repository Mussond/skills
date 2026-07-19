# Atomica11y Reference

Source: https://www.atomica11y.com/
Updated: 2026-03

Atomica11y provides per-component accessibility checklists across four dimensions:
- **Design** — what to specify in Figma (UX/visual requirements, WCAG-mapped)
- **Web** — HTML/ARIA patterns + Gherkin-style test checklists
- **iOS** — HIG-aligned criteria + VoiceOver/Switch Control behaviour
- **Android** — Material-aligned criteria + TalkBack behaviour

---

## Offline JSON Sources

Web, iOS, and Android criteria are all available offline. Do **not** attempt to fetch Atomica11y pages — the site blocks automated requests with a 403.

| Platform | File | Components |
|----------|------|-----------|
| Web | `references/criteria-web.json` | 58 |
| iOS | `references/criteria-ios.json` | 33 |
| Android | `references/criteria-android.json` | 34 |

Each entry in all three files contains:
- `title` — component display name
- `url` — canonical Atomica11y URL (use path slug to identify the component)
- `id` — stable identifier (e.g. `accessible-web-button-json`)
- `compact` — compact plain-text checklist (how-to-test steps)
- `gherkin` — Gherkin-style test scenarios (GIVEN / WHEN / I SEE or I HEAR)

**How to look up a component:** find the slug from the Component Index below, then find the entry in the relevant JSON file where the slug appears at the end of the `url` field. Extract `compact` and `gherkin` and incorporate them into the conformance answer.

**Only Design pages require a screenshot from the user** — use the URL pattern:
`https://www.atomica11y.com/accessible-design/[slug]/`

---

## URL Patterns

| Platform | Base URL | Source |
|----------|----------|--------|
| Design | `https://www.atomica11y.com/accessible-design/[component]/` | Ask the user for screenshot |
| Web | `https://www.atomica11y.com/accessible-web/[component]/` | `criteria-web.json` |
| iOS | `https://www.atomica11y.com/accessible-ios/[component]/` | `criteria-ios.json` |
| Android | `https://www.atomica11y.com/accessible-android/[component]/` | `criteria-android.json` |

---

## Component Index

Columns show the slug for each platform (slugs often differ between platforms) and which JSON file covers it. Design = screenshot from the user required.

### Alerts & Feedback

| Component | Web slug | iOS slug | Android slug | Design |
|-----------|----------|----------|--------------|--------|
| Alert / announcement | `alert` | `announcement` | — | Yes |
| Toast / Snackbar | `toast-snackbar` | — | `snackbar` | Yes |
| Progress indicator | `progress` | `progress-gauge` | `progress-indicator` | Yes |
| Dialog alert | `dialog-alert` | `dialog-alert` | `dialog-modal` | Yes |

### Form Controls

| Component | Web slug | iOS slug | Android slug | Design |
|-----------|----------|----------|--------------|--------|
| Button | `button` | `button` | `button` | Yes |
| Checkbox | `checkbox` | `checkbox` | `checkbox` | Yes |
| Radio button | `radio` | `radio` | `radio` | Yes |
| Toggle switch | `toggle-switch` | `toggle-switch` | `toggle-switch` | Yes |
| Text input | `input-text` | `input-text` | `input-text` | Yes |
| Number input | `input-number` | `input-number` | `input-number` | Yes |
| Password input | `password-input` | — | `input-password` | Yes |
| Textarea | `textarea` | — | — | Yes |
| Select dropdown | `select` | `pop-up-button` | — | Yes |
| Search input | `search` | `search` | `search` | Yes |
| Range slider | `range-slider` | `slider` | `slider` | Yes |
| Stepper input | `stepper-input` | `stepper` | `stepper-input` | Yes |
| Star rating input | `star-rating` | — | — | Yes |
| Autocomplete / Listbox | `listbox-autocomplete` | — | — | Yes |
| Date picker | `date-picker` | `date-picker` | `date-picker` | Yes |
| Filter | `filter` | — | — | Yes |
| Form (general) | `form` | — | — | Yes |
| Hint, help, or error | `hint-help-error` | — | — | Yes |
| Phone input | — | `input-phone` | `input-phone` | — |
| Website input | — | `input-website` | `input-website` | — |
| Segmented control | — | `segmented-control` | `segmented-button` | — |
| Picker button | — | `picker-button` | — | — |
| Picker wheel | — | `picker-wheel` | — | — |
| Pull/drop-down button | — | `pull-drop-down` | — | — |

### Navigation & Structure

| Component | Web slug | iOS slug | Android slug | Design |
|-----------|----------|----------|--------------|--------|
| Navigation landmark | `nav` | — | — | Yes |
| Tab bar / Tab group | `tabs` | `tab-bar` | `tabs` | Yes |
| Breadcrumb navigation | `breadcrumbs` | — | — | Yes |
| Pagination nav | `pagination` | — | — | Yes |
| Skip link | `skip-link` | — | — | — |
| Nav popover button | `nav-popover` | — | — | Yes |
| Header / banner landmark | `header` | — | — | Yes |
| Footer / contentinfo | `footer` | — | — | Yes |
| Main landmark | `main` | — | — | Yes |
| Region / section landmark | `section-region` | — | — | Yes |
| Sticky element | `sticky-content` | — | — | Yes |
| Scrolling container | `scrolling-container` | `horizontal-scroll` | — | Yes |
| Web HTML page | `html` | — | — | — |
| iOS app view | — | `ios-view` | — | — |
| Bottom app bar | — | — | `bottom-app-bar` | — |
| Navigation bar (Android) | — | — | `navigation-bar` | — |
| iframe | `iframe` | — | — | — |

### Disclosure & Overlay

| Component | Web slug | iOS slug | Android slug | Design |
|-----------|----------|----------|--------------|--------|
| Expander accordion | `expander` | `expander` | — | Yes |
| Dialog modal | `dialog-modal` | `dialog-modal` | `dialog-modal` | Yes |
| Dialog sheet | `dialog-sheet` | `dialog-sheet` | `sheet` | Yes |
| Dialog full screen | — | — | `dialog-full-screen` | — |
| Tooltip | `tooltip` | `popover` | `tooltip` | Yes |
| Tooltip rich | — | — | `tooltip-rich` | — |
| Popover | `popover` | — | — | Yes |
| FAQ | `faq` | — | — | Yes |

### Display & Content

| Component | Web slug | iOS slug | Android slug | Design |
|-----------|----------|----------|--------------|--------|
| Card | `card` | `card` | `card` | Yes |
| Informative image | `image` | `image` | `image` | Yes |
| Decorative image / icon | `image-decorative` | `image-decorative` | `image-decorative` | Yes |
| Heading | `heading` | `heading` | `heading` | Yes |
| Link | `link` | `link` | — | Yes |
| List | `list` | — | — | Yes |
| Table | `table` | — | — | Yes |
| Strikethrough content | `strikethrough` | — | — | — |
| Footnote | `footnote` | — | — | Yes |
| Separator / HR | `separator` | — | — | Yes |
| Maps, charts & graphics | `figure` | — | — | Yes |
| Video/audio player | `video-audio` | — | — | Yes |
| Carousel slideshow | `carousel` | `carousel` | `carousel` | Yes |
| Badge | — | — | `badge` | — |
| Chips | — | — | `chips` | — |
| Menu | — | — | `menu` | — |
| Icon button | — | — | `button-icon` | — |
| Floating action button | — | — | `button-floating` | — |

### Dynamic & App Patterns

| Component | Web slug | iOS slug | Android slug | Design |
|-----------|----------|----------|--------------|--------|
| Dynamic single page app | `aria-live` | — | — | — |
| Chat | `chat` | — | — | Yes |
| Animation | `animation` | — | — | Yes |
| Time picker | — | — | `time-picker` | — |

---

## What Each Platform Section Contains

### Web, iOS, Android checklists (from JSON)
All three platforms have offline JSON files. Each contains:
- Compact step-by-step how-to-test checklist (`compact` field)
- Gherkin-style test scenarios (`gherkin` field): GIVEN / WHEN / I SEE or I HEAR
- Keyboard, desktop screen reader, and mobile screen reader coverage

### Design checklist (from screenshots — ask the user)
- WCAG criterion mapped to each requirement (e.g. "1.4.3 AA")
- What the designer must specify or annotate
- Common anti-patterns to avoid
- Annotation guidance for handoff

---

## Notes on Coverage

- All three platform JSON files are offline — no fetching needed for Web, iOS, or Android
- Only Design pages require a screenshot from the user
- Slugs frequently differ between platforms — always check the Component Index, do not guess
- iOS/Android have platform-specific components not present on web (e.g. `bottom-app-bar`, `tab-bar`, `ios-view`)
- Web has web-specific components not present on mobile (e.g. `iframe`, `skip-link`, `aria-live`)

---

## Adding New Components

When you discover a component on Atomica11y not yet listed here:
1. Add a row to the relevant table above with all available platform slugs
2. Note which JSON files cover it (Web / iOS / Android) and whether Design exists
3. If a new JSON file is provided for a platform, add it to the Offline JSON Sources table at the top
