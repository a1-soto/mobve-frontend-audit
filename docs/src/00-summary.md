# Mobve frontend audit and design system: summary

Date: 2026-11-03. Scope: the public website mobve.com and the staff app on the staging host, plus a proposed design system and prototypes.

Context: mobve.com is the real site, deployed for testing. The staff app runs on a staging host. Findings are therefore split into defects that are real at any stage and items to close before launch.

## Documents

| # | Document | What it covers |
|---|---|---|
| 01 | [Website audit](01-website-audit.html) | Flow, links, UX, graphic design, design system, responsive, contrast, hover, performance, SEO, forms and chat, security headers |
| 02 | [Indexing](02-indexing.html) | Current indexing signals and how to remove the site from search or keep it indexed |
| 03 | [App audit](03-app-audit.html) | Staff workspace: map, UX, accessibility, responsive, performance, security headers, design |
| 04 | [App click test](04-app-click-test.html) | Every control in the app and where it leads |
| 05 | [Design system](05-design-system.html) | The proposed system: color, type, space, components, states, charts, categories |
| 06 | [Prototypes](06-prototypes.html) | The prototypes and which findings each one answers |

Related files in this repository:

- `design-system/mobve-design-system.css`: the system's values and components.
- `design-system/index.html`: the design system reference page with live specimens.
- `design-system/prototype.html`: website and app prototype.
- `design-system/appointments.html`: Appointments screen prototype.
- `diagrams/web-flow.pdf` and `diagrams/app-flow.pdf` (with HTML versions): flow diagrams of the website and the app, also on the Miro board https://miro.com/app/board/uXjVESDiKo0=/

## Most important findings

### Website (mobve.com)

1. No working way to contact the company: the chat is down, the only form lives inside the chat, and contact.html links to a section (#waitlist) that does not exist.
2. The 60-second demo, the main call to action, does not work for visitors: its status API answers 401 or 503.
3. Draft and internal content is public: a "Private preview" banner, a link to an internal checklist (review.html), draft titles on pricing, privacy and terms.
4. The brand font is named but never loaded, so the site renders in the system font.
5. The design system is incomplete: 20 font sizes, many touch targets under 44 px, missing hover and pressed states, six different blues across site and app.

### Staff app

1. Settings, Resident requests fails to load, and its Try again button sends no request.
2. Appointments, Pipeline view: the heading and the Add appointment button are pushed past the right edge of a 1440 px screen.
3. Every page has the same browser title, and all Settings pages share the h1 "Settings".
4. Most text is 10 to 12 px and touch targets do not use the declared 44 px size.
5. Save buttons are enabled without changes on nine Settings pages, while others stay disabled until a change.

### Before launch

App links point to the staging host, the home page is indexable while the site is in testing, every file is served with no-store caching, and the public site has no HSTS or frame-ancestors header (the app has both).

## Proposed solution

A single design system for the website and the app (document 05), and prototypes that apply it (document 06):

- Color: six base colors (primary #0b63ce, secondary #ffc845, ink #101b2b, paper #ffffff, muted #536173, background #fafafa), three traffic-light semantic signals with a dark text each, five appointment category colors, and every state and tint calculated from these.
- Type: Inter Variable, nine roles, three weights, nothing under 12 px.
- Components with every state defined: hover, pressed, focus, disabled, loading, error.
- Patterns that fix specific findings: a contact form that does not depend on the chat, an honest unavailable state for the demo, a recommended pricing plan, larger chart legends, category colors that never read as status.

## Scope and limits

- Reviewed: the rendered website and app in the browser, the public website JavaScript (config.js, voice.js, site-chat.js, app.js read in full), HTTP headers, Lighthouse, performance traces.
- Not seen: the app's source code, the backend and its repository, Cloudflare and DNS settings, Search Console.
- Not tested: actions that save, send, download or end the session; other roles; populated data.
- The code security method was applied only to the public website files. A full code audit needs the repository.

## Tools and process

Chrome extension for browser automation (navigation, DOM and style inspection, scripts, hover, screenshots, console and network), browser DevTools tools (device emulation, Lighthouse, performance traces), command line (HTTP headers, redirects, files), Miro for flow diagrams. Method references: a design system checklist, an SEO audit framework, a graphic design foundations guide, a brand identity method (category color research), and a code security audit method applied in a limited way.
