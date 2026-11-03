# Website audit: mobve.com

Date: 2026-11-03. Scope: the public website (home and 11 inner pages), the exits to the app, the front-end code the site serves, performance, SEO, graphic design, design system, responsive and hover behavior.

Context confirmed by the owner: mobve.com is the real site, deployed for testing. Section 2 lists defects that are real at any stage. Section 3 lists items that are expected in a test deployment and must be closed before launch.

## 1. What works

### 1.1 Flow and links

- All 11 inner pages answer 200 with a correct title and a single h1: security, contact, privacy, pricing, integrations, about, brand, terms, accessibility, credits, review.
- Every anchor used on the home exists (demo, pricing, portfolios, property-life, faq, top, main), and so do the pricing anchors (essentials, ai_operations, portfolio, enterprise).
- Unknown routes return a real 404. /index.html answers 200 as a duplicate of / and the canonical covers it.
- The four plan buttons carry the plan in the URL (register?plan=...), so the app can pre-select it.
- The app login loads, with labeled fields and correct autocomplete.
- The mobile menu closes after choosing a link and with Escape, and returns focus to its button.

### 1.2 UX and accessibility

- Lighthouse Accessibility 100 on desktop and mobile. Skip link, landmarks, html lang, one h1 per page.
- No icon-only control without an accessible name. Every image has alt text, the logo link included.
- Visible focus styles, no outline removed, prefers-reduced-motion handled, dvh used.
- Tabs use arrow, Home and End keys. FAQ uses native details. Plan dialogs use the native dialog element.
- Demo consent checkbox required before a call. Pricing table in a scrollable region with caption and scoped headers.

### 1.3 Graphic design

- Strong hierarchy in the hero: two-tone headline, one primary button, one secondary link, a supporting image with a data card.
- Coherent real photography with credits and honest "illustrative" labels.
- Restrained palette with generous spacing and a fixed maximum width.
- The primary button is identical everywhere and has a clear hover (darker fill, 1 px lift, 0.2 s).
- Calm, plain product voice. Fictional data labeled as fictional.

### 1.4 Performance

- LCP 1.97 s on a cold desktop load, 0.65 s on mobile emulation (Fast 4G, 4x CPU). CLS 0.00 on load and over a full scroll. No long tasks.
- 13 KB JavaScript, 15 KB CSS, 598 DOM nodes, 21 requests. Server answers in 61 to 88 ms when measured directly.

### 1.5 SEO and technical

- Home: title 52 characters, description 157 characters, canonical, Open Graph and Twitter cards, JSON-LD (Organization, WebSite). Lighthouse SEO 100.
- robots.txt and sitemap.xml valid. Search Console verification tag present.
- Strict Content-Security-Policy, nosniff, referrer-policy no-referrer, permissions-policy limiting the microphone. Served through Cloudflare over HTTP/2.
- Public front-end code: no secrets in config.js, dynamic text inserted with textContent, audio payload size limits, a request id against duplicate leads, provider codes validated with a strict pattern.

## 2. Real defects (any stage)

### High

1. Dead link: about.html and contact.html link to mobve.com/#waitlist ("Request early access"). The section does not exist on the home, so the click lands at the top with no message.
2. Cloudflare script blocked by the site's own policy: on every load an inline Cloudflare script (window.__CF$cv$params) is blocked by script-src 'self'. One console error, one Issues entry and one 401 request error appear on every visit, and Lighthouse Best Practices drops to 92. Fix: disable that Cloudflare feature or allow it with a hash (validate in the Cloudflare dashboard).
3. The brand font is not delivered: the CSS names Inter but there is no @font-face and no font file, so the page uses the system font. Weights 550, 620, 650 and 750 collapse to the nearest available weight.
4. The floating "Ask Mobve" button (64 x 87 px, fixed bottom right) covers body text at 320, 390 and 768 px, with its label directly over content.

### Medium

5. Type scale: 20 font sizes from 9 to 56 px and 8 weights. Text of 8 to 10 px in the hero eyebrow, photo captions and the hero data card (measured on mobile). Minimum should be 12 px.
6. Touch targets under 44 px: 27 elements on desktop and 22 on mobile (nav links 21 px high, Log in and Sign up 28 to 32 px, footer links 36 px, consent checkbox 18 px, privacy notice link 13 px, "Compare all plan details" 14 px).
7. Design system incomplete: 11 CSS tokens, no semantic colors, no type, radius, shadow or motion tokens; 9 border radii and 21 text colors in use; button styles differ between home and inner pages.
8. Hover and pressed states: no :active rule anywhere. Footer links, FAQ questions, language buttons and the chat launcher show no hover change.
9. The 8 property-type cards look like cards but are not links or buttons, and each repeats the label "PROPERTY OPERATIONS".
10. Heading structure: footer column titles and the "Everything in ..." lines in pricing are h2.
11. Pricing has four equal cards and no recommended plan. FAQ has only 4 questions and uses the default triangle while pricing uses a "+" for the same pattern. The footer has no contact details, address or legal entity.
12. Inner pages have no main navigation, and container widths vary (about 820 px for text pages, about 1,080 px for pricing).
13. Images: 150 to 300 KB JPEGs, about 1.5 MB avoidable on mobile. The logo PNG is 856 px wide and shown at 70 to 164 px. width and height attributes do not match the real aspect ratio of several portfolio images.
14. Redirects: www.mobve.com returns 404 and http to https uses 302.
15. The pricing table scroll region on mobile is not keyboard focusable and has no label.

