---
name: swiss-design
description: Apply a Swiss International Style design system using Tailwind CSS. Use when asked to style a webpage, clean up a UI, apply a design system, make something look great, or when the user references Swiss design, grotesque fonts, Helvetica, grid systems, modernist typography, or 1960s/1950s design aesthetics. Implements IBM Plex Sans typography, stone color palette, opacity-based hierarchy, generous whitespace, and structured grid layouts.
license: MIT
metadata:
  author: zeke
  version: "1.0"
---

# Swiss Design System

A design system rooted in the Swiss International Style of the 1950s–60s: grotesque typography, rigorous grid, bold geometric forms, generous whitespace, and restrained color.

## Six Principles

1. **Grid first.** Every layout lives on a 12-column grid with an 8px base unit.
2. **Mobile first, always.** Design for the smallest viewport first, then expand. Every layout must work at 320px and at 1440px. Use `sm:`, `md:`, `lg:` Tailwind prefixes systematically.
3. **Whitespace is structure.** Generous padding and margins are not waste — they are the design.
4. **Opacity, not hue, creates hierarchy.** Never introduce a second color to indicate text weight or importance. Use opacity.
5. **One accent.** Each project gets exactly one accent color, used sparingly at multiple opacities.
6. **Narrow columns.** Body text never exceeds `max-w-[60ch]`. Wider columns hurt legibility.

---

## Typography

**Primary font:** IBM Plex Sans (Google Fonts)

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:ital,wght@0,300;0,400;0,500;0,600;1,300;1,400&display=swap" rel="stylesheet">
```

**Fallback chain** (in order of preference):

| Font | Source | Character |
| ---- | ------ | --------- |
| IBM Plex Sans | Google Fonts | Primary. Rational, slightly condensed, 1960s systems rationalism |
| Hanken Grotesk | Google Fonts | Closest to Neue Haas Grotesk lineage |
| Barlow | Google Fonts | Condensed Swiss-grid proportions, strong vertical rhythm |
| Host Grotesk | Google Fonts | Warm grotesque, good at all sizes |
| DM Sans | Google Fonts | Clean neo-grotesque fallback |
| system-ui | Built-in | Last resort |

```css
font-family: 'IBM Plex Sans', 'Hanken Grotesk', 'Barlow', 'Host Grotesk', 'DM Sans', system-ui, sans-serif;
```

**Type scale:**

| Role | Tailwind | Line height | Max width |
| ---- | -------- | ----------- | --------- |
| Display | `text-7xl font-light tracking-tight` | `leading-none` | unconstrained |
| H1 | `text-5xl font-light tracking-tight` | `leading-tight` | unconstrained |
| H2 | `text-3xl font-light tracking-tight` | `leading-snug` | unconstrained |
| H3 | `text-xl font-normal` | `leading-snug` | unconstrained |
| Body | `text-base font-normal` | `leading-relaxed` | `max-w-[60ch]` |
| Small | `text-sm font-normal` | `leading-relaxed` | `max-w-[60ch]` |
| Caption | `text-xs font-normal tracking-wide uppercase` | `leading-normal` | unconstrained |
| Mono | `font-mono text-sm` | `leading-relaxed` | `max-w-[60ch]` |

- Headings: `font-light` (300) or `font-normal` (400). Never bold for headings.
- Emphasis within body: `font-medium` (500). Never `font-bold` (700).
- Letter spacing on display/h1: `tracking-tight` (-0.02em).
- Captions and labels: `tracking-wide uppercase text-xs`.

### Typographic details

The Swiss style depends on typographic precision. These rules are non-negotiable:

- Use the ellipsis character `…`, never three periods `...`.
- Use curly quotes `"` `"` and `'` `'`, never straight quotes `"` `'`.
- Loading and progress states end with an ellipsis: `Loading…`, `Saving…`.
- Number columns and tables use `font-variant-numeric: tabular-nums` (Tailwind: `tabular-nums`) so digits align vertically.
- Headings use `text-wrap: balance` (Tailwind: `text-balance`) to prevent widows. Body paragraphs use `text-pretty` where supported.
- Non-breaking spaces between value and unit, and inside brand names: `10&nbsp;MB`, `⌘&nbsp;K`.

---

## Color System

### Stone palette (light mode → dark mode)

