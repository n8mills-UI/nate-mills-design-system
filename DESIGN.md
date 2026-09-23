---
# The value blocks below (colors, typography, rounded, spacing) are GENERATED from
# tokens.json by tokens/designmd.mjs and drift-gated on deploy. Do not hand-edit between the
# `# DESIGN:*:start` / `# DESIGN:*:end` markers; edit tokens.json and regenerate. The prose, the
# component recipe map, and everything outside the markers is hand-authored.
version: 2.0.0
name: Nate Mills Portfolio
description: >
  Design, build, or substantially improve any page, prototype, or document that has to look like it
  came from natemills.me: portfolio sections, case-study pages, one-pagers, decks, and on-brand
  artifacts built with no access to the repo. Carries the resolved tokens, the published CSS class
  API to link against, and the rules that keep the result from looking generated.
about: >
  A design-systems consultant's portfolio where the system IS the pitch. The voltage is a single
  high-chroma lime held as a scarce accent against warm off-white and warm near-black, with honest
  hairline borders instead of decorative shadows or gradients. It counter-positions against the
  typical portfolio that scatters colour and leans on drop shadows: here depth is carried by a
  surface ladder and 1px hairlines, type hierarchy comes from weight not opacity, and every value
  traces to a token. Both a light theme (off-white canvas, ink accent) and a dark theme (near-black
  canvas, lime accent) are first-class, and the whole thing is authored to WCAG 2.2 AA in both.

colors:
  # DESIGN:colors:start
  # Brand identity (fixed, never theme-flips)
  brand-lime: "#d2ff37"                                                         # --brand-primary
  brand-lime-dim: "#b8e030"                                                     # --brand-primary-dim
  brand-lime-vivid: "#eeff00"                                                   # --brand-primary-vivid
  brand-ink: "#1c1c1f"                                                          # --brand-ink
  brand-gradient: "linear-gradient(135deg in oklab, #d2ff37 0%, #eeff00 100%)"  # --brand-gradient

  # Light theme semantics (the default page)
  bg: "#f5f5f5"                                                                 # --color-bg
  surface: "#ffffff"                                                            # --color-surface
  surface-sunken: "#ececec"                                                     # --color-surface-sunken
  surface-inverse: "#0a0a0b"                                                    # --color-surface-inverse (always-dark, both themes)
  text-primary: "#0a0a0b"                                                       # --color-text-primary
  text-secondary: "#3f3f46"                                                     # --color-text-secondary
  text-tertiary: "#67676f"                                                      # --color-text-tertiary
  border: "#e4e4e7"                                                             # --color-border
  border-strong: "#d4d4d8"                                                      # --color-border-strong
  border-brand: "#d2ff37"                                                       # --color-border-brand (lime, fixed both themes)
  accent: "#1c1c1f"                                                             # --color-accent (theme-aware: ink light, lime dark)
  accent-hover: "#0a0a0b"                                                       # --color-accent-hover
  on-accent: "#ffffff"                                                          # --color-on-accent
  focus-ring: "#1c1c1f"                                                         # --color-focus-ring (theme-aware)
  link: "#1c1c1f"                                                               # --color-link (theme-aware)
  link-hover: "#0a0a0b"                                                         # --color-link-hover

  # Text on always-dark slabs (theme-invariant)
  on-ink-primary: "rgba(255, 255, 255, 0.88)"                                   # --color-on-ink-primary
  on-ink-secondary: "rgba(255, 255, 255, 0.66)"                                 # --color-on-ink-secondary
  on-ink-muted: "rgba(255, 255, 255, 0.4)"                                      # --color-on-ink-muted
  on-ink-border: "rgba(255, 255, 255, 0.08)"                                    # --color-on-ink-border

  # Dark theme semantics (data-theme="dark" or OS dark)
  dark-bg: "#0a0a0b"                                                            # --darkTheme-color-bg
  dark-surface: "#1c1c1f"                                                       # --darkTheme-color-surface
  dark-surface-sunken: "#141416"                                                # --darkTheme-color-surface-sunken
  dark-text-primary: "#f4f4f5"                                                  # --darkTheme-color-text-primary
  dark-text-secondary: "#a1a1aa"                                                # --darkTheme-color-text-secondary
  dark-text-tertiary: "#909096"                                                 # --darkTheme-color-text-tertiary
  dark-border: "#27272a"                                                        # --darkTheme-color-border
  dark-accent: "#d2ff37"                                                        # --darkTheme-color-accent (brand lime, deliberate)
  dark-accent-hover: "#b8e030"                                                  # --darkTheme-color-accent-hover
  dark-focus-ring: "#d2ff37"                                                    # --darkTheme-color-focus-ring
  dark-link: "#d2ff37"                                                          # --darkTheme-color-link

  # Scrims
  overlay-soft: "rgba(0, 0, 0, 0.35)"                                           # --color-overlay-soft
  overlay-base: "rgba(0, 0, 0, 0.62)"                                           # --color-overlay-base
  overlay-strong: "rgba(0, 0, 0, 0.88)"                                         # --color-overlay-strong
  # DESIGN:colors:end

