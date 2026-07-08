# babarkkhan.com - Working Notes

Last updated: 8 July 2026 (copy overhaul from Babar's edited docx)

## Current state

Two-page static site on GitHub Pages (CNAME: babarkkhan.com).

- `index.html` - homepage. Positioning: **global executive and operator at the edge of technology and AI**. Sections: hero (positioning line + 3-sentence third-person bio, no stats block), credential ticker (now includes $150M+ and 20+ years), Current Roles, Invest/Build/Bridge, Five Lenses, Perspective teaser, contact CTA.
- `insights.html` - the "Perspective" page (renamed from thesis.html 8 Jul; visible label stays "Perspective"). Sections: Deep Tech x Applied AI thesis, Where I Invest (Biotech + AI Infrastructure), Track Record, How I Work (3 cards, last spans full width), CTA.
- Booking link everywhere: **https://cal.com/bkhan**
- Name: **Babar Khan** in nav/footer/body; the homepage `<title>`/OG/Twitter title use the full **Babar Khalid Khan** (Babar's choice in the docx). No em dashes anywhere in copy (hard writing rule).
- Assets: `photo-light.webp` / `photo-dark.webp` (hero, theme-swapped), `og-image.jpg` (1200x630 share card), `favicon.svg`, `apple-touch-icon.png`, `logos/` (local track-record logos; Clearbit is dead, never use it).
- `babarkkhan-website-copy.docx` - the editable copy doc shared with Babar; kept in the repo as the review surface. Latest version is his edited copy.
- Originals `photo-profile_white.JPG` and `photo-profile-dark.jpg` kept in repo as source material only; nothing references them.

## Done 8 Jul 2026 (copy overhaul from Babar's edited docx + 4 chat comments)

- Applied Babar's full copy rewrite from the edited docx: new hero bio, sharper pillar copy (Build/Bridge), all five lens entries rewritten in his voice, Where-I-Invest and How-I-Work rewritten, track-record role notes (Sonde "my first deal", Animoca "in closing"), new insights subtitle ("As a techno-optimist...").
- **Removed the stats block** from the hero ("seems gimmicky") and folded $150M+ / 20+ years into the ticker.
- **Removed leading zeros** from all numbered elements (pillars 1/2/3, lenses 1-5, invest cards 1/2).
- **Removed the Five Lenses subtitle** "One career, five vantage points".
- **Renamed thesis.html -> insights.html** (git mv; all hrefs + canonical + og:url updated). Visible "Perspective" label unchanged.
- Merged the old "Board governance" + "Founder mentorship" How-I-Work cards into one "Founder friendly + board governance" card that spans full width (`.value-card.span-full`).

## Judgment calls / assumptions to confirm

- **Recognition strip removed** from the homepage. It was absent from Babar's edited copy doc, so treated as intentional. MIT Innovators + 3 patents still live in the ticker; WEF/Milken + the degree line are now gone from the site. Easy to restore from git if wanted.
- **Truncated footnote completed.** Babar's doc ended mid-sentence with "Assess 50+ deep tech"; rendered as "Assess 50+ deep-tech opportunities a year." Confirm the intended number/wording.

## Parked / next time

- **Writing/ideas surface** ("Notes"/essays page). Note the page is now literally called `insights.html`, so a future essays section could live here or as a sibling. Highest-leverage future addition for the "edge of AI" positioning. Not started.
- Track-record logos are 128px favicons pulled from each company's site; fine at 48px display, but could be replaced with proper brand SVGs for crispness.
- Decide whether to delete the unreferenced original photos from the repo (they live in git history regardless).
- Optional SEO extras skipped as low-value for a 2-page site: sitemap.xml, robots.txt.

## Conventions (do not break)

- No em dashes in any copy. Use commas, periods, parentheses, or spaced hyphens.
- Zero build step, zero dependencies: hand-written HTML/CSS/JS only, Google Fonts is the sole external call.
- Dark mode: `data-theme="dark"` on `<html>`, persisted in localStorage key `bkk-theme`, shared across both pages. Hero photo swaps via data-light/data-dark attributes.
- The Perspective page file is `insights.html` (renamed from thesis.html on 8 Jul 2026). Keep the visible label "Perspective".
- Local preview: any static server from the repo root (the review sessions use `python -m http.server`).
