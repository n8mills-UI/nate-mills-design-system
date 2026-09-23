<div align="center">

<img src="https://raw.githubusercontent.com/n8mills-UI/nate-mills-design-system/main/assets/header-banner.png" alt="Nate Mills Design System. Authored once as DTCG tokens, generated to CSS, audited to WCAG 2.2 AA." width="860">

[![License: MIT](https://img.shields.io/badge/License-MIT-d2ff37?style=flat-square&labelColor=1c1c1f)](./LICENSE)
[![Design Tokens: DTCG](https://img.shields.io/badge/Design_Tokens-DTCG-d2ff37?style=flat-square&labelColor=1c1c1f)](https://www.designtokens.org/)
[![WCAG 2.2 AA](https://img.shields.io/badge/WCAG-2.2_AA-d2ff37?style=flat-square&labelColor=1c1c1f)](https://www.w3.org/WAI/WCAG22/quickref/)
[![Built with Style Dictionary](https://img.shields.io/badge/Built_with-Style_Dictionary-1c1c1f?style=flat-square)](https://styledictionary.com)

[![Design system, live](https://img.shields.io/badge/Design_system-Live-d2ff37?style=flat-square&labelColor=1c1c1f)](https://natemills.me/#uth-colour)
[![Live site](https://img.shields.io/badge/Live-natemills.me-1c1c1f?style=flat-square)](https://natemills.me)
[![Case study](https://img.shields.io/badge/Case_study-Bupa-1c1c1f?style=flat-square)](https://bupa.natemills.me)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-millsdesign-0a66c2?style=flat-square&logo=data:image/svg%2Bxml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0id2hpdGUiPjxwYXRoIGQ9Ik0yMC40NDcgMjAuNDUyaC0zLjU1NHYtNS41NjljMC0xLjMyOC0uMDI3LTMuMDM3LTEuODUyLTMuMDM3LTEuODUzIDAtMi4xMzYgMS40NDUtMi4xMzYgMi45Mzl2NS42NjdIOS4zNTFWOWgzLjQxNHYxLjU2MWguMDQ2Yy40NzctLjkgMS42MzctMS44NSAzLjM3LTEuODUgMy42MDEgMCA0LjI2NyAyLjM3IDQuMjY3IDUuNDU1djYuMjg2ek01LjMzNyA3LjQzM2EyLjA2MiAyLjA2MiAwIDAxLTIuMDYzLTIuMDY1IDIuMDY0IDIuMDY0IDAgMTEyLjA2MyAyLjA2NXptMS43ODIgMTMuMDE5SDMuNTU1VjloMy41NjR2MTEuNDUyek0yMi4yMjUgMEgxLjc3MUMuNzkyIDAgMCAuNzc0IDAgMS43Mjl2MjAuNTQyQzAgMjMuMjI3Ljc5MiAyNCAxLjc3MSAyNGgyMC40NTFDMjMuMiAyNCAyNCAyMy4yMjcgMjQgMjIuMjcxVjEuNzI5QzI0IC43NzQgMjMuMiAwIDIyLjIyNSAweiIvPjwvc3ZnPg==&logoColor=white)](https://www.linkedin.com/in/millsdesign)

</div>

This is the real design system behind my portfolio, opened up so you can see how it is built, not just that it exists. It is small on purpose: one accent, a tuned neutral scale, two fonts, and a strict three-tier token model. Everything starts in one `tokens.json` file and propagates outward, so reskinning the brand is a one-line change and every component follows.

I publish it because the discipline is the point. A design system is easy to claim and hard to govern. This repo is the audit trail for the claims: the token source, the generated CSS, the component layer, and the written rules that keep them honest.

> **See it live.** The [under-the-hood design system](https://natemills.me/#uth-colour) resolves every token in real time, in light and dark, section by section. This repo is the source it runs on.

## What's inside

One source, three generated outputs, and the discipline between them. That is the whole system.

- **`tokens.json`** : the single source of truth, in the [W3C Design Tokens Community Group](https://www.designtokens.org/) (DTCG) format. Three tiers: primitives (raw values), semantics (roles), and component tokens (btn/card/chip/badge, aliasing semantics only).
- **`tokens.css`** : the generated CSS custom properties, built from `tokens.json` by [Style Dictionary](https://styledictionary.com). All three themes (light, dark, high-contrast) included. Never hand-edited.
- **`tokens.js` / `tokens.d.ts`** : the same tokens as a typed JavaScript object, resolved to literal values for the default theme. For build tools that read tokens in JS, not CSS. Generated, never hand-edited.
- **`components.css`** : the component layer. Buttons, cards, chips, and the section heading pattern, each reading semantic tokens only.
- **[`DESIGN.md`](./DESIGN.md)** : the portable brand contract and the written rules. One self-contained file that hands an AI coding agent (or a contractor) everything it needs to build on-brand without the repo: resolved colour, type, spacing and radius values in the frontmatter, a component recipe map, the do's and don'ts, and the voice guide for copy. The value blocks are generated from `tokens.json` and drift-gated, so they never fall out of sync with the system.

Prefer the guided tour to the raw source? The [live view](https://natemills.me/#uth-colour) walks every section with the real values resolved.

## The model in one breath

```
PRIMITIVES   raw values, named by hue and stop      -->  e.g. --neutral-850: #1c1c1f
SEMANTICS    roles, reference primitives via var()   -->  e.g. --color-accent: var(--neutral-850)
COMPONENTS   classes that read semantics only        -->  e.g. .btn--primary { background: var(--brand-primary) }
```

One way, top to bottom: components read semantics, semantics read primitives, primitives are literals. Nothing reaches back up. So one edit at the top, a new brand hue, propagates through every semantic and component that uses it. No find-and-replace, no drift. That propagation is the whole point.

## The foundations at a glance

<div align="center">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/n8mills-UI/nate-mills-design-system/main/assets/bento-foundations-dark.png">
  <img src="https://raw.githubusercontent.com/n8mills-UI/nate-mills-design-system/main/assets/bento-foundations-lime.png" alt="The design system foundations in one view: the lime and neutral colour ramps with their stop numbers, the Anton display specimen, the Work Sans, JetBrains Mono and PT Serif faces, and the spacing scale drawn at true width" width="860">
</picture>
</div>

Colour, type, and spacing, all generated from `tokens.json`. Display type is Anton, set large and tight; Work Sans carries body copy and controls; JetBrains Mono is for labels and numbers, with the slashed zero the system insists on; and PT Serif is kept for the one place that earns it: the pull quotes.

## Accessibility is a constraint, not a feature

It is wired into the tokens, so you cannot opt out of it by accident:

- Every text token is contrast-checked for WCAG 2.2 AA: a blocking CI lint over the token source in both themes, plus live ratio computation on the Under-the-Hood page.
- Focus rings are never removed without a replacement.
- Default control height is 44 by 44 px. Two documented dense sizes sit below it on purpose, a 32px small button and a 24px dot; both clear the WCAG 2.5.8 AA 24px floor and carry a larger pointer target than their painted box.
- Every animation is gated behind `prefers-reduced-motion`, collapsed in one place, not per component.

There is one honest carveout. The brand lime is a background and accent only. It fails as foreground text on the light surface, roughly 1.06 to 1, so the system refuses to let you use it there and hands you a theme-aware token instead. The full reasoning is in [`DESIGN.md`](./DESIGN.md#color-roles).

## Use it

The fastest route is to link the live foundation. No install, no build step, and it is the same CSS
the site runs on, so it cannot fall behind.

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Anton&family=PT+Serif:ital,wght@0,400;0,700;1,400;1,700&family=Work+Sans:ital,wght@0,400..800;1,400..800&display=swap" rel="stylesheet">
<link href="https://natemills.me/assets/fonts.css" rel="stylesheet">
<link href="https://natemills.me/assets/tokens.css" rel="stylesheet">
<link href="https://natemills.me/assets/components.css" rel="stylesheet">
```

Then compose with the published classes and tokens:

```html
<button class="btn btn--primary">Get in touch</button>
```

```css
.cta {
  background: var(--brand-primary);
  color: var(--brand-ink);
  border-radius: var(--radius-md);
  padding: var(--space-3) var(--space-5);
}
```

`tokens.css` carries every custom property in all three themes and `components.css` reads them, so
tokens must load first. `fonts.css` declares the self-hosted mono and its slashed zero.

**Building with an AI agent?** Point it at [`DESIGN.md`](./DESIGN.md), or at
`https://natemills.me/DESIGN.md`. It is a self-contained brief: the resolved values, the class API
to link against, and the rules that keep the result from looking generated.

Prefer the source? Clone it and take what you need, including the raw DTCG token file and the typed
JS export:

```bash
git clone https://github.com/n8mills-UI/nate-mills-design-system.git
```

> **Note on npm.** `@n8mills/design-tokens` was published in 2026 and is no longer maintained. The
> registry copy is frozen at an old version and does not match this repo. Link the CSS above or
> clone the source instead.

See the [live design system](https://natemills.me/#under-the-hood) for the why. Read [`DESIGN.md`](./DESIGN.md), `tokens.json` and `components.css` for the how. Fork it for another brand by changing `--lime-500` and watching every consumer follow. That is the system working as designed.

## License

[MIT](./LICENSE). Use it, learn from it, build on it.

---

<div align="center">

Built by Nate Mills, Design Systems and Full-Stack Design.
[natemills.me](https://natemills.me) | [LinkedIn](https://www.linkedin.com/in/millsdesign)

</div>