typography:
  families:
    # DESIGN:type-families:start
    display: '"Anton", Impact, "Haettenschweiler", sans-serif'  # --font-display
    body: '"Work Sans", -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif'  # --font-body
    mono: '"JetBrains Mono", ui-monospace, "SF Mono", Menlo, Consolas, monospace'  # --font-mono
    serif: '"PT Serif", Georgia, serif'  # --font-serif
    # DESIGN:type-families:end
  # DESIGN:type-styles:start
  hero:  # display specimen; a consuming site’s own hero may set bespoke clamps
    family: display
    size: "clamp(40px, 9vw, 118px)"  # --display-hero
    weight: 600                      # --display-weight
    lineHeight: 1.05                 # --line-display
    tracking: "-0.0176em"            # --display-tight
  h1:  # every section heading
    family: display
    size: "clamp(34px, 5.8vw, 72px)"  # --text-h1
    weight: 600                       # --display-weight
    lineHeight: 1.05                  # --line-display
    tracking: "-0.0176em"             # --display-tight
  h2:  # card titles, sub-heads
    family: display
    size: "clamp(22px, 4vw, 32px)"  # --text-h2
    weight: 600                     # --display-weight
    lineHeight: 1.15                # --line-heading
    tracking: "-0.02em"             # --tracking-tight
  card-title:  # large feature-card titles
    family: display
    size: "clamp(22px, 4vw, 44px)"  # --display-card-title
    weight: 600                     # --display-weight
    lineHeight: 1.15                # --line-heading
    tracking: "-0.0176em"           # --display-tight
  stat-num:  # stat callout numerals
    family: display
    size: "clamp(40px, 7vw, 88px)"  # --display-stat-num
    weight: 600                     # --display-weight
    lineHeight: 1.05                # --line-display
    tracking: "-0.0176em"           # --display-tight
  intro:  # section intro line
    family: body
    size: "clamp(20px, 5vw, 24px)"  # --display-intro
    weight: 400                     # --weight-regular
    lineHeight: 1.45                # --line-snug
    tracking: "-0.02em"             # --tracking-tight
  body:  # paragraphs
    family: body
    size: "16px"     # --text-body
    weight: 400      # --weight-regular
    lineHeight: 1.5  # --line-body
    tracking: 0      # --tracking-normal
  body-compact:  # footer, card bullets, dense UI
    family: body
    size: "14px"     # --size-sm
    weight: 400      # --weight-regular
    lineHeight: 1.5  # --line-body
  caption:  # captions, footnotes
    family: body
    size: "12px"     # --text-caption
    weight: 400      # --weight-regular
    lineHeight: 1.5  # --line-body
  label:  # uppercase eyebrows, chips, badges; line-height 1.4
    family: mono
    size: "11px"        # --text-label
    weight: 500         # --weight-medium
    tracking: "0.08em"  # --tracking-label
  # DESIGN:type-styles:end

rounded:
  # DESIGN:rounded:start
  none: 0        # --radius-none (square)
  sm: "8px"      # --radius-sm (inputs, small controls)
  md: "10px"     # --radius-md (mid-size controls, insets)
  lg: "14px"     # --radius-lg (social links and other mid-weight containers)
  xl: "20px"     # --radius-xl (DEFAULT for cards and modals, prominent panels)
  full: "999px"  # --radius-full (pills, chips, badges, buttons, icon buttons)
  # DESIGN:rounded:end

