# AGENTS.md: building with the Nate Mills design system

Rules for any AI coding agent building something that must look like natemills.me. Values live in DESIGN.md, the class facts as data in components-api.json. In your own AGENTS.md (or CLAUDE.md, for Claude Code) add: "Before writing UI for natemills.me, read https://natemills.me/AGENTS.md and follow it."

## Link the foundation, never rebuild it

<!-- AGENTS:links:start -->
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Work+Sans:ital,wght@0,400..800;1,400..800&display=swap" rel="stylesheet">
<link href="https://natemills.me/assets/fonts.css" rel="stylesheet">
<link href="https://natemills.me/assets/tokens.css" rel="stylesheet">
<link href="https://natemills.me/assets/components.css" rel="stylesheet">
```
<!-- AGENTS:links:end -->

Tokens before components. fonts.css is required (self-hosted Anton and JetBrains Mono, with its slashed zero). Never `@import`, `file://` or a placeholder address. The foundation styles classes, not elements: set `body { font-family: var(--font-body); color: var(--color-text-primary); background: var(--color-bg); }` and your headings yourself. Icons are Lucide: `<i data-lucide="name" aria-hidden="true">` stays empty until you load Lucide and call `lucide.createIcons()`.

## Rules

1. Use a published class before a value. The list below is the whole public API; anything else in components.css is a portfolio internal.
2. Use the exact names. No `.button`, no `.btn-primary`, no `.card-dark`.
3. Never redefine a published class. Compose: write your own class next to `.btn` or `.card`, never inside it.
4. Every colour, size, radius, border and spacing is a `var(--token)` from the names below. No hex and no px of your own.
5. Semantic names flip by theme on their own: `--color-bg`, `--color-text-primary`, `--color-accent`. There is no `--dark-*` or `--darkTheme-*` name; the dark value belongs to the same property.
6. Lime (`--brand-primary`) is scarce: primary button, brand outlines, focus rings on dark, status dots. Never body text on a light surface. For a selected state use `--color-accent`.
7. Pick the surface first (`--color-bg`, `--color-surface`, `--color-surface-sunken`, or always-dark `--color-surface-inverse`), then its text: `--color-text-*` on light, `--color-on-ink-*` on a dark slab.
8. Hairline borders separate (`--border-hairline`); a shadow is only for an overlay. No gradients on surfaces, no opacity for hierarchy.
9. Both themes are first class. Build light, then check dark: `data-theme="dark"` on `<html>`.
10. WCAG 2.2 AA in both themes: 4.5:1 body text, 3:1 large text and non-text, a visible focus ring. Default targets are 44px (`--touch-target-min`); the dense `.btn--sm` is 32px, which still clears AA's 24px minimum. An icon is decorative: give its control a text label or an `aria-label`.

## Slips seen in our agent test (October 2026, 15 builds)

- Hand-building carousel controls (`.ds-carousel-nav` exists). Nav bars and form fields have no published class: build them from tokens and leave `.btn` alone.
- Copying a dark-theme name that does not exist (see rule 5).
- Leaving an error state uncoloured: the one feedback colour is for errors, so copy `.card--error`. There is no success or warning colour.

## Published classes

<!-- AGENTS:classes:start -->
**Buttons:** Base .btn is the 44px default. Size modifiers wire the --btn-* tokens.
`.btn`, `.btn--primary`, `.btn--secondary`, `.btn--icon`, `.btn--sm`, `.btn--md`, `.btn--lg`

```html
<a class="btn btn--primary" href="mailto:mail@natemills.me">Say G'day</a>
<button class="btn btn--icon" type="button" aria-label="Toggle dark mode"><i data-lucide="moon" aria-hidden="true"></i></button>
```

**Cards:** Surface step plus a hairline border. Never a drop shadow.
`.card`, `.card--dark`, `.card--interactive`, `.card--compact`, `.card--spacious`, `.card--empty`, `.card--error`, `.card--loading`

```html
<a class="card card--interactive" href="/work">
  <h3>Card title</h3>
  <p>One or two lines of body copy.</p>
</a>
```

**Chips and badges:** Resolve by job: a label is a chip, a status is a badge. A badge is read-only, never interactive.
`.chip`, `.chip--outline`, `.badge`, `.badge__dot`

