# babarkkhan.com - Working Notes

Last updated: 3 September 2026 (dark-only simplification; merged and live on main)

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

## Done 3 Sep 2026 (dark only; light theme and toggle removed)

Babar wants the site simplified while he works on something else: **dark mode
only, no switch.** He may reinstate light mode later, so nothing was thrown
away that would be expensive to rebuild.

- The dark palette is now the sole `:root`. The `[data-theme="dark"]` block
  is gone and its 34 overrides were folded into the base rules, using tokens
  rather than the hard-coded hexes they carried.
- Removed: the toggle button in both navs, `applyTheme` / `toggleTheme`, the
  `bkk-theme` localStorage key, and the `html { visibility: hidden }` plus
  inline head script that existed only to stop a theme flash. That last one
  also removed a real failure mode: if the inline script had ever been
  blocked, the page would have stayed blank.
- Added `<meta name="color-scheme" content="dark">` so form controls and
  scrollbars match.
- Dead tokens dropped: `--white`, `--white-rgb`, `--line-teal` (index),
  `--teal-bright` (insights). Theme cross-fade transitions on `body`, `nav`
  and the blanket card rule are gone; each card keeps its own hover
  transition. Removing the blanket rule also restored `.pillar-card`'s
  transform transition, which the blanket rule had been clobbering.
- JavaScript on both pages is down to the four-line IntersectionObserver.
  index.html 29.2 -> 24.3 KB, insights.html 27.4 -> 22.8 KB.

**`photo-light.webp` is kept but unreferenced.** The hero uses
`photo-dark.webp` directly (no `data-light`/`data-dark` swap). Both files are
the same 1480x1572 aligned crop, so restoring light mode is just wiring the
swap back up.

Verified by pixel-diffing full-page dark screenshots before and after: the
two pages are **identical outside the nav band**, where the toggle used to
be. The CSS fold and the token cleanup were each diffed separately and came
back pixel-identical.

One regression caught during this work: the rule that removed `.theme-toggle`
CSS also matched three combined selectors of the form
`.nav-icon, .theme-toggle { ... }`, which silently took the mobile
`.nav-icon` sizing with it and grew the nav from 52px to 66px tall. Restored
as `.nav-icon`-only rules and re-verified from 320px up.

### If light mode comes back

Reintroduce a `[data-theme="light"]` token block, re-add the toggle button
and the small theme script, and restore the hero `data-light`/`data-dark`
swap. Every value needed is in this file's 3 Sep entries and in git history
at `4890518`.

## Done 3 Sep 2026 (type scale: 12px floor)

Babar's rule: **nothing below 12px anywhere on the site.** Readability and
scannability come first. Sixteen declarations were under that floor.

Full scale now in use (fluid clamps on the big heads are unchanged):

| px | used for |
|----|----------|
| 12 | mobile-only steps: `.nav-link`, `.nav-back`, `.creds-item` |
| 13 | uppercase micro-labels: section/band/persp labels, `.ts-label`, `.band-org`, `.creds-item`, `.track-meta`, `.track-role`, `.footer-r`, nav links |
| 14 | page eyebrows: `.eyebrow`, `.thesis-eyebrow` |
| 15 | small copy and buttons: `.invest-card-sub`, `.invest-item-title`, `.value-title`, `.track-footnote`, `.persp-btn`, `.contact-btn`, footer |
| 16 | body copy and numbered markers: `.pillar-card p`, `.band-sub`, `.persp-sub`, `.invest-item-body`, `.value-body`, `.track-name`, `.pillar-num`, `.lens-label span` |
| 17 | lead copy: `.hero-bio p`, `.lens-body`, `.contact-lede`, `.thesis-cta-sub` |
| 18 | `.invest-card-num`, `.thesis-subtitle`, `.nav-logo` |
| 22-26 | card and lens titles |

Specifically fixed from Babar's notes:

- **The 1 / 2 on the invest cards** were 11px, smaller than the 14px copy
  they labelled. Now 18px, larger than the 15px sub beneath them.
- **"Perspective"** (`.thesis-eyebrow`) 11px -> 14px, and every other
  eyebrow with it.
