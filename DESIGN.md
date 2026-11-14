---
# The value blocks below (colors, typography, rounded, spacing, structure, motion) and the version are GENERATED from
# tokens.json by tokens/designmd.mjs and drift-gated on deploy. Do not hand-edit between the
# `# DESIGN:*:start` / `# DESIGN:*:end` markers; edit tokens.json and regenerate. The prose, the
# component recipe map, and everything outside the markers is hand-authored.
version: 4.0.1
name: Nate Mills Portfolio
description: >
  Design, build, or substantially improve any page, prototype, or document that has to look like it
  came from natemills.me: portfolio sections, case-study pages, one-pagers, decks, and on-brand
  artifacts built with no access to the repo. Carries the resolved tokens, the published CSS class
  API to link against, and the rules that keep the result from looking generated.
about: >
  A design-systems consultant's portfolio where the system IS the pitch. The voltage is a single
  high-chroma lime held as a scarce accent against a neutral off-white and a cool near-black, with honest
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
  brand-secondary: "#eeff00"                                                    # --brand-secondary (the yellow beside lime)
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
  border-strong: "#d4d4d8"                                                      # --color-border-strong (a colour; var(--border-strong) is the whole 1px border)
  border-brand: "#d2ff37"                                                       # --color-border-brand (lime, fixed both themes)
  accent: "#1c1c1f"                                                             # --color-accent (theme-aware: ink light, lime dark)
  accent-hover: "#0a0a0b"                                                       # --color-accent-hover
  on-accent: "#ffffff"                                                          # --color-on-accent (theme-aware)
  focus-ring: "#1c1c1f"                                                         # --color-focus-ring (theme-aware)
  link: "#1c1c1f"                                                               # --color-link (theme-aware)
  link-hover: "#0a0a0b"                                                         # --color-link-hover

  # Text on always-dark slabs (theme-invariant)
  on-ink-primary: "#e4e4e7"                                                     # --color-on-ink-primary
  on-ink-secondary: "#b2b2b3"                                                   # --color-on-ink-secondary
  on-ink-muted: "rgb(255 255 255 / 0.4)"                                        # --color-on-ink-muted
  on-ink-border: "rgb(255 255 255 / 0.08)"                                      # --color-on-ink-border

  # Dark theme semantics (the same properties as above, re-pointed under data-theme="dark" or OS dark; no --dark-* property exists)
  dark-bg: "#0a0a0b"                                                            # --color-bg (dark theme)
  dark-surface: "#1c1c1f"                                                       # --color-surface (dark theme)
  dark-surface-sunken: "#141416"                                                # --color-surface-sunken (dark theme)
  dark-text-primary: "#f4f4f5"                                                  # --color-text-primary (dark theme)
  dark-text-secondary: "#a1a1aa"                                                # --color-text-secondary (dark theme)
  dark-text-tertiary: "#909096"                                                 # --color-text-tertiary (dark theme)
  dark-border: "#27272a"                                                        # --color-border (dark theme)
  dark-border-strong: "#3f3f46"                                                 # --color-border-strong (dark theme)
  dark-accent: "#d2ff37"                                                        # --color-accent (dark theme; brand lime, deliberate)
  dark-accent-hover: "#b8e030"                                                  # --color-accent-hover (dark theme)
  dark-on-accent: "#0a0a0b"                                                     # --color-on-accent (dark theme)
  dark-focus-ring: "#d2ff37"                                                    # --color-focus-ring (dark theme)
  dark-link: "#d2ff37"                                                          # --color-link (dark theme)
  dark-link-hover: "#ffffff"                                                    # --color-link-hover (dark theme)

  # Scrims
  overlay-soft: "rgb(10 10 11 / 0.35)"                                          # --color-overlay-soft
  overlay-base: "rgb(10 10 11 / 0.62)"                                          # --color-overlay-base
  overlay-strong: "rgb(10 10 11 / 0.88)"                                        # --color-overlay-strong
  # DESIGN:colors:end

