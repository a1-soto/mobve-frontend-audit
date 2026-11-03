# Mobve: frontend audit and design system

Audit of the public website (mobve.com) and the staff app (staging), a proposed design system for both, and prototypes that apply it. Date: 2026-11-03.

## Start here

- Summary: `docs/html/index.html` or `docs/pdf/00-summary.pdf`.
- Flow diagrams: `diagrams/web-flow.pdf` and `diagrams/app-flow.pdf`.
- Design system reference with live specimens: `design-system/index.html`.
- Prototypes: `design-system/prototype.html` (website and app) and `design-system/appointments.html` (Appointments screen).

## Contents

```
docs/
  src/    Markdown source of every document
  html/   HTML version (index.html is the summary)
  pdf/    PDF version of every document, the design system reference and the prototypes
diagrams/
  web-flow.html, web-flow.pdf   website flow
  app-flow.html, app-flow.pdf   staff app flow
design-system/
  mobve-design-system.css   tokens, base styles and components
  index.html                design system reference page
  prototype.html            website and app prototype
  appointments.html         Appointments screen prototype
```

## Documents

| # | Document | HTML | PDF |
|---|---|---|---|
| 00 | Summary | docs/html/00-summary.html | docs/pdf/00-summary.pdf |
| 01 | Website audit | docs/html/01-website-audit.html | docs/pdf/01-website-audit.pdf |
| 02 | Indexing | docs/html/02-indexing.html | docs/pdf/02-indexing.pdf |
| 03 | App audit | docs/html/03-app-audit.html | docs/pdf/03-app-audit.pdf |
| 04 | App click test | docs/html/04-app-click-test.html | docs/pdf/04-app-click-test.pdf |
| 05 | Design system | docs/html/05-design-system.html | docs/pdf/05-design-system.pdf |
| 06 | Prototypes | docs/html/06-prototypes.html | docs/pdf/06-prototypes.pdf |

Also in `docs/pdf/`: `design-system-reference.pdf`, `prototype-website-and-app.pdf`, `prototype-appointments.pdf`.

## Viewing

Open the HTML files in a browser. They load the CSS by relative path, the Inter font from Google Fonts and, for the diagrams, the Mermaid library from a CDN, so an internet connection is needed for the exact rendering. Production should self-host Inter Variable.

## Scope

The audit covers what a browser can see: rendered pages, computed styles, network calls, HTTP headers and the public website JavaScript. It does not cover the app's source code, the backend, Cloudflare or DNS settings, or actions that write data. Details in the scope section of each document.
