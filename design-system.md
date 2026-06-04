# Nate Mills Design System

This is the system that powers my portfolio: the philosophy, the token model, the rules, and the
file map. It is small on purpose, and strict on purpose. If you came to see how a one-person design
system stays consistent without a framework or a build pipeline you have to babysit, this is the
whole thing.

---

## Philosophy

A design system is easy to start and hard to keep honest. Most do not die at launch. They fall
apart later, quietly, when nobody is looking: a stray hex here, a one-off font size there, a card
that drifts a few pixels from its siblings. This system is built so that drift is hard to introduce
and easy to catch.

Four values shape every decision:

- **One source, one edit.** Every value lives once, in `tokens.json`. Change a primitive and every
  semantic and component that references it follows. Reskinning the brand is a single line.
- **Accessible by default.** Accessibility is a constraint the system enforces, not a checklist bolted
  on at the end. Tokens that cannot pass contrast are simply not allowed where they would fail.
- **Restraint over reach.** One accent, a tuned neutral scale, two fonts. No states the portfolio
  does not use, no themes it does not need. The smaller the system, the easier it is to govern.
- **Plain platform.** CSS custom properties, semantic HTML, no runtime framework. The whole thing
  loads in one network round trip and works even when opened as a local file.

**Who this is for.** Engineers reading the token and component layers, designers reading the scales
and rules, and anyone evaluating whether the claims this portfolio makes about systems are real.

---

## Getting started

- **If you build interfaces:** start with `tokens.css` (the generated variables) and `components.css`
  (the classes that consume them). Read the semantic table below to learn which role token to reach
  for.
- **If you design:** start with the Typography, Spacing, and Colour sections. The scales are short
  and the reasoning for each is written down.
- **If you write product copy:** jump to Content Voice and Tone at the end. The system governs words
  as well as pixels.
- **If you maintain the system:** read the Contribution Rules and the Guardrails. They are the
  difference between a system and a stylesheet.

---

## 1. The token model

```
Tier 1  PRIMITIVES   Raw values, named by hue and stop. No meaning on their own.
Tier 2  SEMANTICS    Roles. Reference primitives through var(). Consumed by every component.
Tier 3  COMPONENTS   CSS classes that read semantics only. The only layer that styles markup.
```

The rule is one-way: components read semantics, semantics read primitives, primitives are literals.
No component reads a primitive directly. The one exception is the `[data-theme="dark"]` block, which
re-binds the same semantic names to a different set of primitives. This is the same shape that
Polaris, Carbon, and Material 3 standardise around, for the same reason: when you change a primitive,
every semantic that references it follows, and every component that reads those semantics follows.