typography:
  families:
    # DESIGN:type-families:start
    display: '"Anton", Impact, "Haettenschweiler", sans-serif'  # --font-display
    body: '"Work Sans", "Work Sans Fallback", -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif'  # --font-body (the family; --text-body is the body size)
    mono: '"JetBrains Mono", ui-monospace, "SF Mono", Menlo, Consolas, monospace'  # --font-mono
    # DESIGN:type-families:end
  # DESIGN:type-styles:start
  hero:  # display specimen; a consuming site’s own hero may set bespoke clamps
    family: display
    size: "clamp(2.5rem, 9vw, 7.375rem)"  # --display-hero
    weight: 400                           # --display-weight
    lineHeight: 1.05                      # --line-display
    tracking: "-0.0176em"                 # --display-tight
  section-title:  # every section heading (.section-title); Anton has one weight and draws 400 whatever is asked, so 800 shows only in a display font that has it
    family: display
    size: "clamp(min(4.25rem, 19vw), 8.7vw, 7.5rem)"  # --display-section
    weight: 800                                       # --weight-extrabold
    lineHeight: 1.05                                  # --line-display
    tracking: "-0.0176em"                             # --display-tight
  h1:  # document headings outside .section-title
    family: display
    size: "clamp(2.125rem, 5.8vw, 4.5rem)"  # --text-h1
    weight: 400                             # --display-weight
    lineHeight: 1.05                        # --line-display
    tracking: "-0.0176em"                   # --display-tight
  h2:  # card titles, sub-heads
    family: display
    size: "clamp(1.375rem, 4vw, 2rem)"  # --text-h2
    weight: 400                         # --display-weight
    lineHeight: 1.15                    # --line-heading
    tracking: "-0.02em"                 # --tracking-tight
  card-title:  # large feature-card titles
    family: display
    size: "clamp(1.375rem, 4vw, 2.75rem)"  # --display-card-title
    weight: 400                            # --display-weight
    lineHeight: 1.15                       # --line-heading
    tracking: "-0.0176em"                  # --display-tight
  stat-num:  # stat callout numerals
    family: display
    size: "clamp(2.5rem, 7vw, 5.5rem)"  # --display-stat-num
    weight: 400                         # --display-weight
    lineHeight: 1.05                    # --line-display
    tracking: "-0.0176em"               # --display-tight
  intro:  # section intro line
    family: body
    size: "clamp(1.25rem, 5vw, 1.5rem)"  # --display-intro
    weight: 400                          # --weight-regular
    lineHeight: 1.45                     # --line-snug
    tracking: "-0.02em"                  # --tracking-tight
  body:  # paragraphs
    family: body
    size: "1rem"     # --text-body
    weight: 400      # --weight-regular
    lineHeight: 1.5  # --line-body
    tracking: 0      # --tracking-normal
  body-compact:  # footer, card bullets, dense UI
    family: body
    size: "0.875rem"  # --size-sm
    weight: 400       # --weight-regular
    lineHeight: 1.5   # --line-body
  caption:  # captions, footnotes
    family: body
    size: "0.75rem"  # --text-caption
    weight: 400      # --weight-regular
    lineHeight: 1.5  # --line-body
  label:  # uppercase eyebrows, chips, badges; line-height 1.4
    family: mono
    size: "0.6875rem"   # --text-label
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
  s50: "2px"                                                # --space-50
  s100: "4px"                                               # --space-100
  s200: "8px"                                               # --space-200
  s250: "10px"                                              # --space-250
  s300: "12px"                                              # --space-300
  s400: "16px"                                              # --space-400
  s500: "24px"                                              # --space-500
  s600: "32px"                                              # --space-600
  s700: "48px"                                              # --space-700
  s800: "64px"                                              # --space-800
  s900: "96px"                                              # --space-900 (section padding lower bound)
  s1000: "128px"                                            # --space-1000 (section padding upper bound)
  s1100: "192px"                                            # --space-1100
  s1200: "256px"                                            # --space-1200
  section-padding: "clamp(96px, min(14.2vh, 12vw), 256px)"  # --section-padding
  card-pad-compact: "16px"                                  # --card-pad-compact
  card-pad-standard: "24px"                                 # --card-pad-standard
  card-pad-spacious: "32px"                                 # --card-pad-spacious
  # DESIGN:spacing:end

