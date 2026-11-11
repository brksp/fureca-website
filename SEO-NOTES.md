# Golmodel search discovery changes

Prepared 5 November 2026 against commit `545db9d7edfc28d4580f4fe11750c5ab9a692c9f` of `brksp/fureca-website`.

## Custom domain (11 November 2026)

The site moved from `https://brksp.github.io/fureca-website/` to `https://golmodel.app/`. The domain is registered at Cloudflare; its DNS records point at GitHub Pages with the proxy off (DNS only), so GitHub issues the certificate. This change updates every canonical, hreflang, Open Graph, JSON-LD, language-switch and sitemap URL together and adds the `CNAME` file.

`robots.txt` now sits at the host root (`https://golmodel.app/robots.txt`), so the host-root section further down describes the old host only. In Search Console, add a Domain property for `golmodel.app` (verified with a DNS TXT record in Cloudflare) and submit `https://golmodel.app/sitemap.xml`.

## Changes ready for review

- Keep the existing English URL and visual system.
- Add a Turkish landing page at `tr/` and equivalent English/Turkish prediction guides.
- Add individual titles, descriptions, self-referencing canonical URLs, Open Graph, Twitter summary metadata and Smart App Banner metadata.
- Connect equivalent language versions with reciprocal `hreflang` links; English is the x-default.
- Include six public URLs in `sitemap.xml`.
- Add factual SoftwareApplication data on landing pages. No ratings or reviews are fabricated. This basic markup does not promise eligibility for Google's software-app rich result, which has additional requirements.
- Preserve privacy-policy and support body content. Preserve the existing performance figures but label them as a historical sample, rather than live accuracy.
- Replace the homepage's old Analyze-tab CTA with the current Results/team-following flow described in App Store version 1.4.0.
- Extract shared home-page styling to `assets/site.css`; keep language links visible on mobile.
- Fix the existing invalid `flex-wrap: gap` CSS declaration.

## Publishing

These changes are prepared for review, not a deployed release. Merge, deployment and Search Console submission remain separate steps. The site should continue using the existing GitHub Pages URL.

Review the diff before merging. Confirm that GitHub Pages publishes from this repository root. Deploy to the existing URL; do not create a second competing copy of the site on another host.

After deployment check these URLs return 200:

1. https://brksp.github.io/fureca-website/
2. https://brksp.github.io/fureca-website/tr/
3. https://brksp.github.io/fureca-website/how-it-works.html
4. https://brksp.github.io/fureca-website/tr/model-nasil-calisir.html
5. https://brksp.github.io/fureca-website/sitemap.xml

If a custom domain is adopted later, update every canonical, hreflang, Open Graph URL, JSON-LD URL and sitemap URL together, and implement redirects from the previous host. Buying a domain is not a prerequisite for this patch.

## robots.txt: host-root requirement

The live host-root `https://brksp.github.io/robots.txt` returned 404 during the audit. For Google, a 404 robots.txt normally means no crawl restrictions, not a crawl block.

`https://brksp.github.io/fureca-website/robots.txt` would not be the host's robots file. Do not add it here expecting it to manage crawlers. If a host-root robots file is wanted, publish/merge its rules through the account-level `brksp.github.io` site. Preserve rules for other projects on this host.

Suggested addition to that host-root file:

```text
User-agent: OAI-SearchBot
Allow: /fureca-website/

Sitemap: https://brksp.github.io/fureca-website/sitemap.xml
```

Do not overwrite an existing host-root file. Check inherited or explicit Googlebot/Bingbot rules separately. OAI-SearchBot access is independent from GPTBot training permissions. This patch makes no change to training permissions. The robots change is optional when the path is already allowed; it is not a ranking boost.

## Google Search Console

Requires the owner's account; not submitted during this work.

1. Add/select the URL-prefix property `https://brksp.github.io/fureca-website/`.
2. Complete ownership verification with the exact HTML tag or file supplied by Search Console. No verification token has been invented or committed.
3. In Sitemaps submit `sitemap.xml` after it is live.
4. In URL Inspection inspect the four landing/guide URLs above. Run Test Live URL, check accessibility and canonical information, then Request Indexing where available.
5. Follow Page indexing and Performance > Search results. A public `site:` search is not an authoritative index-status test.

Submitting a sitemap or requesting indexing does not guarantee indexing, position or a delivery date. Repeated requests do not create a ranking advantage. Do not use Google's Indexing API for these ordinary marketing pages.

## Measuring visits through to downloads

No new analytics SDK, cookies or third-party measurement were added to the website by this patch.

- Create real campaign links in App Store Connect > Analytics > Acquisition > Campaigns, for example `web_en_home`, `web_tr_home`, `web_en_guide`, `web_tr_guide`.
- Copy the generated links (including the account's real provider token) into the corresponding CTA hrefs. Do not invent a `pt` token or treat a bare `ct`/UTM parameter as verified install attribution.
- When intentionally adding web analytics, collect outbound App Store clicks and landing-page/referrer dimensions in a web stream. Keep developer traffic and the iOS app stream separable; align the privacy notice with the actual implementation.
- Compare Search Console non-brand clicks, campaign-attributed first-time downloads and, once production analytics is clean, team follows and returning users. App Store privacy thresholds and attribution windows can leave small campaigns unreported.

## Validation performed

All six HTML pages were checked for a unique title, description, H1, expected canonical, parseable JSON-LD, internal links, local assets and fragment targets. The two language pairs were checked for correct languages and reciprocal hreflang links. Sitemap XML parses and contains six distinct URLs. Browser rendering, Search Console access, rich-result eligibility and post-deployment crawler access are not verified by these checks.

## Sources

- https://developers.google.com/search/docs/crawling-indexing/sitemaps/build-sitemap
- https://developers.google.com/crawling/docs/robots-txt/robots-txt-spec
- https://developers.google.com/search/docs/specialty/international/localized-versions
- https://developers.google.com/search/docs/appearance/ai-features
- https://developers.google.com/search/docs/appearance/structured-data/software-app
- https://developers.openai.com/api/docs/bots
- https://developer.apple.com/help/app-store-connect-analytics/acquisition/campaign-links
