# Indexing: status and how to change it

Date: 2026-11-03. Scope: mobve.com and the staging app host. Context: the site is the real domain, deployed for testing.

## 1. What was found

- Home (/ and /index.html): robots, googlebot and bingbot meta set to "index,follow,max-image-preview:large,max-snippet:-1". No X-Robots-Tag header. Self-referencing canonical. Googlebot receives 200 and the full page. The home is fully eligible to be indexed.
- Inner pages: "noindex,nofollow" in the meta tag, and also in an X-Robots-Tag header (confirmed on security, pricing, contact and review).
- robots.txt allows everything and announces the sitemap. sitemap.xml lists only the home, without lastmod.
- A google-site-verification tag is present, so a Search Console property was probably created. Its data could not be read.
- Staging app host: login and register have a noindex meta tag; there is no robots.txt and no X-Robots-Tag header.
- Variants: http answers 302 to https; https://www.mobve.com answers 404.

Is it indexed today? A public web search for "site:mobve.com" returned nothing, but that is weak evidence. Confirm in Search Console (URL Inspection, Pages report) or with a site: search in Google.

Risk: the home asks to be indexed while it shows draft pricing and a demo that does not work. A search snippet could show that under the real brand.

## 2. Option A: keep it out of the index while testing (recommended until launch)

Do not block crawling first: a blocked page never shows Google its noindex.

1. Set the three robots meta tags on the home to "noindex,nofollow".
2. Add an X-Robots-Tag "noindex, nofollow" response header for the whole site in Cloudflare (Transform Rules), so it can be turned off in one place.
3. Remove the Sitemap line from robots.txt and empty or remove sitemap.xml. Keep "Allow: /".
4. Add the same header to the staging app host.
5. If already indexed: Search Console Removals, prefix https://mobve.com/ (about 6 months while the noindex stays). Bing Webmaster Tools, Block URLs.
6. Verify with URL Inspection ("Excluded by noindex tag") and with curl -sI https://mobve.com/.
7. Optional, after the pages drop out: put the test site behind Cloudflare Access, basic auth or an IP allowlist.

## 3. Option B: keep it indexed and up to date

1. Remove draft text from snippets, or mark it with data-nosnippet, or limit snippets with max-snippet:160.
2. Make the demo state honest.
3. Fix variants: 301 from www and from http.
4. For each page that should rank: index,follow, self canonical, unique title (50 to 60 characters) and description (150 to 160), Open Graph, schema (Organization, FAQPage, Offer when prices are approved).
5. Sitemap with every indexable URL and real lastmod; submit it in Search Console and Bing.
6. After changes: update lastmod, request indexing for the changed URL, use IndexNow for Bing; removed pages return 404 or 410; moved pages keep a 301 for a year.
7. Monitor the Pages and Performance reports, Core Web Vitals and structured data.

## 4. Switching from testing to launch

1. Remove the X-Robots-Tag rule.
2. Set the chosen pages to index,follow with clean metadata.
3. Remove the preview banner and the Review notes link.
4. Add all indexable pages to the sitemap and restore the Sitemap line.
5. Fix www and http redirects.
6. Submit the sitemap and request indexing for the home, pricing and contact.

## 5. Recommendation

Option A until launch, then section 4. First confirm in Search Console whether the home is already indexed, and who owns that property.