# Borders, focus and targets: whole shorthand values, so a recipe names one instead of spelling
# 1px solid or 44px.
structure:
  # DESIGN:structure:start
  border-hairline: "1px solid #e4e4e7"  # --border-hairline (the default 1px border)
  border-strong: "1px solid #d4d4d8"    # --border-strong
  border-focus: "2px solid #1c1c1f"     # --border-focus (the keyboard-focus outline)
  focus-ring-offset: "2px"              # --focus-ring-offset
  touch-target-min: "44px"              # --touch-target-min (the smallest tap target)
  # DESIGN:structure:end

motion:
  # DESIGN:motion:start
  duration-fast: "150ms"                        # --duration-fast (hover, focus, small state changes)
  duration-base: "220ms"                        # --duration-base (reveals, modals, swaps)
  duration-slow: "400ms"                        # --duration-slow (context shifts and slides)
  ease-default: "cubic-bezier(0.4, 0, 0.2, 1)"  # --ease-default
  ease-entrance: "cubic-bezier(0, 0, 0.2, 1)"   # --ease-entrance (arriving on screen)
  ease-exit: "cubic-bezier(0.4, 0, 1, 1)"       # --ease-exit (leaving the screen)
  # DESIGN:motion:end

# There is no elevation scale. Depth is the surface ladder plus hairline borders (see "Depth and
# elevation" below). The focus ring is the one ring-shaped value, and it is an outline, not a step.
focus:
  outline: "{structure.border-focus}"        # outline: var(--border-focus); never a box-shadow
  offset: "{structure.focus-ring-offset}"    # outline-offset: var(--focus-ring-offset)

# Component recipes reference {token} names that resolve against the blocks above, so a value change
# propagates automatically. A border with no shorthand of its own is the hairline width, 1px, plus a
# colour token. Each variant is its own entry.
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
    typography: "{typography.families.body} at 14px, weight 600, normal tracking, sentence case (not the mono label)"
    rounded: "{rounded.full}"
    padding: "10px 18px"
    height: "{structure.touch-target-min} (md); 32px (sm); 52px (lg)"
  button-primary-hover:
    backgroundColor: "{colors.brand-ink}"
    textColor: "{colors.brand-lime}"
  button-secondary:
    backgroundColor: "transparent"
    textColor: "{colors.text-primary}"
    border: "{structure.border-hairline} (a stronger grey in dark)"
    rounded: "{rounded.full}"
    padding: "10px 18px"
  button-secondary-hover:
    backgroundColor: "{colors.brand-lime}"
    textColor: "{colors.brand-ink}"
    border: "1px solid {colors.border-brand}"
  button-icon:
    shape: "circle, {rounded.full}"
    border: "{structure.border-hairline} (a stronger grey in dark)"
    iconColor: "{colors.text-primary}"
    size: "{structure.touch-target-min}, glyph 16px"
    note: "The one canonical icon button. An icon-only button is never a pill with a label."
  card:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.text-primary}"
    border: "{structure.border-hairline}"
    rounded: "{rounded.xl}"
    padding: "{spacing.card-pad-standard}"
    hover: "outline and slight lift, NOT a fill"
  card-dark:
    backgroundColor: "{colors.brand-ink}"
    textColor: "{colors.on-ink-primary}"
    border: "1px solid {colors.on-ink-border}"
  carousel-nav:
    layout: "dots bottom left, two round arrows bottom right, below the cards; no progress bar and no count"
    dots: "8px {colors.text-primary} dots at 30% alpha; the current one fills and stretches to 24px over {motion.duration-slow}"
    arrows: "{structure.touch-target-min} circles, {colors.text-primary} at 12% alpha (18% on hover), a 24px chevron"
    strip: "from 768px .ds-carousel--strip bleeds the track to the page edge; put .ds-carousel and data-ds-carousel on the same track and set --strip-across and --strip-gaps on the track"
    onDarkSlab: "re-map --color-text-primary on that band; the dots and arrows paint from it"
  badge:
    backgroundColor: "transparent"
    textColor: "{colors.text-secondary}"
    border: "{structure.border-hairline}"
    typography: "{typography.label} mono, weight 500"
    rounded: "{rounded.full}"
    padding: "4px 12px"
    dot: "{colors.brand-lime} (6px, stays lime in both themes; the word carries meaning)"
  chip:
    backgroundColor: "{colors.surface-sunken}"
    textColor: "{colors.text-primary}"
    border: "{structure.border-hairline}"
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

