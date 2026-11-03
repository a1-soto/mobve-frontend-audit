# App audit: staff workspace

Date: 2026-11-03. Scope: the logged-in staff workspace on the staging host, role Owner, account Jackson Properties LLC. Method: read-only. Nothing was saved, sent, exported or deleted, and Log out was not used.

## 1. Summary

The app is more mature than the public site: fast (LCP 0.74 s, CLS 0.018, TTFB 134 ms), strong security headers, an accessible mobile drawer, labeled forms and table regions, semantic status tokens and a loaded brand font. Three real defects (items 1, 2 and 3 in section 4) and polish items remain.

## 2. App map

- Entry: public site, then /login. Any app URL without a session answers 307 to /login.
- Shell: sidebar (Dashboard, Maintenance Requests, Appointments, Call Log, Settings, Logout), header (company, property and building selectors, Emma AI, user menu), drawer on narrow screens.
- Dashboard: filters, 6 KPI cards, maintenance performance cards, charts, recent calls, Attention Required.
- Maintenance Requests: summary, pipeline by stage, filters, List, Board and Group by category views, Export CSV, detail page per request.
- Appointments: Overview (scorecards, Day, Week and Month schedule) and Pipeline (New to Won), Add appointment dialog, Attention required, Needs a time.
- Call Log: filters and empty state.
- Settings: overview with a setup checklist (17 percent) and 19 pages in six groups.
- Flow diagram: Miro board https://miro.com/app/board/uXjVESDiKo0=/

## 3. What works

- All 5 main routes and 19 Settings routes visited; 18 of 19 Settings pages load; no link leads nowhere.
- All /api calls observed answered 200 (the only 503 was the page request of Resident requests). No console errors.
- Clear breadcrumb, title and description on every screen; useful empty states; honest labels ("Collecting data", "Not connected").
- Dialogs and menus open with focus inside, close with Escape and return focus.
- Landmarks, skip link, aria-current, one h1 per page, labeled fields, wide tables in a labeled focusable scroll region.
- Contrast: of 196 text elements on the Dashboard, only the "—" placeholders fail (#a3a3a3 on white, 2.5:1).
- Responsive at 500 px: no horizontal overflow on Dashboard, Maintenance and Appointments; accessible drawer.
- Performance: TTFB 134 ms, FCP 236 ms, LCP 736 ms, CLS 0.018, 35 KB transferred, slowest API call 581 ms.
- Security headers: CSP with nonce and strict-dynamic, HSTS with preload, X-Frame-Options DENY, nosniff, COOP and CORP, no-store for private pages, 301 from http.
- Design tokens (18) including semantic status colors and a 44 px touch target; Inter Variable loaded.

## 4. What needs fixing

### Defects

1. Settings, Resident requests shows "This information could not be loaded". The page request returned 503, and Try again sends no new request.
2. Appointments, Pipeline at 1440 px: heading, Add appointment and "Updated" extend to 1612 px; the button (1329 to 1477 px) is partly off screen and the page does not scroll horizontally.
3. Every page has the same browser title "Mobve | Staff workspace", and all 19 Settings pages use the h1 "Settings".
4. Text size: most content is 11 to 12 px, labels 10 px, 9 px measured at 500 px.
5. Touch targets: about 20 elements per page under 44 px although a 44 px token exists.

### UX and polish

6. Full page loads show a blank "Checking legal acceptance..." screen (seen on Appointments; the legal-acceptance call runs on every load).
7. Hover: sidebar background changes to #f5f7f9 only; Delta, Reset filters and Emma AI show no change; no pressed state.
8. Required fields in Add appointment are not marked.
9. Empty KPI dashes in #a3a3a3 (2.5:1).
10. The request detail h1 is the internal code (CALL-0A8DB8A5).
11. Phone numbers are unformatted.
12. The week calendar header is wider than a 500 px screen.
13. call-answering is requested on every page change (about 20 times in the walk).
14. Dashboard and Maintenance show different date ranges without saying so.

### Expected in staging

Phone numbers and routing unavailable until provider verification; setup checklist at 17 percent; no usage events; empty call scorecards.

## 5. Scope

- Seen: the rendered app, computed styles, network calls and headers, at 500 px and 1440 px, role Owner, one account with mostly empty data.
- Not seen: the app source code and bundles, the backend, other roles and accounts, populated data. No security code audit of the app.
- Not verified: actions that write data, Lighthouse for the app (the automated tool runs without the session), keyboard-only and screen reader runs.

## 6. Corrections made during the audit

- A first check suggested unnamed controls on Team and access; the check was wrong.
- A request detail error came from a truncated test URL; the real link works.