| Role | Light | Dark | Tailwind |
| ---- | ----- | ---- | -------- |
| Page background | `stone-50` | `stone-950` | `bg-stone-50 dark:bg-stone-950` |
| Surface / card | `stone-100` | `stone-900` | `bg-stone-100 dark:bg-stone-900` |
| Subtle surface | `stone-200` | `stone-800` | `bg-stone-200 dark:bg-stone-800` |
| Border | `stone-200` | `stone-800` | `border-stone-200 dark:border-stone-800` |
| Subtle border | `stone-100` | `stone-900` | `border-stone-100 dark:border-stone-900` |
| Primary text | `stone-900` | `stone-50` | `text-stone-900 dark:text-stone-50` |
| Secondary text | `stone-900/70` | `stone-50/70` | `text-stone-900/70 dark:text-stone-50/70` |
| Tertiary text | `stone-900/40` | `stone-50/40` | `text-stone-900/40 dark:text-stone-50/40` |
| Placeholder | `stone-900/30` | `stone-50/30` | `text-stone-900/30 dark:text-stone-50/30` |

### Opacity hierarchy (the core rule)

To make text less dominant, reduce opacity — never change the hue.

```
Full presence:   text-stone-900          (primary)
Softer:          text-stone-900/70       (secondary, labels)
Quiet:           text-stone-900/40       (tertiary, captions)
Ghosted:         text-stone-900/20       (disabled, placeholder)
```

Dark mode: replace `stone-900` with `stone-50`. The opacity values stay identical.

### Accent color

Each project uses **one** accent color. Default is Swiss poster red.

| Name | Hex | Tailwind arbitrary |
| ---- | --- | ------------------ |
| Swiss Red (default) | `#C8102E` | `[#C8102E]` |
| Cobalt | `#003B8E` | `[#003B8E]` |
| Golden | `#F0B429` | `[#F0B429]` |
| Forest | `#2D6A4F` | `[#2D6A4F]` |

Use accent at these opacities only:

```
Full:    bg-[#C8102E]          text-[#C8102E]
Muted:   bg-[#C8102E]/60       text-[#C8102E]/60
Subtle:  bg-[#C8102E]/20       (backgrounds, tints)
Ghost:   bg-[#C8102E]/10       (very light tints)
```

---

## Spacing & Grid

**Base unit:** 8px. All spacing is a multiple of 8.

| Token | Value | Usage |
| ----- | ----- | ----- |
| `gap-2` | 8px | Tight inline gaps |
| `gap-4` | 16px | Component internal |
| `gap-8` | 32px | Between components |
| `gap-16` | 64px | Between sections |
| `py-16` | 64px | Section padding (minimum) |
| `py-24` | 96px | Section padding (standard) |
| `py-32` | 128px | Section padding (generous) |

**Grid:**

```html
<!-- 12-column grid — always mobile-first, columns collapse to full-width on small screens -->
<div class="grid grid-cols-12 gap-4 md:gap-8">
  <div class="col-span-12 md:col-span-8">...</div>
  <div class="col-span-12 md:col-span-4">...</div>
</div>
```

**Max content width:** `max-w-5xl` or `max-w-6xl` with `mx-auto px-4 md:px-8`.

---

## Responsive Design

The Swiss grid adapts fluidly across viewports. Every layout decision must be made at two scales: mobile (single column, generous vertical rhythm) and desktop (multi-column, horizontal tension).

**Breakpoint strategy:**

| Prefix | Width | Use for |
| ------ | ----- | ------- |
| (none) | 0px+ | Mobile — single column, full width |
| `sm:` | 640px+ | Large phones, small tablets |
| `md:` | 768px+ | Tablets, narrow desktop — introduce 2-col layouts |
| `lg:` | 1024px+ | Desktop — full 12-col grid, max content width |

**Mobile layout rules:**
- All grid columns collapse to `col-span-12`
- Section padding reduces: `py-16 md:py-24 lg:py-32`
- Horizontal padding tightens: `px-4 md:px-8`
- Display type scales down: `text-5xl md:text-7xl lg:text-8xl`
- Multi-column nav collapses to hamburger or hidden
- Tables scroll horizontally: wrap in `overflow-x-auto`
- Side-by-side cards stack vertically: `grid-cols-1 md:grid-cols-2 lg:grid-cols-3`

**Fluid type pattern:**

```html
<!-- Scale display type fluidly across viewports -->
<h1 class="text-4xl sm:text-5xl md:text-6xl lg:text-7xl font-normal tracking-tight leading-none">
  Swiss International Style
</h1>

<!-- Or use clamp() for truly fluid scaling -->
<h1 class="text-[clamp(2rem,6vw,5rem)] font-normal tracking-tight leading-none">
  Swiss International Style
</h1>
```

**Responsive section pattern:**