Hand this file to an AI coding agent or a contractor, and they can build a page that feels like
natemills.me without the repo or any build tools. Every value in the generated blocks comes straight
from `tokens.json`, the DTCG token source in the public repository, so it can't drift.

## Use the published CSS

Link the foundation. Do not rebuild it from the values above.

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Work+Sans:ital,wght@0,400..800;1,400..800&display=swap" rel="stylesheet">
<link href="https://natemills.me/assets/fonts.css" rel="stylesheet">
<link href="https://natemills.me/assets/tokens.css" rel="stylesheet">
<link href="https://natemills.me/assets/components.css" rel="stylesheet">
```

`tokens.css` carries every custom property in all four themes (light, dark, and high contrast of each) and
`components.css` reads them, so tokens must load first. `fonts.css` is separate and required: it
declares the self-hosted Anton and JetBrains Mono and turns on the slashed zero. Work Sans comes from
Google Fonts, which is why that request is in the list too. Drop any one of the six and the type
silently falls back.

Icons are Lucide, and no stylesheet draws them: an `<i data-lucide="name" aria-hidden="true">` stays
empty until you load Lucide and call `lucide.createIcons()`.

Rules for using it:

- **Use the exact class names below.** Do not invent synonyms. There is no `.button`, no `.btn-primary`
  with one dash, and no `.card-dark`.
- **Do not read the stylesheet into context.** It is implementation you do not need. The table below is
  the whole public API.
- **Never `@import`, never `file://`, never a placeholder URL.** Link the absolute URLs above. You may
  copy `tokens.css` and `components.css` into the project and link them relatively, but keep `fonts.css`
  linked from natemills.me: it loads its font files from `/assets/fonts/` on whatever site serves it,
  so a copied `fonts.css` finds nothing unless your site serves those files at that same path.
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
| `.btn--secondary` | transparent, border-grey outline (stronger grey in dark); fills lime on hover |
| `.btn--icon` | the one canonical icon button: 44px circle, never a labelled pill |
| `.btn--sm` | 32px |
| `.btn--md` | 44px like base, with tighter 8px / 16px padding |
| `.btn--lg` | 52px |

**Cards:** Surface step plus a hairline border. Never a drop shadow.

| Class | Use |
| --- | --- |
| `.card` | base; its heading takes the level of where the card sits (h3 under a section h2) |
| `.card--dark` | on an always-dark slab; switches to the on-ink-* text family |
| `.card--interactive` | THE clickable-card hover: border strengthens and lifts, no fill |
| `.card--compact` | 16px padding |
| `.card--spacious` | 32px padding |
| `.card--empty` | centred empty state |
| `.card--loading` | skeleton state; fill it with .card-skel bars or it is an empty box |
| `.card-skel` | one skeleton bar inside .card--loading; pair it with a size below |
| `.card-skel--media` | media-block bar |
| `.card-skel--title` | title bar |
| `.card-skel--line` | body-line bar |

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
| `.section-title` | any heading level, picked for where it sits (h2 for a page section, h3 inside one); carries the drawn brand period |
| `.section-subtitle` | intro line under the title |

**Links:** A border-bottom underline, so the rule colours and animates independently of the text.

| Class | Use |
| --- | --- |
| `.link-underline` | base |
| `.link-underline--prose` | inside body copy |
| `.link-underline--icon` | carries a trailing glyph; give the glyph .icon-size-xs |
| `.icon-size-xs` | the trailing glyph inside .link-underline--icon: sizes it and nudges it on hover; does nothing elsewhere |

**Tabs:** Swap panels in place.

| Class | Use |
| --- | --- |
| `.tabs` | the row; role="tablist" |
| `.tabs--lg` | display-face tabs that head a whole view |
| `.tabs--compact` | mono caption tabs inside a card, each with its own underline |
| `.tab` | one tab: a <button type="button" role="tab"> |

**Carousel navigation:** The default carousel: dots bottom left, round arrows bottom right, BELOW the cards. One nav, site-wide.