spacing:
  # DESIGN:spacing:start
  s1: "4px"                                                 # --space-1
  s2: "8px"                                                 # --space-2
  s3: "12px"                                                # --space-3
  s4: "16px"                                                # --space-4
  s5: "24px"                                                # --space-5
  s6: "32px"                                                # --space-6
  s7: "48px"                                                # --space-7
  s8: "64px"                                                # --space-8
  s9: "96px"                                                # --space-9 (section padding lower bound)
  s10: "128px"                                              # --space-10 (section padding upper bound)
  s11: "192px"                                              # --space-11
  s12: "256px"                                              # --space-12
  section-padding: "clamp(96px, min(14.2vh, 12vw), 256px)"  # --section-padding
  card-pad-compact: "16px"                                  # --card-pad-compact
  card-pad-standard: "24px"                                 # --card-pad-standard
  card-pad-spacious: "32px"                                 # --card-pad-spacious
  # DESIGN:spacing:end

# There is no elevation scale. Depth is the surface ladder plus hairline borders (see "Depth and
# elevation" below). The focus ring is the one ring-shaped value, and it is an outline, not a step.
focus:
  ring: "0 0 0 2px {colors.focus-ring}"   # 2px keyboard-focus outline, offset 2px

# Component recipes reference {token} names that resolve against the blocks above, so a value change
# propagates automatically and no raw value can drift here. Each variant is its own entry.
components:
  nav:
    background: "transparent (frosted glass pill once scrolled)"
    textColor: "{colors.text-tertiary}"
    typography: "{typography.label}"
    activeTextColor: "{colors.text-primary}"
    activeUnderline: "1px, {colors.accent} (ink on light, lime on dark)"
    note: "State reads from underline shape PLUS colour, never colour alone."
  hero-headline:
    typography: "{typography.hero}"
    textColor: "{colors.text-primary}"
    emphasisWord: "one word may be italic and a muted colour; never the whole heading"
  button-primary:
    backgroundColor: "{colors.brand-lime}"
    textColor: "{colors.brand-ink}"
    border: "1px solid {colors.border-brand}"
    typography: "{typography.label} at 14px, weight 600"
    rounded: "{rounded.full}"
    padding: "10px 18px"
    height: "44px (md); 32px (sm); 52px (lg)"
  button-primary-hover:
    backgroundColor: "{colors.brand-ink}"
    textColor: "{colors.brand-lime}"
  button-secondary:
    backgroundColor: "transparent"
    textColor: "{colors.text-primary}"
    border: "1px solid {colors.text-tertiary}"
    rounded: "{rounded.full}"
    padding: "10px 18px"
  button-secondary-hover:
    backgroundColor: "{colors.surface-sunken}"
    border: "1px solid {colors.text-primary}"
  button-icon:
    shape: "circle, {rounded.full}"
    border: "1px solid {colors.text-tertiary}"
    iconColor: "{colors.text-secondary}"
    size: "44px, glyph 16px"
    note: "The one canonical icon button. An icon-only button is never a pill with a label."
  card:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.text-primary}"
    border: "1px solid {colors.border}"
    rounded: "{rounded.xl}"
    padding: "{spacing.card-pad-standard}"
    hover: "outline and slight lift, NOT a fill"
  card-dark:
    backgroundColor: "{colors.brand-ink}"
    textColor: "{colors.on-ink-primary}"
    border: "1px solid {colors.on-ink-border}"
  carousel-nav:
    layout: "bare chevron buttons and a counter on a rail below the cards"
    dotActive: "{colors.accent}"
    dotInactive: "{colors.text-tertiary} (tuned to clear 3:1)"
    dotInactiveOnInverse: "{colors.on-ink-muted}"
    counter: "{typography.label} mono"
  badge:
    backgroundColor: "transparent"
    textColor: "{colors.text-secondary}"
    border: "1px solid {colors.border}"
    typography: "{typography.label} mono, weight 500"
    rounded: "{rounded.full}"
    padding: "4px 12px"
    dot: "{colors.brand-lime} (6px, stays lime in both themes; the word carries meaning)"
  chip:
    backgroundColor: "{colors.surface-sunken}"
    textColor: "{colors.text-primary}"
    border: "1px solid {colors.border}"
    typography: "{typography.label} mono, weight 500"
    rounded: "{rounded.full}"
    padding: "4px 10px"
  footer:
    backgroundColor: "{colors.brand-lime}"
    textColor: "{colors.brand-ink}"
    note: "A fixed lime slab, lime in BOTH themes; one of the few large lime fills allowed."
  link:
    textColor: "{colors.link}"
    decoration: "underline"
    hover: "{colors.link-hover}"
    external: "opens a new tab, rel set, trailing up-right arrow glyph plus a screen-reader cue"
---

# Nate Mills Portfolio: Brand Contract