```html
<section class="py-16 md:py-24 lg:py-32 border-b border-stone-200 dark:border-stone-800">
  <div class="max-w-6xl mx-auto px-4 md:px-8">
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
      ...
    </div>
  </div>
</section>
```

**Touch targets:** All interactive elements must be at least 44×44px on mobile. Use `min-h-[44px] min-w-[44px]` for buttons and nav links.

**Navigation on mobile:** Collapse to a minimal top bar. Hide secondary nav links below `md:`. Never use hamburger menus with deeply nested hierarchies — the Swiss style favors flat, clear navigation.

---

## Dark Mode

Use Tailwind's `media` strategy (respects system preference automatically):

```js
// tailwind.config.js
darkMode: 'media'
```

Every color token has a `dark:` variant. See the stone palette table above. Never use `bg-black` or `bg-white` — always use stone scale.

### `color-scheme`

Tailwind only restyles your code. The browser still renders scrollbars, native form controls, and the canvas before CSS loads using its own defaults. Without `color-scheme`, a Swiss page in dark mode shows light scrollbars and light-mode native inputs against `bg-stone-950`.

Always declare both schemes on `<html>`:

```css
html { color-scheme: light dark; }
```

Or via meta tag (parsed before CSS, prevents flash):

```html
<meta name="color-scheme" content="light dark">
```

Also set `<meta name="theme-color">` to match the page background so the mobile browser chrome blends in.

---

## Gotchas

- **Never use a second color to signal hierarchy.** Opacity only. `text-stone-900/70`, not `text-stone-500`.
- **Never exceed `max-w-[60ch]` for body text.** Wider columns are illegible.
- **Never `bg-white` or `bg-black`.** Use `bg-stone-50` / `bg-stone-950`.
- **IBM Plex Sans is not a system font.** Always include the Google Fonts `<link>` tag.
- **One accent per project.** Do not introduce a second accent color. Use opacity variations instead.
- **Headings are light, not bold.** `font-light` for display and h1, `font-normal` for h2–h3.
- **No border-radius on structural elements.** Inputs, cards, and containers use `rounded-none` or at most `rounded-sm`. The Swiss style is rectilinear.
- **Section padding is generous.** Minimum `py-16`, standard `py-24`. Never less.
- **Every layout must work on mobile.** Default (no prefix) classes are mobile. Always add `md:` and `lg:` variants for larger viewports. Never build desktop-first and try to retrofit mobile.
- **Tables on mobile need `overflow-x-auto`.** Never let a wide table break mobile layout.
- **Touch targets minimum 44px.** Buttons, links, and nav items must be tappable on mobile.
- **Fluid type, not fixed.** Use responsive type classes (`text-3xl md:text-5xl`) or `clamp()` — never a single fixed size that works only at one viewport.
- **Never `outline-none` without a focus replacement.** Interactive elements need a visible focus indicator. Use `focus-visible:ring-2 focus-visible:ring-stone-900 dark:focus-visible:ring-stone-50` (or the accent) instead. Prefer `:focus-visible` over `:focus` so the ring only appears on keyboard navigation.
- **Honor `prefers-reduced-motion`.** If you add transitions or animations, gate them: `motion-safe:transition motion-reduce:transition-none`. Animate only `transform` and `opacity`. Never `transition: all`.
- **Set `color-scheme: light dark` on `<html>`.** Otherwise scrollbars and native form controls stay light in dark mode.
- **Straight quotes and `...` are bugs.** Use curly quotes and the `…` character.

---

## Behavior, accessibility, and quality

This skill is an aesthetic and visual system. It does not cover accessibility, focus management, form behavior, hydration, performance, or interaction quality.

For those, defer to the Vercel Web Interface Guidelines, which are framework-agnostic and complementary:

- Skill: `vercel-labs/agent-skills/web-design-guidelines`
- Raw rules: https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/command.md

After applying Swiss styling, fetch the rules above and audit the result for accessibility, focus states, form behavior, animation safety, performance, and i18n. Treat findings as required fixes, not suggestions. Where the two systems overlap (typography niceties, dark mode, focus rings), the rules already inlined in this SKILL.md take precedence.

## When to read reference files

| Task | File |
| ---- | ---- |
| Full color token table, CSS custom properties, dark mode details | `references/design-system.md` |
| Tailwind component patterns: buttons, cards, nav, forms, badges | `references/components.md` |
| Paste-ready `tailwind.config.js` and CSS `@theme` block | `references/tailwind-config.md` |
| Applying this system to an existing page, audit checklist | `references/prompting.md` |
