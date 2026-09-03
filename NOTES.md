# babarkkhan.com - Working Notes

Last updated: 3 September 2026 (accessibility + structure pass)

## Done 3 Sep 2026 (accessibility, dark mode, heading structure)

Audit pass on both pages: headless render at 1440/820/390px in both themes,
WCAG contrast on every colour pair, asset and heading-outline checks.

- **Light-mode contrast now passes AA.** Darkened two light-theme tokens:
  `--teal` `#1B8C6E` -> `#17775D`, `--ink-soft` `#6B7A99` -> `#63718F`. Every
  accent label, tag and meta line was between 3.86:1 and 4.31:1 before; all
  now clear 4.5:1. Also raised white-on-navy text: footer `.35` -> `.55` on
  both pages, invest-card number `.4` -> `.6`, CTA icon links `.45` -> `.6`.
  Dark theme already passed everywhere and is untouched.
- **Track-record logos fixed in dark mode.** The dark override swapped the
  white logo tile for a dark one; BlueNalu and Paradromics are dark marks
  with no light variant and were invisible. Tile now stays white in both
  themes. (Still worth replacing the 128px favicons with real brand SVGs.)
- **Perspective link restored in the mobile nav.** It was `display: none`
  below 600px, leaving the second page unreachable from the nav on phones.
  Nav is compacted instead (smaller logo/icons, extra step below 370px).
  Verified no overlap or horizontal scroll from 320px up.
- **Heading outlines rebuilt on both pages, with zero copy changes.** Five
  Lenses had no heading at all and the Perspective page's three sections
  ("Where I Invest", "Track Record", "How I Work") were `<p>` eyebrows, so
  the page outline was h1 -> Biotech -> AI Infrastructure -> Let's connect.
  Section labels without a display line are now `<h2>`; card and item titles
  are `<h3>`/`<h4>` beneath them.
- **Dark-mode invest cards are two-tone again.** Header and body were both
  `#161B22`, flattening the card. Body lifted to `#1A212B`, header dropped to
  `#0D1117` with a teal bottom border.

## Done 3 Sep 2026 (copy decisions from Babar)

- **No email on the site, deliberately.** Babar does not want a published
  address (spam). Contact is LinkedIn + cal.com only. Do not add a mailto.
- **"Multiple US Patents"** everywhere. The ticker said "3 US Patents" while
  Lens 2 said "multiple"; "multiple" wins. Both ticker copies updated.
- **Animoca Brands removed** from the track record. That deal is off. Card,
  its logo file, and the "Investor (in closing)" line are all gone; the grid
  is now 4 columns (2x2 on mobile). Do not reinstate.
- **Sonde Health role note removed** ("my first deal, ran it end-to-end
  except sourcing"). The card now carries no role line while the other three
  do, so `.track-card` centres its content vertically to keep the omission
  looking deliberate. **Open:** whether Sonde should get a neutral role
  label instead. Nothing invented in the meantime.
- **"Assess 50+ deep-tech opportunities a year" deleted** from the track
  footnote. This resolves the July truncation question: the sentence is
  gone rather than completed.
- **Recognition strip stays removed** (WEF/Milken, degree line). Confirmed
  intentional, not an oversight.

### Known, not yet fixed

- `.hero-photo` animates `fadeIn ... forwards`, which ends at `opacity: 1`
  and permanently overrides both the base `0.75` and the dark-mode `0.85`.
  Those values now only apply to `prefers-reduced-motion` users, who see a
  visibly different hero. Decide the intended final opacity, then reconcile.
- **Credentials live only in the ticker**, which is `aria-hidden="true"`
  (correct for a marquee). $150M+, MIT Innovators Under 35, multiple US
  patents and 4 board roles therefore reach no screen reader and no search
  engine, and a sighted visitor only catches them mid-scroll. Removing the
  stats block was right; these facts still need a non-decorative home.
  Recommendation pending Babar's call.
- **Mobile hero.** Stacked, the photo sits below name + positioning + a
  nine-line bio, renders at `70vw` with `object-position: center 15%`, and
  is cropped to the top of the head below the fold. The two hero images are
  also different aspect ratios (1600x1700 light, 1600x1970 dark), so the
  crop shifts when the theme is toggled.
- Two stale remote branches (`claude/pricing-sensitivity-calculator-Bkl6J`,
  `claude/switch-opus-4.6-y35dr`) both predate the July overhaul and still
  carry `thesis.html`. Delete them so they are not mistaken for newer work.

---

Previously updated: 8 July 2026 (copy overhaul from Babar's edited docx)

## Current state

Two-page static site on GitHub Pages (CNAME: babarkkhan.com).

- `index.html` - homepage. Positioning: **global executive and operator at the edge of technology and AI**. Sections: hero (positioning line + 3-sentence third-person bio, no stats block), credential ticker (now includes $150M+ and 20+ years), Current Roles, Invest/Build/Bridge, Five Lenses, Perspective teaser, contact CTA.
- `insights.html` - the "Perspective" page (renamed from thesis.html 8 Jul; visible label stays "Perspective"). Sections: Deep Tech x Applied AI thesis, Where I Invest (Biotech + AI Infrastructure), Track Record (4 companies since Animoca was removed 3 Sep), How I Work (3 cards, last spans full width), CTA.
- Booking link everywhere: **https://cal.com/bkhan**
- Name: **Babar Khan** in nav/footer/body; the homepage `<title>`/OG/Twitter title use the full **Babar Khalid Khan** (Babar's choice in the docx). No em dashes anywhere in copy (hard writing rule).
- Assets: `photo-light.webp` / `photo-dark.webp` (hero, theme-swapped), `og-image.jpg` (1200x630 share card), `favicon.svg`, `apple-touch-icon.png`, `logos/` (four local track-record logos; Clearbit is dead, never use it).
- `babarkkhan-website-copy.docx` - the editable copy doc shared with Babar; kept in the repo as the review surface. Latest version is his edited copy.
- Originals `photo-profile_white.JPG` and `photo-profile-dark.jpg` kept in repo as source material only; nothing references them.

## Done 8 Jul 2026 (copy overhaul from Babar's edited docx + 4 chat comments)

- Applied Babar's full copy rewrite from the edited docx: new hero bio, sharper pillar copy (Build/Bridge), all five lens entries rewritten in his voice, Where-I-Invest and How-I-Work rewritten, track-record role notes (since removed, see 3 Sep entry), new insights subtitle ("As a techno-optimist...").
- **Removed the stats block** from the hero ("seems gimmicky") and folded $150M+ / 20+ years into the ticker.
- **Removed leading zeros** from all numbered elements (pillars 1/2/3, lenses 1-5, invest cards 1/2).
- **Removed the Five Lenses subtitle** "One career, five vantage points".
- **Renamed thesis.html -> insights.html** (git mv; all hrefs + canonical + og:url updated). Visible "Perspective" label unchanged.
- Merged the old "Board governance" + "Founder mentorship" How-I-Work cards into one "Founder friendly + board governance" card that spans full width (`.value-card.span-full`).

## Judgment calls from July - all resolved 3 Sep 2026

- **Recognition strip removed** from the homepage. Confirmed intentional by
  Babar on 3 Sep; WEF/Milken and the degree line stay off the site.
- **Truncated footnote.** Babar's doc ended mid-sentence with "Assess 50+
  deep tech" and it had been rendered as "Assess 50+ deep-tech opportunities
  a year." Resolved 3 Sep: the sentence is deleted, not completed.

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
