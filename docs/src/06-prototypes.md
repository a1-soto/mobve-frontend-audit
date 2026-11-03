# Prototypes as solution

Date: 2026-11-03. The prototypes apply the design system to real screens. They use only `design-system/mobve-design-system.css`; data is illustrative. The Mobve name appears as text only: the logo was not redrawn, as the brand rules forbid replacing it.

## 1. Prototypes

| File | What it shows |
|---|---|
| `design-system/prototype.html` | Website: header, hero, scenario tabs, dark demo band, solutions, pricing, FAQ, contact form, footer. App: sidebar, header, information notice, KPI tiles, call volume chart, received and completed chart, attention panel, week of appointments, maintenance table, empty state, confirmation dialog |
| `design-system/appointments.html` | Appointments screen with the structure of the current app: reporting filters, six scorecards, week calendar with category colors, attention panels, upcoming list with category and status |
| `design-system/index.html` | Design system reference with every component and state |

## 2. Findings and how the prototypes answer them

| Finding | Where | Answer in the prototypes |
|---|---|---|
| No working contact path | Website | Contact form that works without the chat, with validation and a confirmation |
| Demo looks active but is unavailable | Website | Disabled call button, warning notice, early access action |
| Brand font not loaded, 20 sizes, text under 12 px | Website, app | Inter Variable, nine type roles, 12 px minimum |
| Weak or missing hover and pressed states | Website, app | Every control shows distinct hover, pressed, focus, disabled and loading states |
| Six blues, 30 color variables | Website, app | 6 base colors and calculated states |
| Status colors unclear | Website, app | Traffic-light signals with dark text, icons and tints |
| Pricing without emphasis | Website | One recommended plan with a secondary badge (the plan choice is an example) |
| Property cards look clickable but are not | Website | Solution cards are links with hover |
| Chat button covers content | Website | Not prototyped |
| Category colors collide with primary and error | App | Five new category colors on dots, event edges and tints |
| Chart legends too small | App | 14 px markers and labels; Completed in success green; average as dashed gray line |
| Touch targets under 44 px | Website, app | 44 px controls and menu items |
| Resident requests error, Pipeline overflow, page titles | App | Not prototyped: they are code fixes in the app |

## 3. How to view

Open the HTML files in a browser from this repository; they load the CSS by relative path and the Inter font from Google Fonts for the preview. PDF exports of each page are in `docs/pdf/`.