| Class | Use |
| --- | --- |
| `.ds-carousel-nav` | wrapper |
| `.ds-carousel-nav--full` | phone swipe nav; also shows after a strip |
| `.ds-carousel-nav__dots` | the row of dots |
| `.ds-carousel-nav__dot` | one per card; data-on stretches the current one |
| `.ds-carousel-nav__pager` | groups the prev / next arrows |
| `.ds-carousel-nav__arrow` | 44px round prev / next |
| `.ds-carousel--strip` | wide-screen strip that bleeds to the page edge |

**Other**

| Class | Use |
| --- | --- |
| `.avatar` | round portrait |
| `.sr-only` | visually hidden, still announced |
| `.uw-range` | range slider |
<!-- DESIGN:classes:end -->

Anything not in that table is a portfolio internal, not public API. Build it yourself from the tokens.

## Overview

This is my portfolio's design system. It's calm and Swiss-minimal: one bright lime does the talking,
and everything else stays quiet. Light mode sits on a neutral off-white, dark mode on a cool
near-black. Pure white is only for cards, and the ink is never pure black. Depth comes from stepped
surfaces and 1px hairlines, never drop shadows or decorative gradients. Headings are Anton, set
large and tight. Body copy and controls are Work Sans, and JetBrains Mono carries eyebrows and
labels.

Most portfolios splash accent colour across whole sections and use soft shadows to fake hierarchy. I
don't. Colour is scarce, borders separate, and weight and scale make the hierarchy. A new page
should feel just as calm.

No framework sits underneath. It's CSS custom properties and one hand-built class layer, shipped as
static stylesheets, so build what's missing from the tokens rather than pulling in Tailwind or
Material.

### Key characteristics

- Neutral off-white canvas (`{colors.bg}`); pure white is the card surface (`{colors.surface}`), never
  the page. Ink is a cool near-black (`{colors.text-primary}`), not pure black.
- One accent, one lime (`{colors.brand-lime}`), used scarcely. Never a section fill or body text.
- Borders over shadows. Shadows are rare and reserved for overlays.
- Display type is Anton, tight tracking. Anton draws one weight (400) and no italic, and font
  synthesis is off, so a rule asking for 600 or 800 renders the real 400. Never ask this face for a
  bold or an italic it does not have, and never italicise a whole heading.
- Mono (JetBrains Mono) is for uppercase eyebrows, chips, and badges only.
- Both themes are first-class. In dark mode the accent IS the lime, by design.
- WCAG 2.2 AA in both themes is a floor, not a feature.
- Token names match the scale: words for small fixed sets (`--radius-sm`), numbers for open ramps
  (`--space-400`, `--neutral-850`), intent for roles (`--color-text-primary`). Name a new token the
  same way.

## Color roles

The palette is a neutral ramp and one lime, plus the lime's yellow partner. The
neutrals are not warm: the light end (the canvas, the white card, the sunken well) is pure grey with
no hue, and the borders, text and dark surfaces are a faintly cool zinc grey. The yellow
(`{colors.brand-secondary}`) is the colour `{colors.brand-gradient}` runs into, and it appears in
gradients beside the lime, not as a flat colour of its own. There is no
status colour: no error, success, warning or info (external brand colours like a client blue are locked constants used
only inside their own case-study or logo context, never as system colour).

**Brand voltage rule: use the lime (`{colors.brand-lime}`) ONLY for** the primary button fill, brand
outlines (`{colors.border-brand}`), focus rings on dark surfaces, the lime period after a section
title, status dots, and the footer slab. **Never** use lime as body
text, as a link on a light background, as a section background, or as a large fill on the light page.
On the off-white canvas raw lime composites to roughly 1.06:1 and fails WCAG outright.

**The theme-aware accent.** `{colors.accent}` is the one interactive role that follows the theme: it
resolves to ink on light and to lime on dark. Anything that signals an active or selected state
(current nav item, pressed toggle) uses `accent`, never raw lime, so it
stays legible on the light page. `{colors.border-brand}` is the deliberate exception: it stays fixed
lime in both themes because it is a brand-identity outline, not a state signal.

