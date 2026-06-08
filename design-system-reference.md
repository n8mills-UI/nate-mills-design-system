# Nate Mills portfolio design system

The architecture, the rules, and the file map for the design system that powers this portfolio. This is the single source of truth for the brand and the system, and the portable brief to hand a contractor or another AI model. The under-the-hood page is the visual specimen.

If you came here to verify the system claims this portfolio makes, this document is the audit trail. If you came here to extend it, the rules below tell you which layer to edit.

---

## 1. Architecture, the three-tier model

```
Tier 1, PRIMITIVES        →  Raw values. Named by hue and stop only.
                              No semantic meaning. Rarely consumed directly.
                              File: tokens.css, top of :root.

Tier 2, SEMANTICS         →  Reference primitives. Named by role.
                              Consumed by every component.
                              File: tokens.css, after the primitive block.

Tier 3, COMPONENTS        →  Pre-built CSS classes that consume semantics.
                              The only layer that ships markup-level styling.
                              File: components.css (extracted into its own file).
```

The rule is one-way: components read semantics, semantics read primitives, primitives are literals. No component reads a primitive directly. No semantic reads a literal. The exception is the `[data-theme="dark"]` block, which re-binds the same semantic names to a different primitive set.

This shape is what design systems like Polaris (Shopify), Carbon (IBM), Material 3 (Google), and Bupa's token consolidation work all standardise around. The reason: when you re-skin a brand, you change a primitive, every semantic that references it follows, every component that reads those semantics follows. One edit, full propagation.

### The pipeline, single source of truth