This is a portable brand contract. Hand it to any AI coding agent, or a contractor, and it has
everything needed to build a page that feels like natemills.me: no repo, no build tools, just this
file. Every colour, size, radius, and spacing value in the frontmatter above is resolved to a literal
and generated straight from the design token source, so it cannot drift from the real system.

## Use the published CSS

Link the foundation. Do not rebuild it from the values above.

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Anton&family=PT+Serif:ital,wght@0,400;0,700;1,400;1,700&family=Work+Sans:ital,wght@0,400..800;1,400..800&display=swap" rel="stylesheet">
<link href="https://natemills.me/assets/fonts.css" rel="stylesheet">
<link href="https://natemills.me/assets/tokens.css" rel="stylesheet">
<link href="https://natemills.me/assets/components.css" rel="stylesheet">
```

`tokens.css` carries every custom property in all three themes (light, dark, high-contrast) and
`components.css` reads them, so tokens must load first. `fonts.css` is separate and required: it
declares the self-hosted JetBrains Mono and turns on the slashed zero. Anton, Work Sans and PT Serif
come from Google Fonts, which is why that request is in the list too. Drop any one of the six and the
type silently falls back.

Rules for using it:

- **Use the exact class names below.** Do not invent synonyms. There is no `.button`, no `.btn-primary`
  with one dash, and no `.card-dark`.
- **Do not read the stylesheet into context.** It is 75KB of implementation you do not need. The table
  below is the whole public API.
- **Never `@import`, never `file://`, never a placeholder URL.** Link the absolute URLs above, or copy
  the files into the project and link them relatively.
- **Reach for a class before a value.** The resolved colours, type, radii and spacing in the frontmatter
  are for things the class layer does not cover, and for the offline case where you cannot link at all.
  If a class exists, use it.
- **Do not restyle a published class.** Compose around it. If you need a page-specific variation, write
  your own class next to it; never redefine `.btn` or `.card`.

<!-- DESIGN:classes:start -->
**Buttons:** Base .btn is the 44px default. Size modifiers wire the --btn-* tokens.

| Class | Use |
| --- | --- |
| `.btn` | base; always pair with a variant |
| `.btn--primary` | lime fill, ink label; inverts on hover |
| `.btn--secondary` | transparent, tertiary-grey outline |
| `.btn--icon` | the one canonical icon button: 44px circle, never a labelled pill |
| `.btn--sm` | 32px |
| `.btn--md` | 44px, same as base |
| `.btn--lg` | 52px |

**Cards:** Surface step plus a hairline border. Never a drop shadow.

| Class | Use |
| --- | --- |
| `.card` | base |
| `.card--dark` | on an always-dark slab; switches to the on-ink-* text family |
| `.card--interactive` | THE clickable-card hover: border strengthens and lifts, no fill |
| `.card--compact` | 16px padding |
| `.card--spacious` | 32px padding |
| `.card--empty` | centred empty state |
| `.card--error` | centred error state, carries the feedback colour |
| `.card--loading` | skeleton state |

**Chips and badges:** Resolve by job: a label is a chip, a status is a badge. A badge is read-only, never interactive.

| Class | Use |
| --- | --- |
| `.chip` | sunken fill, mono label |
| `.chip--outline` | fill drops out for quieter contexts |
| `.badge` | transparent, hairline border |
| `.badge__dot` | lime status dot; always pair it with a word, never colour alone |

**Section heading:** The section-head block owns the gap from heading to body. Do not add your own margin.

| Class | Use |
| --- | --- |
| `.section-head` | wrapper |
| `.section-label` | uppercase mono eyebrow |
| `.section-label--accent` | accent-emphasis colour, for eyebrows on marquee cards |
| `.section-label--center` | centred |
| `.section-label--icon` | icon-led; the glyph is decorative |
| `.section-label--row` | heading ROW rather than an inline tag |
| `.section-title` | h1/h2, carries the drawn brand period |
| `.section-subtitle` | intro line under the title |

**Links:** A border-bottom underline, so the rule colours and animates independently of the text.

| Class | Use |
| --- | --- |
| `.link-underline` | base |
| `.link-underline--prose` | inside body copy |
| `.link-underline--icon` | carries a trailing glyph |

**Carousel navigation:** Bare chevrons plus a mono counter on a rail BELOW the cards. One nav, site-wide.

| Class | Use |
| --- | --- |
| `.ds-carousel-nav` | wrapper |
| `.ds-carousel-nav--full` | full-width rail |
| `.ds-carousel-nav__rail` | the track |
| `.ds-carousel-nav__arrow` | prev / next |
| `.ds-carousel-nav__pager` | dots |
| `.ds-carousel-nav__fill` | progress fill |
| `.ds-carousel-nav__count` | mono counter |

