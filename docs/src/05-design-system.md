# Design system

Date: 2026-11-03. One token layer for mobve.com and the staff app. Source of values: `design-system/mobve-design-system.css`. Reference page with live specimens: `design-system/index.html`.

## 1. Principles

- Few chosen colors; every state and tint is calculated from them with color-mix(), so nothing drifts out of sync.
- Every interactive control has hover, pressed, focus, disabled, loading and error states, each distinct in color and position.
- Nothing smaller than 12 px; controls 44 px high.
- Color never carries meaning alone: status always comes with an icon or text.
- Target: WCAG 2.2 AA. Every text pair is calculated.

## 2. Color

### 2.1 Base, 6

| Token | Value | Use | Contrast |
|---|---|---|---|
| --color-primary | #0b63ce | Buttons, links, selected state, focus, information, logo | white text 5.69:1 |
| --color-secondary | #ffc845 | Highlights, featured badge, second chart series, accents on the dark band. Never text on paper | ink on it 11.21:1 |
| --color-ink | #101b2b | All text and the dark band | 17.3:1 on paper |
| --color-paper | #ffffff | Surfaces: header, sidebar, cards, panels, inputs | |
| --color-muted | #536173 | Secondary text, captions, placeholders and control borders | 6.32:1 on paper |
| --color-bg | #fafafa | Page background, as in the current app | muted text 6.05:1 |

### 2.2 Semantic, from traffic lights

| State | Signal | Text | Tint | Reference |
|---|---|---|---|---|
| Success | #03a14a (3.39:1 on paper, graphics) | #09672e (7.02:1) | #e1f4e9, 12 percent | green #00a651 |
| Warning | #f7a30d (ink on it 8.4:1) | #7d5002 (6.95:1) | #fef0d8, 16 percent | amber #ffbf00 |
| Error | #d73431 (white text 4.75:1) | #a12623 (7.45:1) | #fbebea, 10 percent | red #e30613 |
| Information | uses the primary and its tint | | | |

The signal marks the state (badge dot, notice border, error border, destructive button, chart status). Text stays in the dark version. The amber warning sits close to the secondary yellow: keep the secondary away from status and always show a warning with its icon and text.

### 2.3 Appointment categories

| Category | Value | On paper | Before | Purposes (inferred, to confirm) |
|---|---|---|---|---|
| Tour | #0891c9 | 3.56:1 | #2a78d6 | Tour, Second Tour |
| Lease | #794db6 | 5.92:1 | #8654b3 | Lease Signing, Renewal Meeting, Document Review, Key Pickup |
| Inspection | #6a7a31 | 4.73:1 | #167a77 | Move In Inspection, Move Out Inspection, Move In |
| Billing | #b55fba | 3.95:1 | #5956c9 | Billing or payment consultation |
| Maintenance | #864821 | 7.09:1 | #b54242 | Maintenance Visit |

Hues avoid the primary, the secondary and the orange-red arc of warning and error, and are at least 0.12 apart in OKLab. They mark dots, event edges and bars; text on them is ink on a 12 percent tint. "General" uses the muted gray.

### 2.4 Calculated, not chosen

| Token | Formula | Result | Use |
|---|---|---|---|
| --color-divider | muted 20 percent over paper | #dddfe3 | Dividers, card edges, neutral badge, disabled field |
| --color-tint | primary 10 percent over paper | #e7effa | Hover fills, selected, information notice |
| --color-tint-strong | primary 24 percent over paper | #c4daf3 | Pressed fills |
| --color-primary-hover | primary with 22 percent black | #094da1 | Hover (white 8.11:1) |
| --color-primary-active | primary with 44 percent black | #063773 | Pressed (white 11.66:1) |
| --color-on-dark-muted | paper 72 percent over ink | #bcbfc4 | Secondary text on the dark band |
| --color-success-tint, warning-tint, danger-tint | signal at 12, 16, 10 percent | #e1f4e9, #fef0d8, #fbebea | Notices and badges |
| --color-danger-hover, danger-active | danger with 22 and 44 percent black | #a82926, #781d1b | Destructive button |

## 3. Typography

Inter Variable, self-hosted (the website policy allows only its own files). Weights 400, 500, 600.

| Role | Size (390 / 768 / 1440 px) | Line height | Tracking | Weight |
|---|---|---|---|---|
| h1 | 40.5 / 52.6 / 64 px, clamp(2.5rem, 1.75rem + 3.2vw, 4rem) | 1.08 | -0.02em | 600 |
| h2 | 32 / 39.4 / 44 px, clamp(2rem, 1.5rem + 2vw, 2.75rem) | 1.12 | -0.02em | 600 |
| h3 | 24 px | 1.25 | -0.01em | 600 |
| Lead | 20 px | 1.45 | 0 | 400 |
| Body | 16 px | 1.5 | 0 | 400 |
| UI (menu, labels, table) | 14 px | 1.4 | 0 | 500 |
| Button | 15 px | 1 | 0 | 600 |
| Caption | 12 px | 1.4 | 0 | 400 |
| Eyebrow | 12 px uppercase | 1.4 | +0.08em | 600 |

