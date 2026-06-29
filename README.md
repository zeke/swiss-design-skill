# swiss-design-skill

A Swiss International Style design system for AI agents. Grotesque typography, rigorous grid, generous whitespace, restrained color — expressed through Tailwind CSS.

[swiss.ziki.boo](https://swiss.ziki.boo)

## Demo

[![swiss-design-skill demo](demo-thumb.jpg)](demo.mp4)

## Install

```sh
npx skills add zeke/swiss-design-skill
```

Or manually copy the skill directory:

```sh
gh repo clone zeke/swiss-design-skill
cp -r swiss-design-skill/swiss-design ~/.config/opencode/skills/
```

## Usage

Once installed, tell your agent to apply it:

- "Apply the swiss-design skill to this page"
- "Clean up this UI using swiss design principles"
- "Make this look great — use the Swiss style"

The agent will apply IBM Plex Sans typography, the stone color palette, opacity-based hierarchy, a 12-column grid, and generous whitespace.

## What's included

```
swiss-design/
├── SKILL.md                    # Quick reference (always loaded)
└── references/
    ├── design-system.md        # Full token reference, CSS variables
    ├── components.md           # Tailwind component patterns
    ├── tailwind-config.md      # Paste-ready tailwind.config.js
    └── prompting.md            # Applying the system to existing pages
```

## Design principles

- **Grid first.** 12-column, 8px base unit
- **Whitespace is structure.** Sections get `py-24` minimum
- **Opacity, not hue, creates hierarchy.** `text-stone-900/70`, never `text-stone-500`
- **One accent.** Swiss red (`#C8102E`) by default; swap to cobalt, golden, or forest per project
- **Narrow columns.** Body text never exceeds `max-w-[60ch]`
- **Light and dark mode** via `prefers-color-scheme`

## Typography

Primary: **IBM Plex Sans** (Google Fonts)

Fallbacks: Hanken Grotesk · Barlow · Host Grotesk · DM Sans

## License

MIT