**Dark-mode accent is the lime, deliberately.** On the dark theme, `accent`, `link`, and `focus-ring`
all resolve to brand lime. This is a locked brand ruling, not a contrast bug: lime on near-black reads
at roughly 17:1 (AAA). Do not "fix" it to a near-white. What is forbidden in dark mode is a solid lime
panel; the calm dark treatment is charcoal with lime text, not lime wallpaper.

**Text on dark slabs.** Some surfaces (testimonials, contact) stay near-black in both themes. Text on
them uses the solid `{colors.on-ink-primary}` or `{colors.on-ink-secondary}`, never the theme-aware
text tokens. `{colors.on-ink-muted}` and `{colors.on-ink-border}` are see-through and never text: they
are for dots, quiet fills and hairlines. Do not use an `on-ink` colour on a light surface; it is
white-on-dark only and will vanish on a white card.

**Colours that read alike.** `{colors.surface-inverse}` is the near-black band itself;
`{colors.brand-ink}` is the charcoal for a card on that band and for text on lime.
`{colors.brand-lime-dim}` is lime's hover step. `{colors.brand-lime-vivid}` and
`{colors.brand-secondary}` share a value today but do different jobs: vivid is only the gradient's
end stop, and secondary is the named second brand colour. Neither is a flat fill.

**How the themes switch.** A page follows the visitor's OS dark setting on its own. Set
`data-theme="dark"` or `data-theme="light"` on `<html>` to pin one. High contrast applies by itself
under `prefers-contrast: more`, in both themes, so there is nothing to build. All of this works only
through the semantic names.

## Typography rules

- Weight and scale carry hierarchy, never opacity. Do not dim body text with alpha to make it read
  secondary; step down a text style instead.
- Display is always roman. A full italic heading is banned. Italic is allowed on a single word or short
  phrase inside a heading, and only when paired with a muted colour to mark it as secondary emphasis.
- Eyebrows and labels are uppercase JetBrains Mono with positive tracking (0.08em labels, 0.18em
  eyebrows) to mark them as taxonomy.
- Body copy is `text-align: start`, ragged right. Never justify.
- Line length caps at 52ch. The 11px mono label (`--text-label`) is the floor; never go smaller.

## Component stylings

- **Buttons** are full pills, Work Sans semibold at 14px, padding 10px/18px, default height 44px. The
  primary button is a lime fill with ink label; on hover it inverts to an ink fill with a lime label.
  The secondary button is transparent with a `{colors.border}` outline (a stronger grey in dark) and
  on hover takes the primary's resting look: a lime fill with an ink label. In a form row the field
  takes the spare width and the button keeps its own.
- **Icon button** is the one canonical circle: a `{colors.border}` hairline ring,
  `{colors.text-primary}` glyph, 44px, `{rounded.full}`, filling lime on hover. Never a pill with a
  label.
- **Cards** sit on `{colors.surface}` with a 1px `{colors.border}` hairline and `{rounded.xl}`, padded
  24px (compact 16, spacious 32). Interaction is outline-plus-lift, not a background fill. Cards on a
  dark slab use the `card-dark` recipe, whose fixed ink and `on-ink-*` tokens keep it dark in both
  themes. Never pin `data-theme` on an element to force a look: the pin survives when the element is
  cloned and silently breaks dark mode.
- **Loading card** is `.card--loading` filled with `.card-skel` bars, one per line of the content it
  stands in for. Without the bars it is an empty box. The shimmer stops under reduced motion.

```html
<div class="card card--loading">
  <span class="sr-only">Loading</span>
  <div class="card-skel card-skel--media"></div>
  <div class="card-skel card-skel--title"></div>
  <div class="card-skel card-skel--line"></div>
</div>
```

- **Tabs** are one row of real buttons tied to their panels. A script moves focus and shows the chosen
  panel; the published CSS only draws them.

```html
<div class="tabs tabs--compact" role="tablist" aria-label="Project views">
  <button class="tab" type="button" role="tab" id="tab-overview" aria-selected="true" aria-controls="panel-overview">Overview</button>
  <button class="tab" type="button" role="tab" id="tab-specs" aria-selected="false" aria-controls="panel-specs" tabindex="-1">Specs</button>
</div>
<div role="tabpanel" id="panel-overview" aria-labelledby="tab-overview">Overview content</div>
<div role="tabpanel" id="panel-specs" aria-labelledby="tab-specs" hidden>Specs content</div>
```