**Other**

| Class | Use |
| --- | --- |
| `.avatar` | round portrait |
| `.sr-only` | visually hidden, still announced |
<!-- DESIGN:classes:end -->

Anything not in that table is a portfolio internal, not public API. Build it yourself from the tokens.

## Overview

This is the portfolio of a Senior Product Designer (Design Systems). The site is the argument: a
calm, Swiss-minimal editorial surface where a single high-chroma lime does all the talking and
everything else stays quiet. The atmosphere is warm off-white paper in light mode and warm near-black
in dark mode, never pure white and never pure black. Depth is built from a surface ladder and honest
1px hairlines, not from drop shadows or decorative gradients. Display type is Anton, set large and
tight; body copy and controls are Work Sans; JetBrains Mono carries eyebrows and labels; PT Serif is
reserved for editorial quotes only.

The counter-position is deliberate: most portfolios scatter accent colour across whole sections and
lean on soft shadows to fake hierarchy. This one refuses both. Colour is scarce, borders are honest,
and hierarchy comes from weight and scale. If you are building a new page, the system is the pitch:
make it look composed, restrained, and inevitable.

It is not a component library, not Tailwind-driven, and not CSS-in-JS. There is no DaisyUI, Material
or utility framework underneath: just CSS custom properties and one hand-built class layer, shipped
as static stylesheets. The custom build is the point, so do not reach for a framework to fill a gap.

### Key characteristics

- Warm off-white canvas (`{colors.bg}`), not white. Ink is warm near-black, not pure black.
- One accent, one lime (`{colors.brand-lime}`), used scarcely. Never a section fill or body text.
- Borders over shadows. Shadows are rare and reserved for overlays.
- Display type is Anton, tight tracking. Anton draws one weight (400) and no italic, and font
  synthesis is off, so a rule asking for 600 or 800 renders the real 400. Never ask this face for a
  bold or an italic it does not have, and never italicise a whole heading.
- Mono (JetBrains Mono) is for uppercase eyebrows, chips, and badges only.
- Both themes are first-class. In dark mode the accent IS the lime, by design.
- WCAG 2.2 AA in both themes is a floor, not a feature.
- Token names match the scale: words for small fixed sets (`--radius-sm`), numbers for open ramps
  (`--space-4`, `--neutral-850`), intent for roles (`--color-text-primary`). Name a new token the
  same way.

## Color roles

The palette is exactly two families: a warm neutral ramp and one lime. There is no red, amber, or
blue in the system (external brand colours like a client blue are locked constants used only inside
their own case-study or logo context, never as system colour).

**Brand voltage rule: use the lime (`{colors.brand-lime}`) ONLY for** the primary button fill, brand
outlines (`{colors.border-brand}`), focus rings on dark surfaces, the lime period after a section
title, the active carousel dot on dark, status dots, and the footer slab. **Never** use lime as body
text, as a link on a light background, as a section background, or as a large fill on the light page.
On the off-white canvas raw lime composites to roughly 1.06:1 and fails WCAG outright.

**The theme-aware accent.** `{colors.accent}` is the one interactive role that follows the theme: it
resolves to ink on light and to lime on dark. Anything that signals an active or selected state
(current nav item, pressed toggle, active dot) uses `accent`, never raw lime, so it stays legible on
the light page. `{colors.border-brand}` is the deliberate exception: it stays fixed lime in both
themes because it is a brand-identity outline, not a state signal.

**Dark-mode accent is the lime, deliberately.** On the dark theme, `accent`, `link`, and `focus-ring`
all resolve to brand lime. This is a locked brand ruling, not a contrast bug: lime on near-black reads
at roughly 10:1 (AAA). Do not "fix" it to a near-white. What is forbidden in dark mode is a solid lime
panel; the calm dark treatment is charcoal with lime text, not lime wallpaper.

**Text on dark slabs.** Some surfaces (testimonials, contact) stay near-black in both themes. Text on
them uses the `on-ink-*` family (88% / 66% / 40% white), never the theme-aware text tokens. Do not use
an `on-ink` colour on a light surface; it is white-on-dark only and will vanish on a white card.

## Typography rules

- Weight and scale carry hierarchy, never opacity. Do not dim body text with alpha to make it read
  secondary; step down a text style instead.
- Display is always roman. A full italic heading is banned. Italic is allowed on a single word or short
  phrase inside a heading, and only when paired with a muted colour to mark it as secondary emphasis.