```html
<span class="chip chip--outline">Design systems</span>
<span class="badge"><span class="badge__dot" aria-hidden="true"></span>Open to work</span>
```

**Section heading:** The section-head block owns the gap from heading to body. Do not add your own margin.
`.section-head`, `.section-label`, `.section-label--accent`, `.section-label--center`, `.section-label--icon`, `.section-label--row`, `.section-title`, `.section-subtitle`

```html
<div class="section-head">
  <h2 class="section-title">Training</h2>
</div>
<p class="section-label">Degree</p>
```

**Links:** A border-bottom underline, so the rule colours and animates independently of the text.
`.link-underline`, `.link-underline--prose`, `.link-underline--icon`

```html
<a class="link-underline link-underline--prose" href="https://natemills.me">natemills.me</a>
```

**Carousel navigation:** Bare chevrons plus a mono counter on a rail BELOW the cards. One nav, site-wide.
`.ds-carousel-nav`, `.ds-carousel-nav--full`, `.ds-carousel-nav__rail`, `.ds-carousel-nav__arrow`, `.ds-carousel-nav__pager`, `.ds-carousel-nav__fill`, `.ds-carousel-nav__count`

**Other**
`.avatar`, `.sr-only`

```html
<span class="avatar"><img src="your-portrait.jpg" alt="Your name" width="44" height="44"></span>
<span class="sr-only">Opens in a new tab</span>
```
<!-- AGENTS:classes:end -->

## Token names you will use

As the CSS declares them; values are in DESIGN.md.

<!-- AGENTS:names:start -->
- **Colour (the same names in every theme):** `--brand-primary`, `--brand-primary-dim`, `--brand-primary-vivid`, `--brand-secondary`, `--brand-ink`, `--brand-gradient`, `--color-bg`, `--color-surface`, `--color-surface-sunken`, `--color-surface-inverse`, `--color-text-primary`, `--color-text-secondary`, `--color-text-tertiary`, `--color-border`, `--color-border-strong`, `--color-border-brand`, `--color-accent`, `--color-accent-hover`, `--color-on-accent`, `--color-focus-ring`, `--color-link`, `--color-link-hover`, `--color-on-ink-primary`, `--color-on-ink-secondary`, `--color-on-ink-muted`, `--color-on-ink-border`, `--color-feedback-background-error`, `--color-on-feedback-error`, `--color-overlay-soft`, `--color-overlay-base`, `--color-overlay-strong`
- **Font families:** `--font-display`, `--font-body`, `--font-mono`
- **Type styles (size, weight, line height, tracking):** `--display-hero`, `--display-weight`, `--line-display`, `--display-tight`, `--display-section`, `--weight-extrabold`, `--text-h1`, `--text-h2`, `--line-heading`, `--tracking-tight`, `--display-card-title`, `--display-stat-num`, `--display-intro`, `--weight-regular`, `--line-snug`, `--text-body`, `--line-body`, `--tracking-normal`, `--size-sm`, `--text-caption`, `--text-label`, `--weight-medium`, `--tracking-label`
- **Radius:** `--radius-none`, `--radius-sm`, `--radius-md`, `--radius-lg`, `--radius-xl`, `--radius-full`
- **Spacing:** `--space-50`, `--space-100`, `--space-200`, `--space-250`, `--space-300`, `--space-400`, `--space-500`, `--space-600`, `--space-700`, `--space-800`, `--space-900`, `--space-1000`, `--space-1100`, `--space-1200`, `--section-padding`, `--card-pad-compact`, `--card-pad-standard`, `--card-pad-spacious`
- **Borders, focus and targets:** `--border-hairline`, `--border-strong`, `--border-focus`, `--focus-ring-offset`, `--touch-target-min`
<!-- AGENTS:names:end -->

## More

- DESIGN.md: https://natemills.me/DESIGN.md (values, recipes, voice and tone)
- components-api.json: https://natemills.me/components-api.json (the classes as data)
- Index for AI tools: https://natemills.me/llms.txt
- Claude Code plugin: `claude plugin marketplace add n8mills-UI/nate-mills-design-system`, then `claude plugin install nate-mills-design-system@nate-mills-design-system`