- **Range slider** is a native `<input type="range">` with a `<label>`: a 44px hit area, a 16px track,
  a 20px thumb. The accent fill left of the thumb reads `--range-pct`, a percentage the page sets on
  the input as the value changes; without it the track shows no fill and the slider still works.

```html
<label for="size">Size</label>
<input class="uw-range" type="range" id="size" min="20" max="56" step="2" value="30" style="--range-pct: 30%">
```

- **Chips vs badges vs dots** resolve by job: a label is a chip, a status or a count is a badge, a
  position in a carousel is its dots, never a badge or a number. A badge is read-only and never
  interactive; its dot stays lime in both themes but colour is never the only signal, every status
  also carries a word.
- **Carousel nav** sits below the cards: dots bottom left, two round arrows bottom right, with no
  progress bar and no count. One dot per card, 8px in `{colors.text-primary}` at 30% alpha; the
  current one fills and stretches to 24px. The arrows are `{structure.touch-target-min}` circles in
  `{colors.text-primary}` at 12% alpha.
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
- **A link with a trailing glyph** is `.link-underline--icon`, and the glyph takes `.icon-size-xs`,
  which sizes it to the label and nudges it on hover. Without that class the glyph renders unsized.

```html
<a class="link-underline link-underline--icon" href="https://example.com" target="_blank" rel="noopener noreferrer">
  Verify the credential<span class="sr-only"> (opens in a new tab)</span>
  <i class="icon-size-xs" data-lucide="arrow-up-right" aria-hidden="true"></i>
</a>
```

## Layout principles

- Content sits in a wide band that stays proportional on normal screens and caps at 1680px so
  ultrawide layouts do not stretch without earning it.
- One container width per section: the 960px prose column (`--container-base`) or that wide band
  (`--container-wide`, for grids). No middle ground, so every section's gutter lines up.
- Vertical rhythm: every section pads top and bottom by `{spacing.section-padding}`, so a gap is two
  units at every width. Beside a colour band, the plain-side neighbour doubles its own edge so the
  plain side still reads as two units. Never halve a gap for phones; the unit already shrinks.
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

Each rule carries its reason, so a rule whose reason no longer holds can be argued with instead of
inherited. A rule that rests on a house choice rather than a standard says so.

Do:
- Do keep the lime scarce. If two primary buttons would appear in one viewport, make one secondary.
  Because: lime is the accent, never the wallpaper; the page stands against portfolios that scatter
  colour, and an accent used everywhere stops marking anything.
- Do build hierarchy from weight and scale. Because: the other lever, opacity, quietly drops text
  below contrast on some surfaces.
- Do use `{colors.accent}` for any active or selected state so it stays legible on light. Because:
  raw lime on a light surface is about 1.06:1 and cannot carry state.
- Do give every status a word, not just a coloured dot. Because: colour alone fails anyone who
  cannot see the colour.
- Do design the static, reduced-motion frame first; motion is garnish that never carries meaning.
  Because: the still frame is what every visitor with reduce motion switched on gets, and what the
  deploy checks test.

Don't:
- Don't use pure white as the page canvas or pure black as ink. The canvas is `{colors.bg}`.
  Because: full white against full black glares, and in dark mode bright text can seem to glow and
  blur, worst for readers with astigmatism. Softer ends still clear WCAG contrast.
- Don't put lime on a light background as text, a link, or a large fill (it fails WCAG at ~1.06:1).
- Don't paint a solid lime panel in dark mode; use charcoal with lime text. Because: lime is an
  accent, never wallpaper; charcoal with lime text reads at roughly 15:1.
- Don't dim text with opacity to fake a secondary tone; step down a text style. Because: opacity
  blends with whatever sits behind it, so the same colour passes on one surface and fails on the
  next, and no checker reading the source sees it.
- Don't italicise a whole heading, and don't use an alpha colour for heading emphasis. Because:
  Anton has no italic, so the browser fakes one, and see-through glyphs leave dark spots where tight
  letters overlap.
