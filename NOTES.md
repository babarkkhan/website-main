# babarkkhan.com - Working Notes

Last updated: 6 July 2026 (repositioning release, commit 974b33b)

## Current state

Two-page static site on GitHub Pages (CNAME: babarkkhan.com).

- `index.html` - homepage. Positioning: **global executive and operator at the edge of technology and AI**. Sections: hero (with stats), credential ticker, Current Roles, Invest/Build/Bridge, Five Lenses, Recognition, Perspective teaser, contact CTA.
- `thesis.html` - the "Perspective" page (kept the filename to preserve inbound links). Sections: Deep Tech x Applied AI thesis, Where I Invest, Track Record, How I Work, CTA.
- Booking link everywhere: **https://cal.com/bkhan**
- Name everywhere: **Babar Khan** (PhD where relevant). No em dashes anywhere (hard writing rule).
- Assets: `photo-light.webp` / `photo-dark.webp` (hero, theme-swapped), `og-image.jpg` (1200x630 share card), `favicon.svg`, `apple-touch-icon.png`, `logos/` (local track-record logos; Clearbit is dead, never use it).
- Originals `photo-profile_white.JPG` and `photo-profile-dark.jpg` kept in repo as source material only; nothing references them.

## Done 6 Jul 2026 (full review + repositioning)

All decisions from the review session were implemented:

- Repositioned from "Senior Investment Leader" to global executive/operator (hero eyebrow, positioning line, third-person bio, title tags, meta).
- Ticker: executive credentials replaced the residency/visa list.
- Consolidated Focus Areas + Differentiation + process diagram into Invest/Build/Bridge.
- Five-lens story (Technologist / Scientist / Operator / Capital Deployer / Connector) moved from thesis to homepage. PIF Governor name-drop generalized to "sovereign investment committees at the highest level".
- Recognition strip added (MIT TR Innovators Under 35 2019, 3 US patents, WEF & Milken, KAUST PhD / Rutgers MS).
- Thesis page reframed as "Perspective"; "Value-Add Beyond Capital" renamed "How I Work"; linked from homepage nav + teaser band (was fully orphaned before).
- Contact CTA: "Building something at the frontier?"
- Fixed: broken Clearbit logos (now local files), 2.6 MB hero photo (now ~230 KB WebP), duplicate .JPG.JPG deleted, undefined --white CSS var, Reclaim/Cal.com link inconsistency, name inconsistency between pages.
- Added: OG/Twitter cards, favicon, apple-touch-icon, canonical URLs, meta descriptions on both pages, JSON-LD Person schema.
- Accessibility: noscript fallback for the visibility-hidden FOUC guard, :focus-visible styles, prefers-reduced-motion (kills marquee + animations), marquee pauses on hover.

## Parked / next time

- **Writing/ideas surface** ("Notes" page with 2-3 short essays on AI + Gulf capital). Agreed as the highest-leverage future addition for the "edge of AI" positioning. Not started.
- Track-record logos are 128px favicons pulled from each company's site; fine at 48px display, but could be replaced with proper brand SVGs for crispness.
- Decide whether to delete the unreferenced original photos from the repo (they live in git history regardless).
- Optional SEO extras skipped as low-value for a 2-page site: sitemap.xml, robots.txt.

## Conventions (do not break)

- No em dashes in any copy. Use commas, periods, parentheses, or spaced hyphens.
- Zero build step, zero dependencies: hand-written HTML/CSS/JS only, Google Fonts is the sole external call.
- Dark mode: `data-theme="dark"` on `<html>`, persisted in localStorage key `bkk-theme`, shared across both pages. Hero photo swaps via data-light/data-dark attributes.
- Keep `thesis.html` filename even though the page is titled "Perspective".
- Local preview: any static server from the repo root (the review sessions use `python -m http.server`).
