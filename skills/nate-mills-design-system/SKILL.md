---
name: nate-mills-design-system
description: Build any page, prototype, component or document that must look like natemills.me, using the Nate Mills design system. Use when a brief names natemills.me, Nate Mills, his portfolio or design system, or asks for something "on brand" for him. Links the live CSS, uses the published classes and tokens by name, and follows the rules that keep the result from looking generated.
license: MIT
metadata:
  author: Nate Mills
  homepage: https://natemills.me/design-system
---

# Nate Mills design system

The system is a small CSS class layer over DTCG tokens, served live from natemills.me. You link it; you never rebuild it from values.

## Do this, in order

1. Read `references/AGENTS.md` beside this file (the foundation links, the rules, the published classes with examples, the token names). It is short and always applies.
2. Link the foundation exactly as its first block shows, in that order.
3. Compose from the published classes before writing a value. For anything else, write your own class next to them using `var(--token)` names only.
4. Need a value, a recipe, the voice or the do's and don'ts? Read `references/DESIGN.md`. Need the classes as data (selectors, states, tokens read)? https://natemills.me/components-api.json.
5. Check both themes (`data-theme="dark"` on `<html>`) and WCAG 2.2 AA: 4.5:1 body text, 3:1 non-text, a visible focus ring.

## Never

- Invent a class name, a hex, or a px of your own.
- Redefine a published class. Compose around it.
- Use lime as text on a light surface, or load the mono from Google Fonts.
- Add a shadow to a card, a gradient to a surface, or opacity for hierarchy.

Both references are the live documents at https://natemills.me/AGENTS.md and https://natemills.me/DESIGN.md; the copies here are published from the same source.