- Don't reach for a drop shadow to separate a card; use a hairline border. Because: there is no
  elevation scale on purpose; depth is the surface ladder plus an edge, the Swiss-minimal choice.
- Don't justify body text. Because: justified text opens rivers between words and slows scanning,
  worst for dyslexic and low-vision readers; use `start`, not `left`, so right-to-left text mirrors.
- Don't drop below the 11px mono label floor (`--text-label`). Because: it is a house floor, not a
  standard; WCAG sets no minimum size, and 11 matches Apple's smallest recommended text size.
- Don't leak an external client brand colour into general UI; those are locked constants for their
  own case-study context only. Because: they are reproduced for accuracy, never themed and never
  aliased into a semantic token.

## Voice and tone

The words follow one rule, the same way the colours do. A page that governs its pixels but lets its
copy wander still feels inconsistent.

- Write in the first person, in plain words, the way one designer talks to another over coffee.
- Let proof carry the brag. Numbers, not superlatives: "18 hours back to the team", never "huge
  productivity gains".
- Say who changed, and how we know. Name the people (customers, designers, engineers, squads) and
  what they now do differently. A feeling needs a measure or a quote: "gave them confidence" and
  "built trust" are claims nobody can check.
- No hedges. Say it or don't.
- Body sentences run 6 to 14 words, one idea each.
- Headings are sentence case, everywhere.

The voice never changes; only the length does. Short copy compresses it:

- **Buttons:** verb plus outcome. "Read the case study", "Get in touch". A button that only names where it goes can be the name alone: "LinkedIn", "Resume".
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
  This system's colour is the set under **Color roles**: neutral greys and one lime with its yellow
  gradient partner.
- No gradient text, glows, blobs, mesh backgrounds, glass, noise overlays, or fake depth. The site keeps
  glass for its own chrome and overlays (the header, menus, tooltips, Ask AI, modal backdrops and the
  scroll-edge blur); do not add it to a page you build. The one
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

Reference breakpoints, each a token: mobile 375px (`--bp-mobile`), tablet 768px (`--bp-tablet`), desktop
1024px (`--bp-desktop`), wide 1440px (`--bp-wide`), ultrawide 1600px (`--bp-ultrawide`). A media query cannot
read a custom property, so the CSS writes the number and the token records it.

- Type is fluid via `clamp()` and capped, so headings grow on wider screens and stop; they never balloon.
- At and below 768px, section-level primary CTAs go full-width and centre for a thumb-friendly tap
  target; inline buttons inside paragraphs stay auto-width.
- Dense value tables tighten below ~640px but never drop a column and never shrink labels below 11px (`--text-label`).
- Touch targets meet 44px (`--touch-target-min`). The dense `.btn--sm` is 32px (`--btn-sm`) with no larger tap area around it, which still
  clears the WCAG 2.5.8 AA 24px minimum; nothing goes below 24px.
- Verify layout at ~375px alongside both light and dark themes whenever you touch a layout.

## Agent prompt guide

When building a new page or prototype with this system:

1. Work one component at a time and reference tokens by name (`{colors.accent}`, `{typography.h1}`,
   `{rounded.lg}`), never by inventing a hex or px value.
2. Decide first which surface a section sits on (`bg`, `surface`, `surface-sunken`, or an always-dark
   `surface-inverse`), then pick text colours to match: `text-*` on light, `on-ink-primary` or `on-ink-secondary` on dark
   slabs.
3. Keep the lime scarce. It appears on the primary button, brand outlines, focus rings on dark, status
   dots, and the footer. Nowhere else.
4. For any active or selected state use `{colors.accent}` (theme-aware), not raw lime, so it survives
   the light theme.
5. Build hierarchy from scale, not opacity. Anton ships one weight (400), so display size does the work; body runs 400 to 600.
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
- There is no status colour: no error, success or warning. A portfolio has no such UI, so the one
  error pair and `.card--error` were removed on 2026-10-25. Say what happened in words. If a consumer
  needs a status colour, add it at the token layer first, then route a semantic.
- Fonts are Anton (display), Work Sans (body and controls) and JetBrains Mono (labels and numbers).
  All three are open source. If one is unavailable, fall back to a condensed grotesque for display,
  a neutral grotesque for body, and any monospace with a slashed zero for labels.
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
