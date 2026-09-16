# hps.eastwood.global

Eastwood Global x High Performance Systems partnership landing page.
Static site. No build step, no framework, no package manager.

## Contents

```
index.html          the entire page: markup, CSS and JS in one file
CNAME               hps.eastwood.global
.nojekyll           tells GitHub Pages to serve /assets untouched
assets/
  lockup.png        Eastwood Global + HPS co-brand lockup
  hero.webp         hero photography
  study.webp        partnership section
  violin.webp       "not only athletes" band
  tennis.webp       partner section, and the duotone bento band
  piano.webp        "what is included" bento tile
  chess.webp        closing call to action
  og-eg-hps.png     1200x630 social share card
```

## Deploy

1. Push this folder to the repo root of the GitHub Pages repository.
2. Repo Settings > Pages > Source: Deploy from branch, `main`, `/ (root)`.
3. Custom domain: `hps.eastwood.global`. The `CNAME` file already sets this.
4. Tick **Enforce HTTPS** once the certificate is issued. This can take up to an hour.

## DNS (for IT)

Add one record at GoDaddy on the `eastwood.global` zone:

| Type  | Host | Points to                | TTL    |
|-------|------|--------------------------|--------|
| CNAME | hps  | <github-username>.github.io | 1 hour |

Nothing else changes. This does not touch the Born Interactive site, its
records, or the root domain. It is the same pattern already in use for
`webinar.eastwood.global` and `gosu.eastwood.global`.

## Editing

Everything is in `index.html`. Copy sits in the markup. Design tokens sit in the
`:root` block at the top of the `<style>` tag: brand colour, type scale, section
rhythm, easing, and the two corner radii (`--r-box` for tiles, `--r-panel` for
the large inset panels). Replacing a photograph means dropping a file of the
same name into `assets/`.

Structure notes:

- Full-bleed colour and photography sections carry `class="panel"`. That is what
  makes them inset rounded blocks; remove the class and a section goes edge to
  edge again.
- The sticky header label reads the `data-where` attribute on each section.
- Photography parallax reads `data-par` (pixels of travel).
- Bento tiles take `navy`, `green`, `wide`, `photo` and `photo-band duo`
  classes. `duo` applies the Deep Blue duotone with the green halftone overlay.
- The timetable week toggle and its two copy blocks live in the `weeks` object
  at the bottom of the script.

## Motion

Motion is CSS-first and driven from one scroll frame in script: scroll progress,
lerped photographic parallax, and the tracking settle on the pinned statement.
Section reveals key off an `is-in` class added by a single IntersectionObserver,
with a four second failsafe, a `<noscript>` fallback, and a full
`prefers-reduced-motion` opt-out, so no element can end up stuck invisible.

CSS scroll timelines (`animation-timeline`) are deliberately not used: they do
not resolve in every browser this page ships to, and a dead timeline with
`fill: both` freezes elements on their first keyframe.

A script pass binds the last two words of every short measure with a
non-breaking space, so headings and labels do not end on a widow or a runt. It
runs before the line-mask wrap, so headings still reveal line by line.

## Accessibility

- Skip link, visible focus rings, 44px minimum touch targets on phones.
- Questions use native exclusive `<details name="faq">`, so the accordion works
  without script.
- Decorative graphics (pixel motif, lane markings, duotone band) are
  `aria-hidden`.

## External dependencies

One: Google Fonts, for Inter and Bodoni Moda. If it is ever blocked, the page
falls back to system sans and system serif and stays readable, but off-brand.
Ask Monica for the self-hosted font build if that becomes a concern.