- **Track record** was the smallest block on the site: names 13 -> 16px,
  sector/stage meta and role 11 -> 13px, footnote 14 -> 15px.

Two layout consequences that had to be handled:

- `.track-grid` used `1fr` tracks, which cannot shrink below their widest
  word. At 16px "Bioindustries" pushed the grid 2px past the viewport at
  320px. Tracks are now `minmax(0, 1fr)`, `.track-name` gets
  `overflow-wrap: break-word`, and card padding tightens below 480px.
  "Series A/B" uses a non-breaking space so the letter never orphans.
- The mobile nav lost its slack once `.nav-link` went 10px -> 12px. The
  tight-nav breakpoint moved from 370px to 385px (375px is a very common
  width and had none) and that block now also trims the logo, icon sizes,
  gaps and nav padding. Re-verified from 320px up with deliberately wider
  substitute fonts: no overlap, no wrap, no horizontal scroll.

Contrast was re-checked after the resize; all pairs still clear 4.5:1.

## Done 3 Sep 2026 (static credentials, hero opacity, hero framing)

- **The scrolling marquee is gone.** Replaced by a static `<ul class="creds">`
  strip. Because it no longer moves it is real content, so `aria-hidden` was
  dropped and the credentials finally reach screen readers and search
  engines. `.ticker-*` CSS and `@keyframes marquee` are deleted. MIT now
  carries its date, "MIT Innovators Under 35 (2019)", and "35+ Countries
  Explored" was added. Eight items after Babar trimmed "Sovereign Capital",
  "Frontier AI" and "Riyadh / New York": two rows of four on desktop, five
  lines on phones (tighter type below 600px). No separators, since dots
  stranded themselves at the start of wrapped lines; alternating teal/grey
  and a 32px column gap do the separating. "35+ countries" was dropped from
  Lens 5 so the fact lives in one place only, the strip.
- **Hero opacity is consistent again.** `--hero-opacity` (0.75 light /
  0.85 dark) is now a token, and `@keyframes fadeIn` animates *to* that
  token instead of to a hard `1`. Verified all four combinations of theme x
  `prefers-reduced-motion` land on the same value, and that the value
  re-resolves correctly when the theme is toggled at runtime.
- **Hero photos re-cropped to a common frame.** They were 1600x1700 (light)
  and 1600x1970 (dark) with different subject scales, so the crop jumped on
  every theme toggle. Both are now 1480x1572 with the subject at the same
  scale and position (detected by background-differencing, then cropped to
  match: subject centre 45.4%, head top 8.3%). Neither was upscaled.
  Originals remain in git history.
- **Mobile hero reworked.** The photo now leads on phones (`order: -1`), is
  taller (78vw), clears the fixed nav rather than being clipped by it, and
  its bottom fade drops from 280px to 110px so it does not swamp a short
  frame. Face and name are above the fold; previously the photo sat below a
  nine-line bio, cropped to the forehead. DOM order is unchanged, so
  reading and tab order are unaffected.

### Known, not yet fixed

- Nothing outstanding from the 3 Sep pass.

---

Previously updated: 8 July 2026 (copy overhaul from Babar's edited docx)

## Current state

Two-page static site on GitHub Pages (CNAME: babarkkhan.com).

- `index.html` - homepage. Positioning: **global executive and operator at the edge of technology and AI**. Sections: hero (positioning line + 3-sentence third-person bio, no stats block), static credentials strip (8 items; replaced the scrolling ticker 3 Sep), Current Roles, Invest/Build/Bridge, Five Lenses, Perspective teaser, contact CTA.
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
- **No font size below 12px, anywhere.** Numbered markers must be at least as large as the copy they label.
- Zero build step, zero dependencies: hand-written HTML/CSS/JS only, Google Fonts is the sole external call.
- **Dark only** since 3 Sep 2026. No theme toggle, no `data-theme`, no localStorage. The hero uses `photo-dark.webp` directly.
- The Perspective page file is `insights.html` (renamed from thesis.html on 8 Jul 2026). Keep the visible label "Perspective".
- Local preview: any static server from the repo root (the review sessions use `python -m http.server`).