- Eyebrows and labels are uppercase JetBrains Mono with positive tracking (0.08em labels, 0.18em
  eyebrows) to mark them as taxonomy.
- Body copy is `text-align: start`, ragged right. Never justify.
- Line length caps at 52ch. The 11px mono label is the floor; never go smaller.

## Component stylings

- **Buttons** are full pills, Work Sans semibold at 14px, padding 10px/18px, default height 44px. The
  primary button is a lime fill with ink label; on hover it inverts to an ink fill with a lime label.
  The secondary button is transparent with a `{colors.text-tertiary}` outline (that outline colour is
  chosen to clear the 3:1 non-text contrast floor).
- **Icon button** is the one canonical circle: a `{colors.text-tertiary}` hairline ring,
  `{colors.text-secondary}` glyph, 44px, `{rounded.full}`. Never a pill with a label.
- **Cards** sit on `{colors.surface}` with a 1px `{colors.border}` hairline and `{rounded.xl}`, padded
  24px (compact 16, spacious 32). Interaction is outline-plus-lift, not a background fill. Cards on a
  dark slab use the `card-dark` recipe, whose fixed ink and `on-ink-*` tokens keep it dark in both
  themes. Never pin `data-theme` on an element to force a look: the pin survives when the element is
  cloned and silently breaks dark mode.
- **Chips vs badges vs counters** resolve by job: a label is a chip, a status is a badge, a count is
  the carousel counter. A badge is read-only and never interactive; its dot stays lime in both themes
  but colour is never the only signal, every status also carries a word.
- **Carousel nav** is bare chevrons plus a mono counter on a rail below the cards. The active dot
  follows `{colors.accent}`; the inactive dot is a solid tuned grey (not a translucent one, which
  would fail 3:1).
- **Footer** is a fixed lime slab with ink text, lime in both themes.
- **Links** are underlined, `{colors.link}` (ink on light, lime on dark). External links open a new
  tab, set `rel`, and carry a trailing up-right arrow glyph plus a screen-reader cue.
- **Action icons** name what the link does: `mail` for a `mailto:` link, `download` for a file
  download, `arrow-up-right` for an external link. Never the `external-link` box glyph, and no icon
  on a same-page anchor, because it never leaves the page.
- **Standing call-to-action links** use a real 1.5px `border-bottom` in `{colors.border-brand}` rather
  than `text-decoration`, so the rule can be coloured and animated independently of the text. Exactly
  ONE of the two underline mechanisms is ever active on a given link: a border and a text-decoration
  underline together render as a visible double line. A component that draws its own border must also
  cancel `text-decoration` in its `:hover` and `:focus-visible`, not only at rest, or the global link
  hover puts the second line back.

## Layout principles

- Content sits in a wide band that stays proportional on normal screens and caps at 1680px so
  ultrawide layouts do not stretch without earning it.
- One container width per section: the 960px prose column (`--container-base`) or that wide band
  (`--container-wide`, for grids). No middle ground, so every section's gutter lines up.
- Vertical rhythm is `{spacing.section-padding}` between sections.
- Spacing is a strict 4px scale. Never use raw px for spacing; reach for a scale step.
- Full-bleed inverse bands (testimonials, contact) break out to the screen edge and stay near-black in
  both themes.
- Stacking uses a named z-index scale with 100-unit gaps. Never hand-write a raw page-level z-index.

## Depth and elevation

Depth is carried by the surface ladder plus hairline borders, not by shadows. The ladder, light to
recessed: `{colors.bg}` (page) to `{colors.surface}` (card, a genuine lift) to
`{colors.surface-sunken}` (wells and insets). Dark mode runs the same three steps in near-blacks.

There is no shadow scale, and no drop shadow on any card, panel, modal or floating control. A card
is a surface step plus a hairline; a selected or open card moves its border, never its elevation; a
lightbox is separated by its scrim, not by a shadow cast onto that scrim. This was always the written
rule, and until 2026-08-29 the code did not match it: a four-step ramp had accumulated on seven
resting surfaces, entering as a token-leak fix that replaced a stray hardcoded shadow with a
sanctioned-looking one instead of deleting it. The ramp is gone and a lint gate now holds the line.

Two scoped effects survive and are deliberately not tokens: the bottom edge of `main` during the
footer parallax reveal, where a shadow is the only way to say one layer is passing over another, and
the floating theme-lab panel, which is instrument chrome rather than a page surface.