The three tiers are **authored once**, in `tokens.json` (the W3C Design Tokens Community Group format, the DTCG Format Module 2025.10, its first stable version). `tokens.css` is **generated** from that source by [Style Dictionary](https://styledictionary.com), the open-source industry-standard token build tool. The same `tokens.json` could also emit iOS, Android, or JS from one edit; here it emits the CSS the site consumes.

Two guards keep it honest:

- A **drift guard** in the deploy (`scripts/deploy-netlify.sh`) rebuilds the tokens and refuses to publish if the committed `tokens.css` does not match what `tokens.json` generates, naming the offending token.
- The on-page "Under the Hood" specimen is **also generated** from `tokens.json` (radii, spacing, colour, type), with its own guard, so the live showcase can never silently fall out of sync with the real tokens. It cannot, for instance, show 3 of 6 radii.

**Workflow: edit `tokens.json`, run `bash tokens/build.sh`, never hand-edit `tokens.css`** (its header says GENERATED). The build files live in `tokens/` (`build.mjs`, `build.sh`, `showcase.mjs`, `showcase.manifest.js`, `README.md`).

Honest scope note for any claim made from this: DTCG 2025.10 is a *W3C Community Group* specification (the industry's interoperability format), not a W3C Recommendation/Standard, and Style Dictionary v5 does not yet fully implement the 2025.10 colour module, so "DTCG-format" is accurate where "fully spec-compliant" would not be.

---

## 2. Primitives

Defined once at `:root` in `tokens.css`.

The neutral scale is 15 stops, tuned so `--neutral-850 #1c1c1f` (the brand ink) sits warmer than Tailwind's zinc-900 `#18181b`. Half-step numbers (`-150`, `-550`, `-850`) preserve specific values that don't fall on a clean 100 grid but appear in the rendered design. The green scale is 12 stops, the only colour primitive the brand needs: `--green-500 #d2ff37` is the brand lime, the rest derived for hover, dim, and dark-mode link states.

The colour primitives are authored in OKLCH (the perceptual colour space defined in CSS Color Module Level 4, created by Björn Ottosson) as DTCG colour objects that also carry the original sRGB hex. `tokens.css` emits a hex fallback line then the `oklch()` line, so the rendered colour is identical everywhere and pre-2023 browsers still get the hex. The OKLCH values are exact conversions of the hand-tuned hexes, verified to round-trip to the same pixel, so the ramp keeps its deliberate non-uniform character: `--green-600` carries higher OKLCH chroma (0.229) than the brand `--green-500` (0.2134). They are converted, not regenerated. External brand colours (`ext-brand-*`) and the glitch effect stay as exact vendor hex.

<!-- TOKENS:primitives:start -->

**Neutrals (custom zinc scale)**

| Token | Hex | OKLCH | Description |
|---|---|---|---|
| `--neutral-0` | `#ffffff` | `oklch(100% 0 0)` | Card surface; text on an accent fill. |
| `--neutral-50` | `#fafafa` | `oklch(98.5% 0 0)` | Elevated surface (legacy). |
| `--neutral-100` | `#f5f5f5` | `oklch(97% 0 0)` | Page background, the brand off-white. |
| `--neutral-150` | `#f4f4f5` | `oklch(96.7% 0.001 286.4)` | Half-step. accent-subtle on light; text-primary on dark. |
| `--neutral-200` | `#ececec` | `oklch(94.3% 0 0)` | Subtle surface; accent-subtle on light. |
| `--neutral-300` | `#e4e4e7` | `oklch(92% 0.004 286.3)` | Hairline border on light (--color-border). |
| `--neutral-400` | `#d4d4d8` | `oklch(87.1% 0.005 286.3)` | Strong border on light (--color-border-strong). |
| `--neutral-500` | `#a1a1aa` | `oklch(71.2% 0.013 286.1)` | Text-secondary on dark. |
| `--neutral-550` | `#909096` | `oklch(65.5% 0.009 286.2)` | Half-step. Text-tertiary on dark. |
| `--neutral-600` | `#67676f` | `oklch(51.7% 0.012 286)` | Text-tertiary on light; section labels. |
| `--neutral-700` | `#3f3f46` | `oklch(37% 0.012 285.8)` | Text-secondary on light; strong border on dark. |
| `--neutral-800` | `#27272a` | `oklch(27.4% 0.005 286)` | Border on dark. |
| `--neutral-850` | `#1c1c1f` | `oklch(22.8% 0.006 285.9)` | Half-step. Brand ink; accent on light; bg-subtle on dark. |
| `--neutral-900` | `#141416` | `oklch(19.2% 0.004 286)` | bg-elevated on dark. |
| `--neutral-950` | `#0a0a0b` | `oklch(14.5% 0.002 286.1)` | bg on dark; text-primary on light; accent-hover on light. |

**Green (lime, the brand colour)**

| Token | Hex | OKLCH | Description |
|---|---|---|---|
| `--green-50` | `#faffeb` | `oklch(99.1% 0.027 118.3)` | Near-white lime tint, decorative only. |
| `--green-100` | `#f5ffd6` | `oklch(98.2% 0.054 118.5)` | Pale lime tint band. |
| `--green-200` | `#ecffad` | `oklch(96.7% 0.106 119)` | Light lime tint band. |
| `--green-300` | `#e2ff85` | `oklch(95.38% 0.151 120.4)` | Light lime tint band. |
| `--green-400` | `#daff61` | `oklch(94.4% 0.185 121.3)` | Lime tint, one step under the brand value. |
| `--green-500` | `#d2ff37` | `oklch(93.6% 0.2134 122.24)` | Brand lime. The single canonical lime, the only stop consumed as identity (--brand-lime). |
| `--green-550` | `#b8e030` | `oklch(84.9% 0.193 122.3)` | Hover-dim lime, between 500 and 600; the target of --brand-lime-dim. |
| `--green-600` | `#c0fa00` | `oklch(91.2% 0.229 124.9)` | Saturated lime shade. Higher OKLCH chroma (0.229) than green-500 (0.2134), the deliberate hand-tuned saturation peak. |
| `--green-700` | `#8db800` | `oklch(72.47% 0.1815 124.72)` | Mid lime shade. |
| `--green-800` | `#5e7a00` | `oklch(53.8% 0.134 124.1)` | Deep lime shade. |
| `--green-900` | `#2f3d00` | `oklch(33.5% 0.082 122.9)` | Darkest usable lime, a near-black green. |
| `--green-950` | `#171f00` | `oklch(22.3% 0.054 122.4)` | Lime-black; accent-subtle on dark (--color-accent-subtle). |

<!-- TOKENS:primitives:end -->

### Semantic-state primitives

**Intentionally omitted.** A portfolio has no warning or error UI; padding the system with emerald / amber / red primitives that no consumer reads would be the opposite of the design-system discipline this page sells. If a future consumer needs them, the rule is: add at the primitive layer first, route a `--color-success / warning / danger` semantic, then consume that. The lime + neutrals split below is the entire portfolio palette.

---

## 3. Semantics

Reference primitives via `var()`. Every component reads these, never raw hex.

### Surfaces and text

<!-- TOKENS:semantics-surfaces:start -->

| Token | Light | Dark |
|---|---|---|
| `--color-bg` | `--neutral-100` | `--neutral-950` |
| `--color-bg-elevated` | `--neutral-0` | `--neutral-900` |
| `--color-bg-subtle` | `--neutral-200` | `--neutral-850` |
| `--color-text-primary` | `--neutral-950` | `--neutral-150` |
| `--color-text-secondary` | `--neutral-700` | `--neutral-500` |
| `--color-text-tertiary` | `--neutral-600` | `--neutral-550` |
| `--color-on-ink-primary` | `rgba(255, 255, 255, 0.88)` | same |
| `--color-on-ink-secondary` | `rgba(255, 255, 255, 0.66)` | same |
| `--color-on-ink-muted` | `rgba(255, 255, 255, 0.4)` | same |
| `--color-on-ink-border` | `rgba(255, 255, 255, 0.08)` | same |

<!-- TOKENS:semantics-surfaces:end -->

**Text on ink.** The three `--color-on-ink-*` tokens are the foreground
text colours for the permanently-dark slabs (testimonials, contact, the Bupa
case study). They do not flip with the theme because those surfaces are dark
in both themes. They replace the 40-odd hardcoded `rgba(255,255,255,a)` /
`rgba(245,245,240,a)` text literals that were scattered across those sections.
Use `-primary` for headings and body, `-secondary` for supporting copy,
`-muted` for fine print and eyebrows. For text on a light surface, keep using
`--color-text-primary / -secondary / -tertiary`.

**Border on ink.** `--color-on-ink-border` is the matching hairline
border colour for dark slabs, the white-alpha line used by `.card--dark`, the
testimonials compact cards, the mode-toggle, and the carousel nav buttons. Like
the `--color-on-ink-*` text tokens it does not flip with the theme. It replaces
the recurring `rgba(255,255,255,0.08)` literal so dark-surface borders share one
source of truth.

### Border, accent, link

<!-- TOKENS:semantics-accent:start -->

| Token | Light | Dark |
|---|---|---|
| `--color-border` | `--neutral-300` | `--neutral-800` |
| `--color-border-strong` | `--neutral-400` | `--neutral-700` |
| `--color-accent` | `--neutral-850` | `--green-500` |
| `--color-accent-hover` | `--neutral-950` | `--brand-lime-dim` |
| `--color-accent-subtle` | `--neutral-150` | `--green-950` |
| `--color-accent-foreground` | `--neutral-0` | `--neutral-950` |
| `--color-focus-ring` | `--neutral-850` | `--green-500` |
| `--color-link` | `--neutral-850` | `--green-500` |
| `--color-link-hover` | `--neutral-950` | `--neutral-0` |

<!-- TOKENS:semantics-accent:end -->

Bupa case study scope-overrides the accent family inside `#bupa` to bring blue back where it legitimately belongs. The base accent is ink, not blue.

**Accent foreground.** `--color-accent-foreground` is the canonical name for text or icons sitting on an accent surface. The old `--color-text-on-accent` token was a never-referenced duplicate and has been removed. Any consumer needing a foreground colour on accent must use `--color-accent-foreground`.

### Brand identity (semantic aliases)

| Token | Value | Use |
|---|---|---|
| `--brand-lime` | `var(--green-500)` | Identity surface, lime band, accent on dark slabs |
| `--brand-ink` | `var(--neutral-850)` | Identity surface, dark slab background, ink type |
| `--brand-on-lime` | `var(--neutral-850)` | Text colour when sitting on `--brand-lime` |
| `--brand-on-ink` | `var(--green-500)` | Lime text on dark slabs, used sparingly |
| `--color-brand-emphasis` | ink (light) / lime (dark) | Theme-aware brand-tinted foreground text |
| `--brand-anthropic-orange-large` | `#d97757` | Brand-exception colour #3. Anthropic warm orange, UTH page only, 18px+ bold |
| `--brand-anthropic-orange-body` | `#b85033` | Darker Anthropic orange for 12-14px body text, UTH page only |

### When to reach for which token

Lime is the brand accent but it fails WCAG as foreground text on the off-white page background (`#d2ff37` on `#f5f5f5` is 1.30:1, far below the 4.5:1 floor). The "on" tokens and `--color-brand-emphasis` cover the cases the system actually needs. Pick by asking: **what is the surface, and what is the role of this colour on it?**

| Need | Reach for | Why |
|---|---|---|
| Lime background slab, identity surface | `--brand-lime` (background) | The accent surface itself. `--brand-lime` is for backgrounds, decorative bars, focus rings on dark surfaces, lime band underlines. Never use it as foreground text on light. |
| Text sitting on top of a known lime background | `--brand-on-lime` (foreground) | Resolves to ink. 14.42:1 contrast on lime. The pair `background: var(--brand-lime); color: var(--brand-on-lime);` is the canonical lime button or lime card. |
| Lime accent text on a known dark slab (`--brand-ink` background, hero gradient, testimonials, contact) | `--brand-on-ink` or `--brand-lime` | Both resolve to `--green-500`. Use `--brand-on-ink` when the relationship to the dark surface matters semantically; use `--brand-lime` when it's just "the accent on this dark thing". 14.42:1 on `--brand-ink`. |
| Brand-tinted foreground text that needs to stay readable on both light and dark page surfaces | `--color-brand-emphasis` (foreground) | Theme-aware. Resolves to `--neutral-850` (ink) in light mode, `--green-500` (lime) in dark mode. Use for eyebrow numbers, inline `<code>` spans, in-line link styling, accent words inside body copy. This is the right answer 90 percent of the time when you previously reached for `color: var(--brand-lime)`. |
| Decorative dot (the period in "nate mills.") | `--brand-lime` (foreground, 1-char) | Documented carveout. The dot is brand identity, 1-character decorative, and the hook's WCAG advisory does not block it. Limited to the `.dot` / `.uth-dot` selectors. |
| Decorative lime bar under an eyebrow label, or border-color on a chip | `--brand-lime` (border / pseudo background) | Borders and pseudo-element backgrounds are not foreground text. No contrast rule applies. |

**Rule of thumb.** `color: var(--brand-lime)` outside a known-dark scope is almost always wrong. If you find yourself writing it, ask whether `--color-brand-emphasis` is what you actually want.

**Functional accents use `--color-accent`, never raw lime on light.** Anything that signals an *active* or *selected* state, the active tab underline, the current nav item, a segmented-toggle pressed state, must use `--color-accent` (theme-aware: ink on light, lime on dark), with `--color-accent-foreground` for text or icons sitting on the accent fill. Raw `--brand-lime` is reserved for dark surfaces; on a light surface it is ~1.4:1 and fails WCAG, so it must never carry state on light. Purely decorative *visual* fills (a divider line behind a subgroup label, a scale bar) use a theme-aware neutral (`rgb(var(--uth-fg) / 0.3)`, `--color-border-strong`), not lime, for the same contrast reason. This is a functional rule, not aesthetic: the accent marks interaction, neutrals decorate. The Under-the-Hood colour card follows it: its per-group gallery/list toggle pressed state is `--color-accent` / `--color-accent-foreground`, and the subgroup divider line is a neutral.

**Worked example, the footer lime-on-lime bug.** `#site-footer` has `background: var(--brand-lime)` hardcoded in both themes (it is a brand identity surface, not theme-following). A prior session swapped the "Design Systems Consultant" inline span from `--brand-ink` to `--color-brand-emphasis` in the name of using more semantic tokens. In dark mode `--color-brand-emphasis` resolves to lime, producing lime-on-lime, invisible. The correct token is `--brand-on-lime` because the surface is always lime regardless of theme. The fix tells you the rule: **`--color-brand-emphasis` is for text on theme-following surfaces; "on" tokens are for text on fixed-colour surfaces.** If the background does not flip with the theme, the text token should not flip either.

**Brand-exception colour #3, Anthropic warm orange.** Promoted into the token system as `--brand-anthropic-orange-large` (`#d97757`, large display) and `--brand-anthropic-orange-body` (`#b85033`, body text). These are the third brand-exception colours alongside the lime pair; they are intentional brand mentions, a documented brand exception, restricted to inline Anthropic name mentions and the UTH page H1 divider. The orange measures 2.86:1 on `#f5f5f5`, failing WCAG AA-large (3:1) by a hair. Allowed only at 18 px+ bold per the exception. Defined in `tokens.css`. An automated WCAG check flags `.uth-accent` as an advisory; this is expected and intentional given the brand exception.

### Brand-exception colours, `.uth-accent`

The Anthropic warm-orange pair is the only chromatic colour in the system besides lime. It is a documented, intentional brand exception, and is restricted to the Under The Hood (UTH) page: inline Anthropic name mentions and the UTH page H1 divider. It is never used for general UI, links, or body accents elsewhere.

| Class | Token | Value | Use |
|---|---|---|---|
| `.uth-accent` | `--brand-anthropic-orange-large` | `#d97757` | Large display orange. 18px+ bold only. Inline Anthropic mentions and the UTH H1 divider. |
| `.uth-accent-text` | `--brand-anthropic-orange-body` | `#b85033` | Darker orange for 12-14px body text. The darker value lifts contrast at small sizes. |

`#d97757` measures 2.86:1 on `#f5f5f5`, just under WCAG AA-large (3:1), so it is allowed only at 18px+ bold per the documented brand exception. `#b85033` is the body-size companion. Both tokens are defined in `tokens.css`. The WCAG hook flags `.uth-accent` as an advisory: this is expected and intentional given the brand exception.

### Semantic state

Intentionally omitted (see primitives section above). The page has no success / warning / danger UI to consume them.

---

## 4. Typography

### Semantic type tokens (primary, going forward)

This is the lean type scale. **New components MUST consume these tokens.** Legacy `--size-*` and `--display-*` tokens (documented in the subsections below) are deprecated, still functional, and being migrated section-by-section using a strangler-fig pattern (new tokens added alongside, consumers migrated gradually, legacy removed once nothing consumes them).

<!-- TOKENS:type-semantic:start -->

| Token | Value | Line height | Used for |
|---|---|---|---|
| `--text-h1` | `clamp(34px, 5.8vw, 72px)` | 1.05 | Page-level section headings (every section h2), hero h1. |
| `--text-h2` | `clamp(22px, 4vw, 32px)` | 1.15 | Card titles, ledes, sub-headings inside section bodies. |
| `--text-body` | `16px` | 1.55 | Paragraphs, lists, default reading text, card body copy. |
| `--text-label` | `11px` | 1.4 | Uppercase mono labels, eyebrows, stat labels, badges. |
| `--text-caption` | `12px` | 1.5 | Tiny captions, footnotes, stat descriptions. |

<!-- TOKENS:type-semantic:end -->

Button sizes (3-tier):

<!-- TOKENS:type-btn:start -->

| Token | Value | Notes |
|---|---|---|
| `--btn-sm` | `32px` | Compact: dense cards, toolbars, filters. Clears the WCAG 2.5.8 AA 24px target minimum. |
| `--btn-md` | `44px` | Default. Most CTAs. Equals the base .btn height and meets the WCAG 2.5.5 AAA 44px touch target. |
| `--btn-lg` | `52px` | Hero CTAs and primary conversion actions. |

<!-- TOKENS:type-btn:end -->

**Two fonts only.** Sans (`--font-body`) is Inter, used for everything except labels and code. Mono (`--font-mono`) is JetBrains Mono, used for labels, eyebrows, code, and the rare stat-num where tabular alignment matters.

The `--font-mono-metric` alias is preserved as a legacy reference. It previously led with IBM Plex Mono (which produced a visible two-mono-font drift on the Bupa card). The font stack now falls through to JetBrains Mono. **New code should use `--font-mono` directly, not `--font-mono-metric`.**

**The migration rule.** Any new component MUST consume `--text-*` tokens for sizing. Any existing component being touched for a real change (not a one-line fix) should be migrated to consume `--text-*` tokens at the same time. Legacy tokens stay functional until all consumers have moved.

**Current consumers of semantic tokens** (post-full-migration):

| Semantic token | Replaces (legacy) | Consumer count | Coverage |
|---|---|---|---|
| `--text-body` | `--size-base` (16px) | 28 rules | sections.css, index.html, components.css |
| `--text-caption` | `--size-xs` (12px) | 33 rules | sections.css, index.html, components.css |
| `--text-label` | `--size-2xs` (11px) | 27 rules | sections.css, index.html, components.css |
| `--text-h1` | `--display-section` | `.section-title` (every section h2) | components.css + inline critical CSS |
| `--text-h2` (consumed via `--display-card-title`) | bespoke clamps | `.feat-card .section-title` (3 cards) | sections.css |
| Bupa card body via `.feat-top .section-subtitle` | `--size-lg` (18px) | 1 rule | sections.css |
| `--tracking-eyebrow` (0.18em) | hardcoded 0.08em / 0.1em | `.feat-badge`, `.feat-spec-label`, `.section-label` | sections.css |

**Migration result (post-full-grind audit):**
- 88+ legacy `--size-*` font-size refs migrated to semantic equivalents across all 3 CSS files
- Site-wide consistency confirmed via DOM probe across 15 sections: eyebrows identical (12 sections), section H2s identical (9 sections), section subtitles identical (10 sections), card H2s identical (3 sections), feat-spec triplet identical (3 cards)
- IBM Plex Mono backdoor killed via `--font-mono-metric` change (now JetBrains Mono only)
- `.feat-badge` tracking standardized to `--tracking-eyebrow` (was 0.08em outlier)

**Intentional exceptions** (do NOT migrate):
- About section lede inline `style="font-size: var(--display-lede)"`. Page intro emphasis, 20 to 24px responsive.
- Hero h1. Terminal-style aesthetic, light weight, own size mechanism.
- Metric stat-num uses `--display-stat-num`. Marquee scale (40 to 88px).
- `.metric-label` (14px title-case Inter) vs `.feat-spec-label` (11px uppercase mono). Different semantic tiers: callout label (impact section card chrome) vs data-table label (feat-card stat row).
- Testimonial half-pixel sizes (`.c-quote` 14.5px, `.c-name` 13.5px, `.c-role` 11.5px). Deliberate visual-fit one-offs scoped to one section.
- UTH design system demo samples showing literal sizes (`.uth-scale-aa` swatches). They SHOWCASE the type scale, must not be migrated.

**Legacy tokens kept as utility tokens** (no clean semantic mapping, retained for one-off needs):
- `--size-sm` (14px). Meta labels, button text, role-company.
- `--size-meta` (13px). Role-meta, footer fine print.
- `--size-lg` (18px). h3 elements in awards, UTH intro paragraph.
- `--size-xl` (24px). h3 elements in recent-work (role-title).
- `--size-2xl` (32px). UTH demo only.
- `--size-3xl` (48px). Constrained section heading tier (per the heading-size rule).

---

### Families (legacy reference, current state)

<!-- TOKENS:type-families:start -->

| Token | Stack | Role |
|---|---|---|
| `--font-display` | `"Inter", -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif` | Display headings (h1, h2, h3) and large numbers. |
| `--font-body` | `"Inter", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif` | Body copy, lists, and buttons. |
| `--font-mono` | `"JetBrains Mono", ui-monospace, "SF Mono", Menlo, Consolas, monospace` | Tabular numbers, code, and eyebrow labels. |
| `--font-serif` | `"PT Serif", Georgia, serif` | Editorial pull quotes, testimonials only. |

<!-- TOKENS:type-families:end -->

A FULL italic display heading is banned. Italic emphasis on a single word or short phrase inside a heading is allowed when paired with a muted colour token to mark that word as secondary emphasis (the "Builder.", "systems brain", "think" pattern used on the live page). The whole heading must never be italic. Heavy weight plus tight tracking carries display; italic is a punctuation accent for one emphasised word.

### Display sizes (hero + section + mid-tier)

| Token | Value | Used by |
|---|---|---|
| `--display-hero` | `clamp(40px, 9vw, 118px)` | Hero h1 |
| `--display-section` | `clamp(28px, 5.8vw, 72px)` | Section h2 |
| `--display-card-title` | `clamp(22px, 4vw, 44px)` | Card-level h2 inside featured projects (`.feat-card .section-title`). Steps down one tier from `--display-section` so card titles never compete with the page section heading above them. |
| `--display-stat-num` | `clamp(40px, 7vw, 88px)` | Large stat numbers (`#metrics .stat-num` general rule). Narrow-mobile MQ (<639px) still has its own `clamp(40px, 12vw, 64px) !important` override for the tighter card width. |
| `--display-lede` | `clamp(20px, 5vw, 24px)` | Page intro lede (e.g., About section's `<p class="section-subtitle">`). Use this token via inline `style="font-size: var(--display-lede);"` to avoid the inline-hardcoded-clamp anti-pattern below. |
| `--display-stat` | `clamp(96px, 12vw, 140px)` | **Misnamed.** Actual use: decorative testimonial quote glyphs (`.c-quote-mark`, `.f-quotemark`). Pending rename to `--display-quote-mark` in a future cleanup. |
| `--display-tight` | `-0.04em` | Display letter-spacing |
| `--display-weight` | `600` | Display weight (the bold tier of the bi-weight system, see Section 4) |

**Heading-size rule.** Heading sizes do not drift per section. Every
heading maps to one of three sizes:

| Tier | Token | Used by |
|---|---|---|
| Hero | `--display-hero` | The single page h1. |
| Section | `--display-section` | Every full-width section h2: about, metrics, experience, projects, skills, certifications, testimonials, FAQ, awards, education, contact, and the under-the-hood h2. |
| Constrained section | `--size-3xl` (48 px) | Section h2s that share a row with a gallery and must fit a half-width column: the Bupa case study and Token Exporter headings. |

Do not introduce a fourth `clamp()` value for a heading. If a section needs a
smaller heading, it uses the constrained tier (`--size-3xl`), not a bespoke
clamp. Sub-headings inside section bodies (h3) use the text scale
(`--size-base` / `--size-xl`), never a display token.

### Type scale (text)

<!-- TOKENS:type-scale:start -->

| Token | Size | Line height |
|---|---|---|
| `--size-xs` | `12px` | `1.45` |
| `--size-sm` | `14px` | `1.5` |
| `--size-base` | `16px` | `1.5` |
| `--size-lg` | `18px` | `1.45` |
| `--size-xl` | `24px` | `1.25` |
| `--size-2xl` | `32px` | `1.15` |
| `--size-3xl` | `48px` | `1.05` |

<!-- TOKENS:type-scale:end -->

### How clamp() tokens are documented

Many display tokens use `clamp(min, preferred, max)` to produce fluid type that scales between a floor (mobile) and a ceiling (large desktop). Document each clamp token with three things: the formula, the viewport widths where clamping binds, and the computed value at representative widths.

**The formula.** `clamp(MIN, PREFERRED, MAX)` resolves to:

- `MIN` whenever `PREFERRED` is below `MIN` (typically narrow viewports)
- `PREFERRED` whenever it sits between `MIN` and `MAX` (the fluid zone)
- `MAX` whenever `PREFERRED` is above `MAX` (typically wide viewports)

For a `vw`-based preferred term like `5.8vw`, the binding viewport widths are:

- `MIN ÷ 0.058` → below this width, MIN wins
- `MAX ÷ 0.058` → above this width, MAX wins
- Between those widths, the value scales smoothly with viewport.

So the token has two natural "breakpoints", but they are properties of the clamp itself, not authored media-query breakpoints.

**Documentation pattern.** For each clamped token, capture the formula plus the binding widths in the token table:

| Token | Formula | MIN binds below | MAX binds above | Used by |
|---|---|---|---|---|
| `--text-h1` | `clamp(34px, 5.8vw, 72px)` | 483 px | 1241 px | Section h2, hero h1 |

For tokens where binding behaviour matters to consumers (any heading or stat-num), additionally show the resolved value at three representative widths:

| Viewport | Preferred (5.8vw) | Resolved | Why |
|---|---|---|---|
| 375 px (mobile) | 21.75 px | **28 px** | Below MIN, floor wins |
| 600 px | 34.8 px | **34.8 px** | In fluid zone |
| 1024 px (tablet) | 59.4 px | **59.4 px** | In fluid zone |
| 1280 px (desktop) | 74.2 px | **72 px** | Above MAX, ceiling wins |
| 1920 px (wide) | 111.4 px | **72 px** | Above MAX, ceiling wins |

**Anti-pattern: per-breakpoint clamp overrides.** If you find yourself reaching for `@media` to override a clamp value at a specific width, either the floor or ceiling is wrong. Adjust the clamp arguments instead so the token continues to work as one continuous fluid value. Reserve `@media` for genuinely discrete behaviour (layout column changes, hiding elements, density swaps), not for nudging a font size at one breakpoint.

### Mobile type scale (lower bounds)

Display tokens and heading clamps follow a 1.25 ratio (major third) anchored at the 16 px body baseline. The lower bound of each clamp is the value the size lands on at the smallest realistic mobile viewport (about 375 px), where the `vw` middle term falls below the floor and the clamp's first arg wins.

| Tier | Mobile floor | Desktop ceiling | Implementation |
|---|---|---|---|
| Body | 16 px | 16 to 18 px | `var(--size-base)` static; `var(--size-lg)` for ledes |
| Lede (About section) | 20 px | 24 px | `var(--display-lede)` |
| Sub-tag (italic muted) | 16 px | 16 px | `var(--size-base)` |
| Section H3 (UTH doc) | 22 px | 56 px | `clamp(22px, 4.5vw, 56px)` |
| UTH subheading | 18 px | 32 px | `clamp(18px, 2.4vw, 32px)` |
| Section H2 | 28 px | 72 px | `--display-section` |
| Card title (`.feat-card .section-title`) | 22 px | 28 to 44 px | `var(--display-card-title)` (mobile MQ override drops to `clamp(22px, 5vw, 28px)` below 600 px) |
| Card spec-num | 22 px | 49 px | `clamp(22px, 3.9vw, 49px)` |
| Stat-num (impact, narrow) | 40 px | 64 px | `clamp(40px, 12vw, 64px) !important` |
| Stat-num (impact, general) | 40 px | 88 px | `var(--display-stat-num) !important` |
| Display H1 (hero) | 40 px | 118 px | `--display-hero` |

At 375 px viewport, the visible tier hierarchy reads: body 16, lede 20, subhead 18 to 22, H2 28, stat-num 40, display 40+. Each tier is visibly distinct from the next; nothing crowds the heading above it.

**Footer body line-height** dropped from 1.65 to 1.55 (WCAG AA minimum is 1.5; staying at 1.55 keeps a slight breath without the loose desktop feel). Mono code labels keep `line-height: 1.65` because mono needs looser leading for legibility.

### Anti-pattern: inline font-size overrides

Do not override `font-size` via inline `style` on a styled paragraph like `.section-subtitle`. Inline styles cannot be responsive without baking a `clamp()` into the inline value, which fragments the type scale across markup.

**Bad:** `<p class="section-subtitle" style="font-size: var(--size-xl);">` hard-codes 24 px on every viewport. Breaks the mobile scale; nothing inherits the change.

**Good:** `<p class="section-subtitle" style="font-size: var(--display-lede);">` consumes the mid-tier `--display-lede` token. Keeps the desktop emphasis, scales down on mobile, fully token-aligned. Future mobile tightening = one token edit, all consumers update.

If a paragraph needs a unique scale across many places, define a class for it in `components.css` and have it consume a display token. Component rules **consume** tokens; they never define their own clamp values. The mid-tier tokens (`--display-card-title`, `--display-stat-num`, `--display-lede`) exist precisely so component rules don't have to.

### Weights and tracking

Weight: five distinct weights, all loaded from Inter, `--weight-regular` **400**, `--weight-medium` **500**, `--weight-semibold` **600**, `--weight-bold` **700**, `--weight-extrabold` **800**. (`--display-weight` stays **600**: the display headings are deliberately semibold, not heavier, so this is separate from the body weight scale.) Restored 2026-06-02 from a former bi-weight (400/600) flattening, since Inter was already being loaded at all five weights.
Tracking: tight `-0.02em`, normal `0`, wide `0.02em`, mono `0.01em`.

Two component-level tracking tokens cover the uppercase label patterns so the values are not re-typed per rule:

- `--tracking-eyebrow` (`0.18em`), wide tracking for uppercase eyebrows and the `.section-label` style.
- `--tracking-label` (`0.08em`), tracking for small uppercase labels (role-card dates, card meta).

### Heading emphasis: never use alpha colours

When emphasising a word or phrase inside a heading (italic, weight contrast, colour shift), the emphasis colour must be a **solid** token, never an alpha-modified one.

**Why:** italic glyphs at tight tracking (especially the display weights, which use `-0.02em` to `-0.04em`) overlap at the letter joins. Where two semi-transparent glyphs overlap, alpha doubles and produces visible dark spots in the overlap zones. The same word renders cleanly with a solid colour because each glyph occludes the next instead of compounding.

**How to apply:**
- Use a solid semantic token. For muted emphasis prefer `var(--color-text-tertiary)` (resolves to `--neutral-600`, `#67676f`) or `var(--color-text-secondary)` (`--neutral-700`).
- For brand-coloured emphasis, use `var(--brand-lime)` or `var(--color-brand-emphasis)`, never `rgb(... / X)` with `X < 1`.
- For dark-mode handling, define the dark variant as another solid token under `[data-theme="dark"]`, not by adjusting alpha.

**Anti-pattern:** `color: rgb(var(--uth-fg) / 0.5)` on an italic display word. Renders fine in isolation; produces visible darkening at letter joins like `tt`, `rt`, `li`, `fi`.

Captured here so future emphasis treatments (UTH headings, future card variants) avoid this trap. Live example: `#under-the-hood-embedded .uth-heading-glitch` in `assets/sections.css`.

---

## 5. Spacing

Doubling rhythm from 4 to 256 px, with `--space-3 (12px)` and `--space-5 (24px)` added for medium-tight breaks.

<!-- TOKENS:spacing:start -->

**Spacing scale**

| Token | Value | Description |
|---|---|---|
| `--space-1` | `4px` | Hairline gap. Icon-to-label, tight inline spacing. |
| `--space-2` | `8px` | Tight gap. Chip padding, small stacks. |
| `--space-3` | `12px` | Medium-tight break (added between 2 and 4). Heading-to-body, compact rows. |
| `--space-4` | `16px` | Base unit. Default gap between related elements and standard card padding. |
| `--space-5` | `24px` | Medium break (added between 4 and 6). Group separation inside a section. |
| `--space-6` | `32px` | Large gap. Between subsections and card to card. |
| `--space-7` | `48px` | Block spacing between stacked content blocks. |
| `--space-8` | `64px` | Major block separation and section inner padding. |
| `--space-9` | `96px` | Section rhythm. The lower bound of vertical section padding (--section-padding). |
| `--space-10` | `128px` | Section rhythm. The upper bound of vertical section padding (--section-padding). |
| `--space-11` | `192px` | Outsized spacing for full-bleed editorial breaks. |
| `--space-12` | `256px` | Largest step. Rare, marquee-scale vertical space. |

<!-- TOKENS:spacing:end -->

Never use raw px in components. The whole point is one place to edit the rhythm.

---

## 6. Radii, borders, shadows

<!-- TOKENS:radii-borders-shadows:start -->

**Radii**

| Token | Value | Description |
|---|---|---|
| `--radius-none` | `0` | Square. No rounding, for sharp-cornered surfaces and full-bleed media. |
| `--radius-sm` | `8px` | Small radius. The workhorse for inputs, chips, and small controls. |
| `--radius-md` | `10px` | Medium radius. Mid-size controls and insets, a touch rounder than sm. |
| `--radius-lg` | `14px` | Large radius. The default for cards and modals. |
| `--radius-xl` | `20px` | Extra-large radius. Prominent panels and feature surfaces. |
| `--radius-full` | `999px` | Full round. Pills, tags, and circular buttons; forces a complete radius at any height. |

**Borders**

| Token | Value | Description |
|---|---|---|
| `--border-hairline` | `1px solid var(--color-border)` | Default 1px hairline border; reads --color-border so it follows the theme. The standard card edge and divider. |
| `--border-strong` | `1px solid var(--color-border-strong)` | Heavier 1px border; reads --color-border-strong. For edges that need to read past a hairline, such as secondary-button outlines. |
| `--border-focus` | `2px solid var(--color-focus-ring)` | 2px focus outline; reads --color-focus-ring (ink on light, lime on dark). The keyboard-focus indicator, never removed without a replacement. |
| `--focus-ring-offset` | `2px` | Offset between an element and its focus ring. Outsets the 2px ring so it clears the element edge. |

**Shadows**

| Token | Value | Description |
|---|---|---|
| `--shadow-none` | `none` | No shadow. The default; the system favours borders over shadows. |
| `--shadow-soft` | `0 1px 2px rgb(var(--brand-ink-rgb) / 0.04), 0 1px 3px rgb(var(--brand-ink-rgb) / 0.06)` | Subtle resting elevation, two stacked ink-alpha layers, for cards that lift just off the page. Dark mode swaps to deeper black-alpha. |
| `--shadow-lift` | `0 4px 12px rgb(var(--brand-ink-rgb) / 0.06), 0 2px 4px rgb(var(--brand-ink-rgb) / 0.04)` | Stronger elevation for overlays and float-on-scroll chrome only, not resting cards. |
| `--shadow-modal` | `0 24px 64px rgba(0, 0, 0, 0.5), 0 8px 16px rgba(0, 0, 0, 0.18)` | Modal and lightbox elevation. The deepest shadow, for surfaces floating above a scrim. |
| `--accent-period-shadow` | `0 1px 2px rgba(0,0,0,0.42), 0 0 0 1px rgba(0,0,0,0.18)` | Depth under the lime period in section titles. Keeps the lime dot legible on light surfaces; resolves to none in dark, where lime already reads. |
| `--accent-dot-shadow` | `0 1px 3px rgba(0,0,0,0.24)` | Depth under the active carousel pagination dot. Keeps the lime dot legible on light surfaces; resolves to none in dark. |

<!-- TOKENS:radii-borders-shadows:end -->

Swiss-minimal favours borders over shadows. Use `--shadow-lift` only on overlays and float-on-scroll chrome.

Two accent-shadow tokens keep the lime accents legible on light backgrounds, and resolve to `none` in dark mode where lime already reads cleanly:

- `--accent-period-shadow`, `text-shadow` on the lime `.section-title .dot` period.
- `--accent-dot-shadow`, `box-shadow` on the active carousel pagination dot (`.splide__pagination__page.is-active` / `.full-dots button[aria-current="true"]` `::before`).

---

## 7. Motion

```
--duration-fast     150 ms     (hover, focus, micro state)
--duration-base     220 ms     (reveal, modal, swap)
--duration-slow     400 ms     (context shift, slide)
--duration-counter  1400 ms    (count-up animations)

--ease-default      cubic-bezier(0.4, 0, 0.2, 1)
--ease-entrance     cubic-bezier(0, 0, 0.2, 1)
--ease-exit         cubic-bezier(0.4, 0, 1, 1)
```

Every animation must respect `prefers-reduced-motion`. The reduced-motion override at the bottom of `tokens.css` collapses every duration to 1 ms and disables transforms.

---

## 8. Layout

```
--container-base   960 px     (prose, single-column sections)
--container-wide   1200 px    (galleries, marquees, grids)

--bp-mobile   375 px
--bp-tablet   768 px
--bp-desktop  1024 px
--bp-wide     1440 px
```

Sections are full-bleed at the outer level (`width: 100vw`, `margin-inline: calc(50% - 50vw)`). Content centres in one of the two container widths so every section's left gutter aligns at 120 px on a 1440 px viewport.

**Responsive value tables (Under-the-Hood).** Token reference tables and the colour list are wrapped in `.uth-table-scroll` and never drop a column at a breakpoint. On desktop, a section with several sub-palettes either pairs them two-up (when their content is narrow, e.g. the lime and neutral primitive ramps) or renders the whole section as one table with the sub-palettes as header rows, so every column lines up straight down across subsections. The rule: scroll or wrap, never hide a column.

**Mobile density rule.** Below ~640px, dense value tables tighten so the most fits without dropping a column: the swatch/visual shrinks to a compact square, the outer and per-column padding step down to the smallest space tokens, and label text holds at the **11px floor** (`--text-label` / `--size-2xs`, the smallest in the scale). Never go below 11px, and never `clamp()` these small labels (clamp is for display text; tiny labels are already at the floor). All value columns in a table share one size, so the hierarchy reads from colour, not size.

---

## 9. Components (extracted into its own file)

Each component lives in `components.css`, reads semantic tokens only, has documented variants.

| Component | Variants | Documented in |
|---|---|---|
| Button | primary, secondary, icon, pill | components.css |
| Card | default, dark, accent (lime) | components.css |
| Chip | ink, lime, neutral | components.css |
| Avatar | round, square, with-ring | components.css |
| Eyebrow | label, label + lime bar | components.css |
| SectionHead | label + title + subtitle triplet | components.css |
| Stat | metric + unit + caption | components.css |
| RoleCard | timeline entry with logo, dates, bullets | components.css |
| TestimonialCard | quote, author, role, company logo | components.css |
| FAQRow | native `<details>` based | components.css |
| Marquee | A+A duplicate-set infinite scroll | components.css |
| FeatCard (editorial) | image-bottom (default), image-top, 1 / 2 / 3 image strip | `assets/sections.css` (`.feat-card`), specimen at `docs/mockups/feat-editorial-card.html` |
| Header nav | shared by main site + design-system view; states: unselected / selected / active | `assets/sections.css` (`#site-nav a, #site-header .uth-nav a`) |

**Header navigation (shared component).** The portfolio header menu and the design-system ("under the hood") header menu are ONE shared style: a single grouped rule `#site-nav a, #site-header .uth-nav a` in `assets/sections.css`. Only the link labels differ (About / Projects / ... vs Colour / Brand / Type / ...). Do not restyle one menu in isolation, edit the shared rule so both stay identical. Link states: unselected = `--color-text-tertiary` (lighter, still AA at 5.4:1 light / 5.7:1 dark), selected and `.is-active` = `--color-text-primary` (ink) with a 1px animated `::after` underline. The underline is ink in light mode and `--brand-lime` in dark (lime on the near-white light header is ~1.1:1, so it stays ink there). State reads from the underline shape plus colour, not colour alone (passes WCAG 1.4.1). The inline menu only renders at wide desktop; narrower widths use the hamburger overlay.

**FeatCard editorial pattern.** The featured-project card with content on the left (eyebrow row, heading, subtitle) and an image strip that can sit at the top or bottom of the card. Used by Bupa, Token Exporter, and the design-system featured-project sections. The image-top variant flips the CSS grid template areas. Image count is flexible (1, 2, or 3 images in the 3-column strip). Live specimen with both position variants at `docs/mockups/feat-editorial-card.html`. The image-position toggle and image-count toggle are documented patterns, not currently wired as runtime controls; flip via class modifier or override `grid-template-areas` on the section.

#### Canonical `.feat-card` markup pattern (until `<feat-card>` web component lands)

The 3 featured-project cards (#bupa, #token-exporter, #design-system-stats) are currently hand-coded HTML that share the `.feat-card` class. Component-level CSS works, but the MARKUP is duplicated and can drift (it did in May 2026; Token Exporter accumulated an empty `.feat-heading-row` wrapper after a logo was removed, throwing its heading spacing 12px off the other two).

Until the `<feat-card>` web component is built (a future enhancement), every `.feat-card` instance MUST match the canonical structure exactly:

```html
<section id="..." aria-labelledby="...-heading" class="container-wide" style="...padding...">
  <div class="feat-card" data-reveal data-theme="light">

    <div class="feat-cta-corner">
      <a href="..." class="btn btn--primary" target="_blank" rel="noopener noreferrer" aria-label="...">
        <i data-lucide="..." aria-hidden="true"></i>
        Read the case study
        <i data-lucide="external-link" aria-hidden="true"></i>
      </a>
    </div>

    <div class="feat-top">
      <!-- eyebrow + badge + title + subtitle -->
      <div>
        <div class="feat-eyebrow-row">
          <span class="feat-badge">
            <img src="..." alt="" aria-hidden="true" width="60" height="60" loading="lazy" decoding="async">
            Bupa case study
          </span>
        </div>
        <h2 id="...-heading" class="section-title" style="margin-top: var(--space-3);">Heading<span class="dot">.</span></h2>
        <p class="section-subtitle" style="margin-top: var(--space-3);">
          Body copy paragraph...
        </p>
      </div>
    </div>

    <!-- 4 stat cells, content-hugging -->
    <div class="feat-specs" aria-label="...">
      <div class="feat-spec">
        <p class="feat-spec-num">74<span class="feat-spec-unit">%</span></p>
        <p class="feat-spec-label">Token reduction</p>
        <p class="feat-spec-desc">Description hidden on mobile.</p>
      </div>
      <!-- 3 more .feat-spec ... -->
    </div>

    <!-- Image strip, 3 imgs. The one with class="mobile-show" is the single image shown on mobile (<=600px). -->
    <div class="feat-strip" aria-label="...">
      <img src="..." alt="..." loading="lazy" width="..." height="..." decoding="async" class="mobile-show">
      <img src="..." alt="..." loading="lazy" width="..." height="..." decoding="async">
      <img src="..." alt="..." loading="lazy" width="..." height="..." decoding="async">
    </div>

  </div>
</section>
```

**Safe-edit checklist.** When touching any `.feat-card`, before committing:
1. Open the OTHER 2 cards side by side. Confirm they share the same structural elements in the same order.
2. The `<h2 class="section-title">` MUST have `style="margin-top: var(--space-3);"` inline. NOT inside a `.feat-heading-row` wrapper (that wrapper only existed for the now-removed Token Exporter logo).
3. The `<p class="section-subtitle">` MUST have `style="margin-top: var(--space-3);"` inline.
4. The `<div class="feat-eyebrow-row">` MUST contain ONLY the `.feat-badge` span (no `<p class="section-label">` eyebrow inside the card; that was removed in May 2026 since the section header already provides the eyebrow context).
5. The image strip MUST have exactly ONE image with `class="mobile-show"` (the one shown when mobile collapses to 1 column). The other 2 are desktop-only.
6. Stat count per card MUST be 4 (drives the 2x2 grid on mobile).
7. Inline styles on the section, .feat-card, and individual elements (margin-top, padding-top, etc.) MUST match across all 3 cards unless a section has a genuine reason to differ.

**Future migration path.** When time allows, build `<feat-card>` as a vanilla JS custom element (no framework, no build step). The element takes content via `data-slot` attributes and renders the canonical structure. Drift becomes structurally impossible. Effort estimate ~2 hours including: light DOM custom element, slot system, carousel-clone compatibility, doc update, full verification across all 3 cards in both source sections AND the top-picks carousel clones.

**Card variants.** `.card` is the light-surface base (off-white bg,
hairline border, soft radius). `.card--dark` is the dark-surface modifier for
dark slabs: it swaps the surface to `--brand-ink`, the text to
`--color-on-ink-primary`, and the border colour to `--color-on-ink-border`,
while inheriting the 1px border style and radius from `.card`. Compose it as
`class="card card--dark ..."`. The testimonials compact cards (`.c-card`) are
built this way. Note the full-view testimonial slide (`.f-card`) is a
deliberately separate component, not a `.card`: it is a 2-column portrait
carousel slide with a 20px radius, no border, and overflow hidden, so composing
it onto the card base would change its appearance.

Adding a new component:
1. Define the class in `components.css`.
2. Only read semantic tokens.
3. Document variants in this file.
4. Add a live sample to the under-the-hood Components section.

### Button behaviour (variants, mobile, icons, backgrounds)

**Variants.**

| Variant | Background | Text | Border | Use on |
|---|---|---|---|---|
| `.btn--primary` | `--brand-lime` | `--brand-ink` | `--brand-lime` | `--color-bg` (off-white) surfaces |
| `.btn--secondary` | transparent | `--color-text-primary` | `--color-border-strong` | `--brand-lime` surfaces (footer, lime slabs) |
| `.btn--white` | `--color-static-white` (theme-invariant) | `--brand-ink` | white | Fixed-dark brand slabs (Bupa case study) |
| `.btn--icon` | transparent | `--color-text-secondary` | `--color-border` | Chrome (header toggles, controls) |

**Background pairing rule.** Lime-on-lime is forbidden. `.btn--primary` MUST NOT sit on a `--brand-lime` background (e.g. the footer). Use `.btn--secondary` instead so the ink text + border carry contrast.

**Mobile width rule (`<=768px`).** Section-level primary CTAs (footer "Get in touch", contact "Email me", featured-card "Read the case study", featured-card "View on Figma") expand to `width: 100%` and `justify-content: center`. Inline buttons inside paragraphs stay auto-width. Rationale: thumb-friendly tap area, no "tiny button in a sea of whitespace" on phones. Implemented via:

```css
@media (max-width: 768px) {
  .feat-cta-corner .btn,
  .contact-cta .btn,
  .footer-actions .btn {
    width: 100%;
    justify-content: center;
  }
}
```

**Icon conventions.** Pair each button with the icon that matches its action type:

| Icon (Lucide) | Use for |
|---|---|
| `mail` (envelope) | `mailto:` links ("Email me", "Get in touch") |
| `external-link` (box with arrow) | Outbound `https://` links ("Read the case study", "View on Figma") |
| `arrow-up-right` (diagonal arrow) | Reserved. Not used in production buttons; was historical placeholder |
| `download` | File download actions ("Download resume") |
| no icon | Same-page anchors |

`arrow-up-right` is NOT a substitute for `external-link`. They look similar but mean different things to screen-reader users and design-system consumers.

**Icon placement.** Trailing, after the label (label-left, icon-right): "Get in touch" then the `mail` icon. Applies to all primary action buttons (hero, footer, drawer) so the CTA shape stays consistent across the site.

### Shape rationale (badges, buttons, circles, square icons)

The portfolio uses five distinct shapes. Each one carries meaning. Mixing them without a rule creates the "too many shapes, what is the logic?" feeling. The logic is: shape equals role.

| Shape | Token | Use for | Examples |
|---|---|---|---|
| **Pill (full radius)** | `--radius-pill` (999px) | Identity tags, taxonomic labels, status indicators | "Available for work" status pill, `.feat-badge` ("Bupa case study", "Figma plugin"), `.bupa-tags`, role chips |
| **Rounded rectangle** | `--radius-soft` (~14px) | Action buttons and content containers | All `.btn` variants ("Get in touch", "Read the case study"), `.card`, modals, slabs |
| **Sharp tag (small radius)** | 4px | Inline emphasis inside running prose | `.faq-stat` chips (`74%`, `18 hours/week`), `<code>` references |
| **Circle (full circle)** | `border-radius: 50%` | Identity surfaces (people, brands) and personal/social affordances | Avatar in mobile drawer, GitHub social icon, LinkedIn social icon, brand logos in cards |
| **Square with radius** | `--radius-soft` | Icon-only utility buttons in chrome | Theme toggle, Download PDF, Mobile hamburger, Close-modal X |

**The rule (single source of truth).**

1. **Shape signals role.** Pill is identity. Rounded rect is action. Sharp is inline data. Circle is person or brand. Square is chrome utility.
2. **Never mix metaphors.** A status pill is never a button. A social media icon is never a square. An icon-only utility button is never a pill.
3. **Width carries the action emphasis, not shape.** A full-width button on mobile and an auto-width button on desktop are the same shape (rounded rect); only the layout changes.
4. **One pill style across the whole portfolio.** All pills share the same border, padding, and typography (mono 11px, 0.08em tracking, uppercase). Variants only differ in colour treatment (lime-tinted vs neutral).
5. **Circles are reserved for identity.** Don't reach for a circle just because it looks softer. If it is not a person, brand, or social/identity affordance, it is a different shape.

**Worked examples (avoid this confusion).**

| Element | Wrong shape | Correct shape | Why |
|---|---|---|---|
| "Get in touch" CTA | Pill | Rounded rect | It is an action, not an identity tag |
| GitHub social icon | Square with radius | Circle | It is a social/identity affordance |
| Theme toggle | Circle | Square with radius | It is a chrome utility, not identity |
| "Featured project" eyebrow | Rounded rect | Pill | It is a taxonomic label |
| Stat callout in FAQ prose (`74%`) | Pill | Sharp tag (4px) | Inline emphasis, not a free-standing label |

**Hero status row example.** The hero's "Available for work" group sits at the bottom of the hero. The correct shape composition is:

- **Status pill** (`pill` shape, lime-tinted with pulse dot): identity, "I am available"
- **Social icons row** (`circle` shape, GitHub + LinkedIn + Substack): social/identity affordances
- **"Get in touch" CTA** (`rounded rect` shape, primary action button): action

Three shapes, three roles, no mixing. The pill and the icons sit on the left; the action button sits on the right. All three share vertical alignment (centred) and a consistent vertical rhythm with the hero's status row baseline.

### Mobile nav overlay (full-screen drawer)

The hamburger menu (`.menu-overlay-a` / `#mobile-nav-drawer`) is one global component, shared by the portfolio header (7 sections) and the under-the-hood design-system header (10 sections). It is active below 1080px, so every phone and iPad-portrait width renders it. Any change to the overlay touches both views, so design for a variable item count.

1. **Fills the viewport height, no scroll.** The list grows to fill the space between the header clearance and the footer, so items become even bands: 7 items breathe, 10 items tighten, neither scrolls. `overflow-y: auto` stays on the drawer as a safety net for short and landscape heights where the bands would otherwise clip; it is not the normal state.
2. **Fluid type, capped.** Number, label, and arrow use `clamp()` so they grow a little on wider screens and stop. The bands fill the space, not the type; the type stays tasteful and never balloons.
3. **Rows are full-bleed.** Each row pulls out to the drawer edges (`margin-inline: -22px; padding-inline: 22px`), so the divider and the hover/active wash run edge to edge while the text stays inset. Do not inset the divider to match the text.
4. **The CTA hugs its label.** "Get in touch" is `flex: 0 0 auto`, not stretched edge to edge. Social icons sit to its left; the footer row does not fill the full width on tablet.
5. **No in-drawer Back.** Returning to the portfolio from the design-system view is handled by the site header's back arrow, which stays visible above the open drawer. Do not add a second Back control inside the drawer; it duplicates the header and reads as a stray nav item.
6. **On-ink colours only.** The drawer is always ink, even when the page is in light mode. Style its controls with explicit on-ink values (as the social icons do), not theme tokens like `--color-text-primary`, which would lose contrast on the ink surface.
7. **Hover and current section share one lime treatment.** A faint full-bleed lime wash (`rgb(var(--brand-lime-rgb) / 0.05)`) plus a lime label marks both the hovered or focused row and the current section. This is global: every drawer item binds `:aria-current` to `activeSection`, and the scroll-spy watches the portfolio and the `uth-*` section ids alike, so both menus light up the same way.

---

## 10. Accessibility

- WCAG 2.2 AA contrast minimum for every text token. Verified in the comments inside `tokens.css` for every semantic colour.
- WCAG 2.2 is also published as the international standard ISO/IEC 40500:2025. Any AA claim here is a self-assessment, not a third-party certification; a formal conformance claim carries a short statement (date, guidelines version and URI, level, scope of pages, technologies relied upon). Adopting OKLCH does not change any of this: contrast is a property of the resolved colour, so an `oklch()` value has the same WCAG ratio as the identical hex, and every checker (axe, Pa11y, DevTools) evaluates the computed value.
- Focus ring is the brand `--color-focus-ring` (ink on light, off-white on dark, 2 px). Never removed without replacement.
- Touch target minimum 44×44 CSS px (`--touch-target-min`).
- Every animation gated behind `prefers-reduced-motion`.
- Semantic HTML first: `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<details>`, `<dialog>`.
- ARIA only where semantic HTML can't carry the meaning.
- Lime on light backgrounds is forbidden as foreground text. `--brand-lime` on `--color-bg` (`#d2ff37` on `#f5f5f5`) is 1.6:1, decorative use only. Lime as foreground only on `--brand-ink` (14.42:1).
- **Never dim accessible text with `opacity`** (or low-alpha ink) to make it read as secondary. Opacity multiplies against whatever sits behind the element and silently drops a passing colour below 4.5:1; the token looks correct in source but fails on screen. Choose a lighter text token that itself clears 4.5:1 instead. (2026-06-01: this trap caused most of an axe-core contrast sweep, `.pol-num` dimmed to `.55`, `.about-muted-list` ink at `0.5`, and the Featured carousel fading non-active cards to `0.4`.)
- **Every `<img>` declares `width` and `height` attributes.** Prevents Cumulative Layout Shift (CLS). Content jumping as images load disorients screen-reader users tracking position, magnifier users following focus, and users with cognitive or vestibular conditions. Dimensions should be the image's natural pixel size; CSS handles responsive scaling on top. SVGs included. Decorative spacer images may use `width="0" height="0"`. Enforced by an automated build check.

---

## 11. File map

```
docs/
  design-system.md          THIS FILE, the single brand + system spec

tokens.css                  Token implementation (primitives + semantics)
components.css              Component layer (extracted into its own file)
print.css                   Print stylesheet, condensed CV format

index.html                  Live portfolio; links external tokens.css + components.css
```

`index.html` links the external `tokens.css` and `components.css`, symlinked from the `design-system/` folder. `tokens.css` is generated from `tokens.json` and is the single source of truth. The former inline token mirror has been removed; there is no longer an inline copy to keep in sync.

---

## 12. Contribution rules

1. **Never write raw hex outside `tokens.css`.** If you need a colour, define a primitive (if it's a new value) or use an existing semantic.
2. **Brand tokens are aliases, not duplicates.** `--brand-lime: var(--green-500);` not `--brand-lime: #d2ff37;`.
3. **Components read semantics only.** Never `var(--green-500)` in a component class; use `var(--color-accent)` or `var(--brand-lime)`.
4. **Test in light and dark.** Every semantic has both. Toggle the page theme before shipping.
    - **Never hardcode `data-theme="light"` on a component.** It pins that element to light regardless of the site theme, and it propagates when the element is cloned (this is what kept the featured cards white in dark mode). Let components follow the page theme; a surface that must stay one colour uses fixed `--brand-*` or "on" tokens, not a pinned `data-theme`.
5. **WCAG 2.2 AA, every text colour.** If you add a new semantic, check the ratio against every surface it could land on.
6. **Reduce motion respect.** Every animation gets a `@media (prefers-reduced-motion: reduce)` collapse.
7. **One container width per section.** `--container-base` (960) for prose, `--container-wide` (1200) for grids. No middle ground.
8. **Section-label + section-title + section-subtitle triplet** is the only heading pattern. Every section uses it.
9. **No FULL italic display headings.** Italic emphasis on a single word inside a heading is allowed (the "Builder.", "systems brain", "think" pattern). Never set the whole heading italic. Heavy weight plus tight tracking carries display.
10. **Document the decision.** Document every non-obvious choice with the rejected option and the reasoning.
11. **Viewport scoping is explicit, never implicit.** Before writing any CSS, identify which viewport(s) the change targets. A property at the BASE rule applies to ALL viewports (mobile + tablet + desktop). Wrap viewport-specific overrides in `@media` blocks. Never put a "mobile fix" at the base rule expecting it to only affect mobile.
    - Mobile only: `@media (max-width: 639px) { ... }`
    - Tablet + desktop (default): base rule, no media query
    - Desktop only: `@media (min-width: 1024px) { ... }`
    - Tablet only: `@media (min-width: 640px) and (max-width: 1023px) { ... }`
    - When overriding a base property at a viewport, comment WHY in the override block so future edits don't blindly modify the base.
12. **Verify at three viewports after every CSS change.** Screenshot or read `getComputedStyle` at 1440px, 768px, AND 390px. A change that fixes mobile but breaks desktop is a regression. Never claim a task complete with only one viewport checked.

---

## 13. Writing voice, tone, and copy patterns

The portfolio uses two registers. Mixing them reads as inconsistent. Pick the right register before writing.

### Voice A, body copy (Craftsman)

Confident, evidence-led, quietly warm. Operator-class.

- **Use in**: hero subhead, About, section subtitles, FAQ leads, case study ledes, role summaries, footer body.
- **Sentence length**: 6 to 14 words ideal. Two clauses max.
- **Pronouns**: first-person ("I"). No royal "we".
- **Proof carries the brag**: "18 hours back to the team" not "huge productivity gains". Numbers do the work adjectives can't.
- **Warmth from honesty, not enthusiasm**: "Most systems don't die at launch. They fall apart later, when nobody's looking." That line is the voice. Operator who knows the shape of the problem.
- **Contractions**: yes. "I'll", "won't", "that's", "I'm".
- **No hedges**: "I believe", "I think", "arguably". Cut.

### Voice B, CTAs and microcopy (Confident)

Verb-first. Outcome-specific. Three to five words. No politeness padding.

- **Use in**: buttons, status pills, error messages, empty states, loading states, link text.
- **Length**: 1 to 5 words on buttons. Up to 12 in error or empty states.
- **Verbs**: "Read", "Get in touch", "View", "Start a conversation". Never "Submit", "Click here", "Learn more".
- **Errors**: name the problem, name the workaround. No apology preamble.
- **Empty states**: name what is missing, name what to do.
- **Status pills**: declarative present tense ("Available for work"), never aspirational ("Open to chat", "Always available").

### Voice C, system docs (Engineering register)

This file and its peers. Deliberately drier than the site.

- Statements of fact in present tense. "The base accent is ink, not blue."
- Confident without bragging. Decisions are explained, not defended. "This is by design." "One edit, full propagation."
- Mostly third-person system-speak ("the system", "the page", "a consumer"). "You" only in CTAs.
- Use in: this file, `tokens.css` comments, component class docblocks, contribution rules, commit messages, internal READMEs, handoff docs.

### Word list

| Use | Avoid |
|---|---|
| `system`, `token`, `governance`, `pipeline`, `foundation` | `passionate`, `world-class`, `cutting-edge`, `transformative`, `seamless` |
| `ship`, `scale`, `adoption`, `contribution` | `amazing`, `incredible`, `excited` |
| `multi-brand`, `cross-platform`, `token-driven` | `we believe`, `we think`, `arguably` |
| `the hard part` (LinkedIn signature) | `UI Wiz`, `pixel pusher` (in body copy) |
| `specialise` (British/Australian) | `specialize` (American) |
| `let's talk`, `get in touch`, `start a conversation` | `click here`, `learn more`, `submit` |

### Copy patterns

**CTA buttons**: verb plus outcome.
- Yes: "Read the case study", "View on Figma"
- No: "Click to learn more", "Submit"

**Section subtitle**: one sentence, sets the stake, 18 words or fewer.
- Yes: "Position papers on the calls that matter, tied to the work that proves them." (FAQ, benchmark)
- No: "Twenty years of work, four numbers that prove it." (defensive)

**Error message**: what plus workaround, no "sorry".
- Yes: "Send failed. Email mail@natemills.me, I'll see it faster anyway."
- No: "Oops! Something went wrong. Please try again."

**Empty state**: what is missing, what to do.
- Yes: "Nothing here yet. Case studies live below."
- No: "No results found."

**Loading state**: set expectation if over 1s, otherwise no copy.
- Yes: "Building the showreel..."
- No: "Loading..." with no context

### Positioning hierarchy (every touchpoint follows this shape)

1. Anchor role: Senior UI Designer
2. Specialty: design systems, governance, accessibility, automation
3. Range: 20 years, five disciplines, three industries
4. Proof: numbers ($4M+ revenue, 18h per week, 74% token reduction)

Same hierarchy on LinkedIn, portfolio, resume, email signature. Same shape, different lengths.

### Honest pitch (memorise this)

> Five disciplines. Three industries. Two decades.
> One obsession: making good design easy to ship at scale.

### What to avoid in all three registers

- Generic marketing superlatives ("world-class", "cutting-edge", "transformative"). Numbers do the bragging.
- Title Case headings, anywhere. Sentence case throughout.
- Italicised display headings (banned by Section 4).
- Em dashes in body copy (per `docs/content.md`).
- "Passionate". Appears in every junior portfolio in Australia.
- "We" when "I" is honest.

---

## 14. What this system is NOT

- It is not DaisyUI. No external component library. The custom build is the portfolio thesis.
- It is not Tailwind-driven. Tailwind is loaded as a utility convenience for one-off layout adjustments, not the system itself.
- It is not a runtime CSS-in-JS solution. Plain CSS custom properties only. The whole thing loads in a single network round trip.
- It is not theme-able beyond light and dark. Bupa case study has scoped overrides for blue; that's the only third theme and it's section-scoped, not global.

If you want to fork this for another brand, change `--green-500` and every consumer follows. That is the system working as designed.

---

## 15. Guardrails, recurring mistakes

Mistakes that have surfaced in past mockups and edits. Check against these before shipping. Consolidated here from the retired `brand-tokens.md`.

- **No blue outside the Bupa case study.** `#0079c8` (Bupa blue) is scoped to `#bupa` only. The base accent is ink. Never set `--color-accent` to blue for general UI.
- **Inter only.** Not Geist, not a substitute. Inter for display and body, PT Serif for editorial pull quotes only, JetBrains Mono for tabular numbers and labels.
- **No FULL italic display headings.** Italic emphasis on a single word or short phrase inside a display heading IS allowed (the muted-em pattern). Never apply `font-style: italic` to the WHOLE hero h1, section h2, or footer headline.
- **Surfaces are off-white or near-black only.** `--color-bg` is `#f5f5f5` (light) or `#0a0a0b` (dark). No cream, khaki, or tinted "warm" backgrounds.
- **Lime is never foreground text on a light surface.** Decorative bars, the `.dot` period, and dark-slab accents only. See section 3 for the token to reach for instead.
- **No raw values in components.** Every colour, space, radius, and duration resolves to a token. A hardcoded hex or px in a component class is a bug.

---

## 16. Naming conventions and benchmarks

One rule: **match the naming style to the scale's nature.** A small fixed set reads best as words; a large or growing ramp stays flexible as numbers; anything role-based is named by intent. Benchmarked against EightShapes (Nathan Curtis), the W3C DTCG format, Tailwind, Material 3, Adobe Spectrum, and Shopify Polaris.

| Scale | Convention | Decision, why, what we rejected |
|---|---|---|
| Radius | T-shirt: `none / sm / md / lg / xl / full` | Fixed set of about 6. Words over numbers because you never insert between radii. Rejected the old `soft` / `card` / `large` mix for putting feel, size, and component names on one axis. Old names kept as deprecated aliases during migration. |
| Spacing | Ordinal on a 4px base: `--space-1..12` | Kept readable ordinals. A hundreds scale (`100` / `200`, so a `150` slots between) is more future-proof, but this system is small and stable, so it is not worth renaming 12 tokens and their consumers. Rejected T-shirt: too few names for a 12-step ramp. |
| Colour primitives | Numeric stops: `neutral-0..950`, `green-50..950` | Hundreds so the ramp stays insertable (a `250` drops in without renaming). The future-proof convention; spacing deliberately trades it for readability. |
| Semantic colour and type | Intent: `--color-text-primary`, `--text-h1` | Named by role, so a re-skin changes the value, not the name. Order reads object, then property, then variant (DTCG / EightShapes). |

**Naming order:** general to specific, `object-property-variant`. Example: `color-feedback-background-error`, not `error-bg-color`.

**Red flags this system rejects:** mixed styles on one axis (the radius bug we fixed); property-first names; a component reading a primitive directly; brand lime as body text on a light surface.

**Sources:** [EightShapes, Naming Tokens in Design Systems](https://medium.com/eightshapes-llc/naming-tokens-in-design-systems-9e86c7444676), [W3C DTCG format](https://www.designtokens.org/TR/drafts/format/), [Material 3 corner radius scale](https://m3.material.io/styles/shape/corner-radius-scale), [Adobe Spectrum design tokens](https://spectrum.adobe.com/page/design-tokens/).
