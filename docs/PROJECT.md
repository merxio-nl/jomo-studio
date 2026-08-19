# PROJECT.md

Verified facts about this repository only. No speculative architecture or
design decisions are recorded here.

## What this repository is

- This is the standalone repository for **JOMO Studio**, a founder-led
  digital studio brand (Yaroslav Redka, Tilburg, Netherlands) focused on
  website strategy, design, and development.
- JOMO Studio was originally built inside `merxio-nl/PORTFOLIO` (under a
  `v2/` subdirectory, alongside an unrelated legacy portfolio site) and
  was extracted into this standalone repository once it was
  production-ready. See `docs/DECISIONS.md` ADR-012 for the extraction
  itself, and the earlier ADRs for everything that happened before it.
- Languages: English (default, unprefixed route), Russian (`/ru/`), Dutch
  (`/nl/`) — all three are populated. Russian is the editorial source of
  truth; English and Dutch are independent, natural localizations of the
  same facts (see ADR-009).
- The site must support adding future projects/case studies — the content
  structure does not assume a fixed, small project count.

## Verified project facts

These are the real facts behind each case study on the site. Do not add
metrics, testimonials, or outcomes beyond what's recorded here without
new information from the repository owner.

### ALLROUND4YOU

- Real, delivered client project. Repository: `merxio-nl/allround4you`
  (public). Production domain (via repo `CNAME`): `allround4you.com` —
  also reachable at `merxio-nl.github.io/allround4you/`. HTTPS on the
  custom domain has previously returned a certificate error; HTTP
  resolves and serves the site.
- Client: ALLROUND4YOU Bouw & Service, a Dutch construction/renovation
  business, single tradesperson, 20+ years experience, no prior website.
- Static HTML/CSS/JS one-page site (not built with this project's own
  Astro stack — it's the client's separate delivered site).
- Full case-study facts (challenge, approach, solution, outcome, timeline,
  revisions) are recorded in `src/content/projects/*/allround4you.json`,
  sourced from the repo, the live site, and details the repository owner
  provided directly.

### Apaxic Towing

- Real towing business in Bonney Lake, Washington, US, live at
  `apaxictowing.com`. The live site's own title casing is "Apaxic LLC
  Towing"; this project uses "Apaxic Towing" to match common usage on the
  live site.
- The site is genuinely used commercially alongside search advertising —
  real customer inquiries, some converting to paid towing jobs. No lead
  counts, revenue, conversion rates, or ad-spend figures are known or
  should be invented.

### RugFlag

- Handmade rug studio, Netherlands. A bilingual (bespoke) site built
  outside this Astro stack. Focus is the visual/design work and client
  presentation — the owner does not currently rely on it as a major
  commercial channel. Do not state that on the public site, and do not
  invent commercial performance either; the case study focuses on the
  work itself.

### Universal Plug

- `merxio-nl/universal-plug`, live at `merxio-nl.github.io/universal-plug`.
  A heat-resistant cap accessory for DIY bottle hookahs (a smoking
  accessory) sold in NL/EU via Telegram/WhatsApp — not an electrical/plug
  product. Started as a small experiment and became a real small sales
  channel; some traffic comes from QR codes on printed cards tracked with
  UTM parameters. No order counts, revenue, or growth figures are known.

## Contact facts

- Email, WhatsApp, and Telegram are the current contact channels
  presented on the site (see `src/i18n/ui.ts` and `Footer.astro`/
  `ContactCta.astro` for exact current copy/links).
- Location: Tilburg, Netherlands.

## Development history

The site went through several owner-reviewed rounds while it lived inside
`merxio-nl/PORTFOLIO`. Kept here as real project history, not current
architecture:

- **Foundation.** Built with Astro (static output) + Tailwind CSS
  (build-time) + Astro Content Collections, replacing an old single-file
  static HTML predecessor. See `docs/DECISIONS.md` ADR-006.
- **Correction round #1.** Restructured the IA into two levels — a
  fast-scan Work overview and individual case-study pages — replaced the
  display typeface (Fraunces → Manrope), and added a working Russian
  translation. See ADR-007. Project order in the Work overview:
  ALLROUND4YOU, Apaxic Towing, RugFlag, Universal Plug.
- **Correction round #2.** Rewrote the JOMO philosophy copy to be
  positive rather than a "what we leave out" contrast, repositioned the
  Creator section (Russian uses "Директор JOMO Studio" per owner
  preference, not "Основатель"), and did a full Russian editorial pass.
- **Correction round #3.** UX compression pass: reordered the homepage,
  rewrote the hero to be direct and commercial, fixed a device-mockup
  percentage-`border-radius` bug (replaced with a fixed-pixel nested
  bezel), and reduced section padding/heading sizes throughout.
- **Typography refinement.** Replaced Manrope with Golos Text for
  display/heading roles and introduced the current role-based typography
  system (Display/H1/H2/H3/Lead/Body/Small/Eyebrow/Nav). See ADR-008.
- **EN/NL localization.** Russian was frozen as the approved editorial
  source; English was brought up to date and Dutch was fully localized
  and activated as a third live locale. The two-language nav switcher was
  replaced with the current three-way switcher. See ADR-009.
- **Production readiness audit.** Added the SEO/metadata foundation
  (canonical, hreflang, Open Graph, Twitter Card, sitemap, robots.txt),
  fixed a real WCAG AA contrast failure, a stale font reference, a
  render-blocking font stylesheet, and converted oversized PNG
  screenshots to WebP. See ADR-010.
- **Brand kit.** Formalized the existing JOMO visual identity (wordmark,
  mark, colors, fonts) into a dedicated `brand/` directory and wired the
  first Open Graph share image. See ADR-011.
- **Repository cleanup + Safari/anchor fixes.** Fixed a real Safari
  Favorites icon bug (alpha channel on `apple-touch-icon.png` — iOS/
  Safari doesn't honor transparency there) and a mobile anchor-scroll
  offset bug (added `scroll-padding-top` matching the sticky header
  height).
- **Standalone extraction.** Moved from `merxio-nl/PORTFOLIO`'s `v2/`
  subdirectory into this repository. See ADR-012.