Radii: cards and modals use `{rounded.xl}`; small controls use `{rounded.sm}`; pills, chips, badges,
and buttons use `{rounded.full}`.

## Do's and Don'ts

Do:
- Do keep the lime scarce. If two primary buttons would appear in one viewport, make one secondary.
- Do build hierarchy from weight and scale.
- Do use `{colors.accent}` for any active or selected state so it stays legible on light.
- Do give every status a word, not just a coloured dot.
- Do design the static, reduced-motion frame first; motion is garnish that never carries meaning.

Don't:
- Don't use pure white as the page canvas or pure black as ink. The canvas is `{colors.bg}`.
- Don't put lime on a light background as text, a link, or a large fill (it fails WCAG at ~1.06:1).
- Don't paint a solid lime panel in dark mode; use charcoal with lime text.
- Don't dim text with opacity to fake a secondary tone; step down a text style.
- Don't italicise a whole heading, and don't use an alpha colour for heading emphasis.
- Don't reach for a drop shadow to separate a card; use a hairline border.
- Don't justify body text, and don't drop below the 11px mono label floor.
- Don't leak an external client brand colour into general UI; those are locked constants for their
  own case-study context only.

## Voice and tone

The words follow one rule, the same way the colours do. A page that governs its pixels but lets its
copy wander still feels inconsistent.

- Write in the first person, in plain words, the way one designer talks to another over coffee.
- Let proof carry the brag. Numbers, not superlatives: "18 hours back to the team", never "huge
  productivity gains".
- No hedges. Say it or don't.
- Body sentences run 6 to 14 words, one idea each.
- Headings are sentence case, everywhere.

The voice never changes; only the length does. Short copy compresses it:

- **Buttons:** verb plus outcome. "Read the case study", "Get in touch".
- **Errors:** name the problem and the workaround. No apology.
- **Status pills:** declarative present tense, "Available for work". Never aspirational.
- **Section subtitle:** one sentence that sets the stake, 18 words or fewer.
- **Empty state:** what is missing, then what to do.
- **Loading state:** copy only if the wait runs over a second, and then it sets the expectation.

| Use | Avoid |
|---|---|
| system, token, governance, pipeline, foundation | passionate, world-class |
| ship, scale, adoption, contribution | amazing, incredible, excited |
| multi-brand, cross-platform, token-driven | we believe, we think, arguably |
| let's talk, get in touch | click here, learn more, submit |

The AI copy tells under **Copy** below are on the avoid list too.

## Reject generated-design reflexes

These are the defaults an agent reaches for when it is not thinking. None of them belong to this
system. The Don'ts above are brand rules; these are the house rules that keep the work from looking
generated.

**Copy**

- No em dashes and no en dashes, anywhere. Use a comma, a colon, a semicolon, or two sentences. This
  one has no exceptions.
- No AI copy tells: "elevate", "seamless", "unleash", "next-gen", "game-changing", "delve",
  "cutting-edge", "supercharge", "harness the power", "it's not just".
- Never ship placeholder content as if it were real: no lorem ipsum, no Jane Doe, no Acme Corp.

**Colour and surface**

- No AI-default gradient palette. The indigo, violet, fuchsia and cyan family (`#4f46e5`, `#6366f1`,
  `#7c3aed`, `#8b5cf6`, `#a855f7`, `#06b6d4`, `#d946ef` and relatives) is the single loudest tell.
  This system has two colour families: a warm neutral ramp and one lime.
- No gradient text, glows, blobs, mesh backgrounds, glass, noise overlays, or fake depth. The one
  gradient in the system is `{colors.brand-gradient}`, and it is brand identity, not decoration.
- No decorative surface to fill space. A border is earned by grouping or interaction.

**Layout**

- No hero followed by three equal cards. Do not force unequal content into equal cells; rank it,
  group it, or rebalance it.
- No metric boxes as ornament, no icon tiles, no card nested inside a card to fix spacing.
- No badge on everything. A badge is a status, not a garnish.
- Do not give every section the same silhouette.

**Type and icons**

- No emoji as icons. Icons are Lucide: `<i data-lucide="name" aria-hidden="true">`.
- Anton is the display face. Never set a heading in Inter, Roboto, Arial, Helvetica or system-ui: a
  default UI face used as a display face reads as a demo, not a design.

**Motion**

- No `transition: all`. Name the properties you are animating.
- No `ease-in` on UI motion. Use ease-out or a named curve, and make exits faster than entrances.
- Gate every hover effect behind `@media (hover: hover)`. On a touch screen a tap latches hover and
  the effect sticks with no way to dismiss it.