**The pipeline.** The tiers are authored once in `tokens.json`, in the
[W3C Design Tokens Community Group](https://www.designtokens.org/) (DTCG) format. `tokens.css` is
generated from that source by [Style Dictionary](https://styledictionary.com), the open-source
standard token build tool. The same source could also emit iOS, Android, or JS from one edit; here
it emits the CSS the site consumes. The workflow is simple: edit `tokens.json`, run the build, never
hand-edit `tokens.css`. A drift guard rebuilds the tokens at deploy time and refuses to ship if the
committed CSS does not match what the source generates.

Honest scope note: DTCG is a Community Group format, the industry's interoperability standard, not a
formal W3C Recommendation, and the colour module is still settling. "DTCG-format" is accurate;
"fully spec-compliant" would not be.

---

## 2. Primitives

Defined once at `:root`. Mirrored in a small inline block in the page so it renders without external
CSS.

**Neutrals.** A custom 16-stop scale, tuned so the brand ink (`--neutral-850 #1c1c1f`) sits a touch
warmer than Tailwind's zinc-900. A few half-steps (`-150`, `-550`, `-850`) preserve values that the
rendered design actually lands on but that do not fall on a clean grid.

| Token | Hex | Where it shows up |
|---|---|---|
| `--neutral-0` | `#ffffff` | Card surface, text on accent |
| `--neutral-100` | `#f5f5f5` | Page background (brand off-white) |
| `--neutral-300` | `#e4e4e7` | Hairline border |
| `--neutral-700` | `#3f3f46` | Secondary text (light) |
| `--neutral-850` | `#1c1c1f` | Brand ink, accent (light), subtle surface (dark) |
| `--neutral-950` | `#0a0a0b` | Page background (dark), primary text (light) |

**Green (lime).** The only colour primitive the brand needs. `--green-500 #d2ff37` is the brand
lime; the rest are derived for hover and dim states.

**Authored in OKLCH.** The colour primitives are written in OKLCH, the perceptual colour space from
CSS Color Module Level 4 (by Björn Ottosson), as DTCG colour objects that also carry the original
hex. The build emits a hex fallback line then the `oklch()`, so the colour is identical everywhere
and pre-2023 browsers still get the hex. The OKLCH values are exact conversions of the hand-tuned
hexes, verified to land on the same pixel, not a regenerated ramp, so the lime keeps its character.

**What is deliberately missing.** No emerald, amber, or red. A portfolio has no warning or error UI,
and padding the system with state colours no component reads would be the opposite of the discipline
it is meant to show. If a future consumer needs them, the rule is: add at the primitive layer, route
a semantic, then consume that. Lime plus neutrals is the entire palette.

---

## 3. Semantics

Roles that reference primitives through `var()`. Every component reads these, never raw hex.

| Token | Light | Dark | Role |
|---|---|---|---|
| `--color-bg` | `--neutral-100` | `--neutral-950` | Page background |
| `--color-bg-elevated` | `--neutral-0` | `--neutral-900` | Raised surface |
| `--color-text-primary` | `--neutral-950` | `--neutral-150` | Body and headings |
| `--color-text-secondary` | `--neutral-700` | `--neutral-500` | Supporting copy |
| `--color-border` | `--neutral-300` | `--neutral-800` | Hairline |
| `--color-accent` | `--neutral-850` | `--neutral-150` | Primary accent (ink, not blue) |
| `--color-focus-ring` | `--neutral-850` | `--neutral-150` | Focus outline |

**Brand identity aliases** sit alongside the role tokens: `--brand-lime` (`var(--green-500)`),
`--brand-ink` (`var(--neutral-850)`), and the paired "on" tokens that name the correct text colour
for a fixed-colour surface (`--brand-on-lime` resolves to ink, `--brand-on-ink` resolves to lime).

**The one rule worth memorising.** The base accent is ink, not colour. Lime is a background and
accent, never foreground text on a light surface. The contrast math forces it: `#d2ff37` on
`#f5f5f5` is 1.3 to 1, far below the 4.5 to 1 floor. So the system gives you the right tool instead:
`--color-brand-emphasis` (theme-aware, resolves to ink on light and lime on dark) for brand-tinted
words in running copy, and the "on" tokens for text on fixed lime or ink surfaces. If you reach for
`color: var(--brand-lime)` outside a known-dark scope, it is almost always the wrong token.

---

## 4. Typography

**Two fonts, no more.** Inter for everything; JetBrains Mono for labels, eyebrows, code, and tabular
numbers. PT Serif appears in exactly one place: the testimonial pull quotes.

The lean semantic scale that new work consumes:

| Token | Value | Used for |
|---|---|---|
| `--text-h1` | `clamp(34px, 5.8vw, 72px)` | Section headings and the hero |
| `--text-h2` | `clamp(22px, 4vw, 32px)` | Card titles, ledes |
| `--text-body` | `16px` | Reading text |
| `--text-label` | `11px` | Uppercase mono labels and eyebrows |
| `--text-caption` | `12px` | Captions and fine print |

Headings use fluid `clamp()` so type scales smoothly between a mobile floor and a desktop ceiling
without per-breakpoint overrides. If you find yourself reaching for a media query to nudge a font
size, the floor or the ceiling is wrong; fix the clamp, not the breakpoint.

Five weights are loaded from Inter (400 to 800). One emphasis rule matters: a full italic display
heading is banned. Italic on a single word inside a heading is allowed, paired with a solid muted
token, never an alpha-modified colour (overlapping italic glyphs at tight tracking double the alpha
and leave visible dark spots at the letter joins).

---

## 5. Spacing

A doubling rhythm from 4 to 256 px, with two medium-tight additions for breaks that need them.

```
--space-1  4px     --space-5  24px    --space-9   96px
--space-2  8px     --space-6  32px    --space-10  128px
--space-3  12px    --space-7  48px    --space-11  192px
--space-4  16px    --space-8  64px    --space-12  256px
```

Never use raw px for spacing in a component. The whole point is one place to edit the rhythm.

---

## 6. Radii, borders, shadows

```
--radius-sm    8px     (cards, modals; full scale is sm / md / lg / xl)
--radius-full  999px   (pills, tags, buttons)

--border-hairline  1px solid var(--color-border)
--border-focus     2px solid var(--color-focus-ring)

--shadow-soft   subtle    (default lift)
--shadow-lift   stronger  (overlays and float-on-scroll chrome only)
```

The aesthetic is Swiss-minimal, so borders carry structure and shadows are rare. Two small
accent-shadow tokens keep the lime accents legible on light backgrounds and resolve to `none` in
dark mode, where lime already reads cleanly.

---

## 7. Motion

```
--duration-fast  150ms   (hover, focus)
--duration-base  220ms   (reveal, swap)
--duration-slow  400ms   (context shift)

--ease-default   cubic-bezier(0.4, 0, 0.2, 1)
```

Every animation respects `prefers-reduced-motion`. A single override at the bottom of `tokens.css`
collapses every duration to 1 ms and disables transforms, so honouring the preference is automatic,
not per-component.

---

## 8. Layout

```
--container-base   960px    (prose, single-column sections)
--container-wide   1200px   (galleries, grids)

--bp-mobile  375px   --bp-tablet  768px   --bp-desktop  1024px   --bp-wide  1440px
```

Sections run full-bleed at the outer level and centre their content in one of the two container
widths, so every section's gutter aligns.

---

## 9. Exemplar components

Components live in `components.css`, read semantic tokens only, and document their variants. Three
are worth showing in full, because they carry most of the system's decisions.

### Button

| Variant | Background | Text | Use on |
|---|---|---|---|
| `.btn--primary` | `--brand-lime` | `--brand-ink` | Off-white surfaces |
| `.btn--secondary` | transparent | `--color-text-primary` | Lime surfaces |
| `.btn--icon` | transparent | `--color-text-secondary` | Chrome (toggles, controls) |

The pairing rule is strict: lime-on-lime is forbidden, so `.btn--primary` never sits on a lime
background; the secondary variant carries contrast there with ink text and a border. Icons trail the
label and map to action type: `mail` for `mailto:`, `external-link` for outbound links, `download`
for files, no icon for same-page anchors. `arrow-up-right` is not a substitute for `external-link`;
they mean different things to a screen-reader user.

### Card

`.card` is the light-surface base: off-white background, hairline border, soft radius. `.card--dark`
is the modifier for dark slabs: it swaps the surface to ink, the text to the on-ink tokens, and the
border to the on-ink hairline, while inheriting the radius and border style from `.card`. Compose it
as `class="card card--dark"`. A surface that must stay dark in both themes uses these fixed tokens,
never a pinned `data-theme`, because a pinned theme propagates when an element is cloned and silently
breaks dark mode.

### The section heading triplet

Every section uses one heading pattern: a label, a title, and a subtitle. Shape signals role across
the whole system: pills are identity (status, taxonomic tags), rounded rectangles are actions
(buttons, cards), circles are people and brands (avatars, social icons), squares are chrome
utilities (toggles). Mixing those metaphors is the fastest way to make an interface feel arbitrary,
so the system names the rule and holds to it.

---

## 10. Accessibility

- WCAG 2.2 AA contrast for every text token, verified against every surface it can land on. The
  ratios are written into the comments in `tokens.css`.
- The focus ring is a 2 px brand outline, never removed without a replacement.
- Touch targets clear 44 by 44 px.
- Every animation is gated behind `prefers-reduced-motion`.
- Semantic HTML first; ARIA only where HTML cannot carry the meaning.
- Lime is forbidden as foreground text on light surfaces. Decorative bars, the brand dot, and
  dark-slab accents only.
- **Never dim accessible text with `opacity`.** Opacity multiplies against whatever sits behind the
  element and silently drops a passing colour below 4.5 to 1. The token looks right in the source and
  fails on screen. Choose a lighter text token that itself clears the floor.
- Every `<img>` declares `width` and `height` to prevent layout shift, which disorients screen-reader
  and magnifier users tracking position.

---

## 11. File map

```
tokens.json      The single source of truth (DTCG format)
tokens.css       Generated CSS custom properties (primitives + semantics)
components.css   The component layer
design-system.md This document
```

`tokens.json` is the source; `tokens.css` is generated and never hand-edited. The page also keeps a
small inline mirror of the token block so it renders correctly when opened as a local file.

---

## 12. Contribution rules

1. Never write raw hex outside `tokens.css`. Define a primitive or use a semantic.
2. Brand tokens are aliases, not duplicates: `--brand-lime: var(--green-500)`, not the hex.
3. Components read semantics only, never a raw primitive.
4. Test in light and dark. Every semantic has both.
5. WCAG 2.2 AA for every text colour, against every surface it could land on.
6. Every animation gets a reduced-motion collapse.
7. One container width per section.
8. The label, title, subtitle triplet is the only heading pattern.
9. No full italic display headings.
10. Be explicit about which viewport a CSS change targets, and verify at three widths before calling
    it done.

---

## 13. What this system is NOT

- Not a component library. The custom build is the point; there is no DaisyUI or Material under it.
- Not Tailwind-driven. Tailwind is a one-off layout convenience, not the system.
- Not runtime CSS-in-JS. Plain custom properties, one network round trip.
- Not theme-able beyond light and dark. The Bupa case study scopes blue back inside its own section;
  that is the only third theme, and it is section-scoped, never global.

Fork it for another brand by changing `--green-500` and watching every consumer follow. That is the
system working as designed.

---

## 14. Guardrails

The mistakes that have actually surfaced, kept here so they do not surface again.

- No blue outside the Bupa case study. The base accent is ink.
- Inter only. PT Serif for pull quotes, JetBrains Mono for labels and numbers.
- No full italic display headings.
- Surfaces are off-white or near-black only. No cream, no tinted "warm" backgrounds.
- Lime is never foreground text on a light surface.
- No raw values in components. Every colour, space, radius, and duration resolves to a token.

---

## 15. Content voice and tone

Consistency is linguistic, not just visual. A system that governs pixels but lets copy wander still
feels inconsistent. These are the registers that keep every surface sounding like one author.

### Voice A, body copy (Craftsman)

Confident, evidence-led, quietly warm. Used in subheads, About, section subtitles, case study ledes.
Sentences run 6 to 14 words. First person. Proof carries the brag: "18 hours back to the team," not
"huge productivity gains." Warmth comes from honesty, not enthusiasm. No hedges.

### Voice B, CTAs and microcopy (Confident)

Verb-first, outcome-specific, three to five words. "Read the case study," "Get in touch," "View on
Figma." Never "Submit," "Click here," or "Learn more." Errors name the problem and the workaround
with no apology preamble. Status pills are declarative present tense ("Available for work"), never
aspirational.

### Voice C, system docs (Engineering register)

Drier than the site, which is why this document reads the way it does. Statements of fact in present
tense. Decisions explained, not defended. Mostly third-person system-speak.

### Word list

| Use | Avoid |
|---|---|
| system, token, governance, pipeline, foundation | passionate, world-class, cutting-edge, seamless |
| ship, scale, adoption, contribution | amazing, incredible, excited |
| multi-brand, cross-platform, token-driven | we believe, we think, arguably |
| let's talk, get in touch | click here, learn more, submit |

### Copy patterns

- **CTA buttons:** verb plus outcome. "Read the case study," not "Click to learn more."
- **Section subtitle:** one sentence, sets the stake, 18 words or fewer.
- **Error message:** what happened plus the workaround, no "sorry."
- **Empty state:** what is missing, what to do.
- **Loading state:** set an expectation if it runs over a second, otherwise no copy.

Across all three registers: numbers do the bragging, headings are sentence case, and superlatives
stay out.