### Responsive

16. Text under 12 px on mobile (hero card, caption, eyebrow).
17. The desktop navigation is hidden up to at least 768 px, so tablets get the hamburger although there is room for six links.
18. The hero headline leaves "next." alone on its line at 320 and 768 px.

### Contrast

19. Hero text over the photo passes today but is fragile: measured against the real pixels the headline reaches at least 3.97:1 (large text needs 3:1) and the caption 7.2:1. A lighter photo would fail. Fix: a solid dark scrim and a caption of at least 12 px.

### Low

20. Menu, language, demo and chat buttons use type="submit" outside a form.
21. The portfolio carousel repeats 8 images; confirm the copies are hidden from screen readers.
22. The phone field in the lead form accepts letters.

## 3. Pre-launch checklist

1. Contact path: the chat is down ("Chat is unavailable right now"), the only form is inside the chat, and contact.html has no form, email or phone.
2. Demo: /api/demo/voice/status answers 401 (sign_in_required) and sometimes 503, while Call Now still looks active.
3. Private preview content: banner "Private preview, Draft material for review", "Review notes" link to review.html, "Before this page goes public" on contact.html, draft titles on pricing, privacy and terms.
4. App links point to the staging host. Switch to the production app host.
5. Indexing: see the indexing document.
6. Caching: every response is sent with Cache-Control no-store, so each visit downloads about 2 MB.
7. Security headers: no Strict-Transport-Security, no frame-ancestors or X-Frame-Options, no Cross-Origin-Opener-Policy. The app sends all of them.
8. Inner page metadata and sitemap need clean titles, descriptions and entries when they go public.
9. Staging app host: login and register are noindex only through a meta tag; add an X-Robots-Tag header.

## 4. Hover test (computed styles on real hover)

| Element | Result |
|---|---|
| Nav links | Color changes, no transition |
| Primary buttons | Fill darkens, 1 px lift, 0.2 s. Consistent |
| See how it works, Log in | Color or underline changes, no transition |
| Scenario tab | Lifts 2 px, no color change |
| See all features | Very subtle color shift |
| Language toggle, FAQ question, footer link, chat button | No visible change |
| Property cards | Not interactive |

## 5. Performance and SEO detail

- Desktop cold load: LCP 1,974 ms (hero image); the 1.8 s server time in that trace was a cold connection, direct measurement gives 61 to 88 ms.
- Weight: 1,991 KB transferred, of which 1,964 KB images.
- Lighthouse: Accessibility 100, SEO 100, Best Practices 92 (the CSP-blocked Cloudflare script and the 401 status request).
- Only the home is indexable; there are no solution pages, use cases or blog. The Spanish switch only changes the demo language, so hreflang is not needed today. No llms.txt; FAQ has no FAQPage schema.

## 6. Forms and chat

The only form is the "Request team contact" lead form inside the chat. Opening the chat started a real session request that failed. Without a session the form cannot be opened and nothing was submitted. Validation was checked on the form definition without sending: required name, email and consent; native email check; maximum lengths 100, 254, 35 and 500; choosing Phone makes the phone required.

How the chat should be tested (in a test environment or with approved test data): start, send a message, empty and 800-character messages, 2-minute idle, contact form with empty, invalid and valid data, duplicate submit, network failure, keyboard and screen reader, retention text, cleanup of the test lead.

## 7. Scope

- Code read in full: config.js, voice.js, site-chat.js, app.js. Read in part: styles.css. Downloaded but not read: demo-data.js, portfolios-carousel.js, site-chat.css, audio-capture.js.
- Not seen: server code, repository, Cloudflare and DNS settings, Search Console. The backend was not probed.
- Not verified: the voice call, chat messages and lead submission, keyboard-only and screen reader runs, landscape, print.

## 8. Corrections made during the audit

- review.html is linked from the banner of the inner pages, not from the home.
- No hreflang is needed: the Spanish switch only affects the demo.
- The empty footer link is the logo image, which has alt text.
- One Cloudflare script is blocked per load, not two.
- Draft banners, staging links and the non-working demo moved to the pre-launch list once the owner confirmed the site is a test deployment.