- Every animation answers `prefers-reduced-motion`. Design the still frame first.
- No scroll-jacking, no parallax, no revealing every section on scroll.

**Mechanics**

- `100dvh`, never `100vh`. The mobile viewport unit is wrong under a browser chrome bar.
- No `href="#"` placeholder links. Every `<img>` carries an `alt` plus a `width` and `height` that
  match the file's own shape, so the browser reserves the right box and the page does not jump.
- Semantic HTML first (`<header>`, `<nav>`, `<main>`, `<section>`, `<button>`). ARIA only where
  HTML cannot carry the meaning.

## Responsive behavior

Reference breakpoints: mobile 375px, tablet 768px, desktop 1024px, wide 1440px, ultrawide 1600px.

- Type is fluid via `clamp()` and capped, so headings grow on wider screens and stop; they never balloon.
- At and below 768px, section-level primary CTAs go full-width and centre for a thumb-friendly tap
  target; inline buttons inside paragraphs stay auto-width.
- Dense value tables tighten below ~640px but never drop a column and never shrink labels below 11px.
- Touch targets meet 44px; small dots keep a 24px hit area.
- Verify layout at ~375px alongside both light and dark themes whenever you touch a layout.

## Agent prompt guide

When building a new page or prototype with this system:

1. Work one component at a time and reference tokens by name (`{colors.accent}`, `{typography.h1}`,
   `{rounded.lg}`), never by inventing a hex or px value.
2. Decide first which surface a section sits on (`bg`, `surface`, `surface-sunken`, or an always-dark
   `surface-inverse`), then pick text colours to match: `text-*` on light, `on-ink-*` on dark slabs.
3. Keep the lime scarce. It appears on the primary button, brand outlines, focus rings on dark, status
   dots, and the footer. Nowhere else.
4. For any active or selected state use `{colors.accent}` (theme-aware), not raw lime, so it survives
   the light theme.
5. Build hierarchy from weight (600 display, 400 body) and scale, not opacity.
6. Use hairline borders for separation; reach for a shadow only on an overlay or lightbox.
7. Support both themes: the dark accent is intentionally the lime, and the dark treatment for a dark
   surface is charcoal with lime text, never lime wallpaper.
8. Hold WCAG 2.2 AA in both themes: 4.5:1 for body text, 3:1 for non-text and large text, visible
   focus, 44px targets.

## Known gaps

- This contract carries resolved values for portability; the source of truth authors every colour in
  OKLCH as well, and the values here are exact round-trips of those OKLCH colours. The shipped CSS
  emits the sRGB hex only, deliberately: the round-trip is exact, so emitting OKLCH changed no pixel,
  and it made computed colours unreadable to sRGB-only accessibility scanners.
- The system has no semantic status colours (success/warning/danger); a portfolio has no such UI. If a
  consumer needs them, add at the token layer first, then route a semantic.
- Fonts are Anton (display), Work Sans (body and controls), JetBrains Mono (labels and numbers) and
  PT Serif (quotes). All four are open source. If one is unavailable, fall back to a condensed
  grotesque for display, a neutral grotesque for body, any monospace with a slashed zero for labels,
  and a transitional serif (Georgia) for quotes.
- The mono zero is SLASHED, and it does not come for free. JetBrains Mono's default zero has a dot
  in it; the slash is the OpenType `zero` feature, applied once at `:root` via
  `font-feature-settings: var(--font-feature-mono)` rather than per rule. The build served by
  Google Fonts has that feature subsetted out, so consuming the font from a CDN gives dotted zeros
  no matter what the token says. Self-host the full release, and if you subset it, retain the
  feature explicitly (`pyftsubset --layout-features+=zero`) because it is not in the default
  retained set. Never let a component set its own `font-feature-settings`: the property replaces
  rather than merges, so one component-level declaration silently restores the dot.
- Exact computed contrast ratios are verified in a live specimen; the floors above (4.5:1 text, 3:1
  non-text) are the targets to design to.
- The accessibility claim is WCAG 2.2 AA, and it is a self-assessment backed by automated gates, not
  a certification. APCA was explored as a sharper readability ceiling above that floor, never as a
  compliance claim: it is not a conformance standard. Do not cite an APCA score as proof.
- The token source is DTCG-format. DTCG is a W3C Community Group format, not a W3C Recommendation,
  so "DTCG-format" is the accurate claim and "fully spec-compliant" would not be.