Paragraphs stop at 65 characters.

## 4. Space, layout, shape, elevation, motion

- Space: 4 px base, 4, 8, 12, 16, 24, 32, 48, 64, 96 px.
- Layout: container 1240 px, gutter clamp(1rem, 4vw, 2rem), section padding clamp(3rem, 2rem + 4vw, 5rem). Breakpoints 480, 768, 1024, 1280 px.
- Radius: 8 px (controls), 14 px (cards, panels, dialogs), pill (badges).
- Elevation: level 1 cards, level 2 hover and menus, level 3 sticky header, level 4 dialogs, plus an inner pressed shadow.
- Motion: 100, 200, 300, 500 ms; standard and emphasized curves; reduced motion drops transitions to 0.01 ms and removes lifts.

## 5. Components and states

| Component | States |
|---|---|
| Primary button | Hover: 22 percent darker, lifts 1 px, shadow level 2. Pressed: 44 percent darker, sinks 1 px, inner shadow. Focus: 2 px ring, offset 2 px. Disabled: 38 percent opacity. Loading: spinner |
| Secondary and ghost buttons | Hover: tint 10 percent, darker text and border. Pressed: tint 24 percent, sinks 1 px |
| Destructive button | Error signal fill, same hover and pressed steps |
| Inverse button (dark band) | White fill; hover tint, pressed tint strong |
| Field | 44 px, 16 px text, border muted (6.32:1), visible label, "(required)" in text, error with danger border, icon and sentence |
| Badge, notice | Tint background, dark text, signal dot or border, icon |
| Category tag, calendar event | Category dot or 4 px edge, 12 percent tint, ink text |
| Tabs, accordion, card, table, empty state, legend | Defined in the CSS with hover and selected states |

## 6. Charts

| Series | Color | Form |
|---|---|---|
| Main measure (Current, Received) | primary | Bars or solid line |
| Outcome (Completed) | success signal | Bars or 3 px line |
| Waiting | warning signal | Bars with legend only |
| Overdue, failed | error signal | Bars or line |
| Reference (Average call duration, target) | muted | 2.5 px dashed line with dot markers |
| Second measure of the same kind | secondary | Bars with legend only |
| Appointment purposes | category colors | Bars, dots, event edges |

Legend markers are 14 px (22 px dashes for lines) with 14 px labels; the current app uses 11 px markers and 9 to 10 px labels.

## 7. Migration map (main items)

| Item | Today | Proposed |
|---|---|---|
| Color variables | 30 on the website, six blues across site and app | 6 base, 3 semantic pairs, 5 categories, the rest calculated |
| Font | System font on the website, Inter Variable in the app | Inter Variable on both |
| Font sizes and weights | 20 sizes, 8 weights on the website | 9 roles, 3 weights |
| Smallest text | 8 to 10 px | 12 px |
| Touch targets | 21 to 36 px in menus and links | 44 px |
| Radii | 9 values | 3 values |
| Button states | Hover only on some controls, no pressed state | All states on every control |
| Semantic colors | Dark tones on pale backgrounds | Traffic-light signals with dark text and tints |
| Category colors | Collided with primary and error | Five clear hues |
| Page background | #fafafa in the app, mixed tints on the website | #fafafa with white surfaces everywhere |

## 8. Decisions log

1. Palette: three routes were compared against a scan of competitors' colors (blue dominant; violet for AI-forward brands; orange, red and green each used by one competitor). Route A, blue and sun, was chosen: one blue for logo and actions, a warm yellow no direct competitor uses as an accent.
2. One gray, #536173, for secondary text and borders (owner's choice).
3. Semantic colors rebuilt from traffic lights after the first version read as neon green and dark ochre (owner's direction).
4. Button states strengthened after review: steps of about 0.085 in lightness plus position changes.
5. Background #fafafa with white surfaces, as in the current app, after testing #e5e7eb and #eff6ff.
6. Category colors: Tour and Billing at the signal lightness; Lease, Inspection and Maintenance deeper (owner's choice), minimum separation 0.121.
7. Charts: Completed uses the success signal for consistency with the success badge; averages are a dashed gray line.

## 9. Open decisions

- Logo color: route A moves the logo blue from #0878f9 to #0b63ce. This is the client's decision; logo files were not changed.
- Confirm how the 12 appointment purposes map to the 5 categories.
- Dark mode, an icon set and a full data palette are not included.
- color-mix() is supported by current browsers; for older ones replace calculated tokens with their results.
- Validate type and line breaks on the real pages with Inter loaded.
