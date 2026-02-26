# vibe-skills

Agent skills for generating and deploying production-grade websites from natural language.

Say what you want. Get a live URL. Done.

## Install

```bash
# Install the deployment layer
npx skills add heredotnow/skill --skill here-now -g

# Install vibe
npx skills add AhmadAdi/vibe-skills --skill vibe -g
```

Works with Claude Code, Cursor, Codex, Gemini CLI, and 35+ other agents.

## Usage

Just talk to your agent:

> "Build me a portfolio site for a senior ML engineer and publish it"

> "Vibe a landing page for an AI dog food startup called BarkBrain"

> "Create a restaurant site for Luigi's Italian in Berlin with menu and hours, then ship it"

The agent generates a complete site, deploys it to [here.now](https://here.now), and gives you a live URL in seconds.

## What Makes This Different

Most AI-generated websites look like AI-generated websites. Purple gradients, Inter font, three-column feature grids, "Transform your workflow" copy.

vibe generates sites that look like a freelancer charged $2,000 for them:

- **Bold aesthetic decisions** — not "modern and clean" defaults
- **Distinctive typography** — curated font pairings, never Inter/Roboto
- **Intentional color** — dominant + accent strategy, never purple/indigo
- **Unconventional layouts** — asymmetry, overlap, grid-breaking
- **Production-quality code** — semantic HTML, WCAG AA, responsive, dark mode, `prefers-reduced-motion`

## How It Works

1. **Design decision** — the agent picks an aesthetic direction, font pairing, color palette, and layout before writing a single line of code
2. **Generation** — a complete, self-contained static site following the built-in design system
3. **Quality check** — automated review against the anti-AI-slop checklist
4. **Deploy** — published to here.now, live URL returned in seconds

No accounts. No config files. No build pipeline. No subscriptions.

## Skills Included

| Skill | Purpose |
|-------|---------|
| `vibe` | Generate + deploy websites from descriptions |

Requires [`here-now`](https://github.com/heredotnow/skill) for deployment (installed separately).

## Design System

The skill includes a comprehensive design system in `references/DESIGN_SYSTEM.md` covering:

- 12 curated Google Fonts pairings with mood descriptions
- Banned font list (Inter, Roboto, Arial, system-ui, Space Grotesk, Poppins)
- 7 ready-to-use color palettes by mood
- 8px spacing grid with CSS custom properties
- Typography scales (compact and spacious)
- Animation rules (one orchestrated entry, no `transition: all`)
- Accessibility requirements (focus states, ARIA, semantic HTML)
- Dark mode implementation
- Image strategies for static deploys

## Site Types

The skill recognizes 9 site archetypes in `references/SITE_TYPES.md`:

- Portfolio / Personal
- Landing Page / Product
- Restaurant / Food
- Event / Conference
- Business / Professional
- Blog / Publication
- SaaS Dashboard
- Coming Soon
- Documentation

Each has tailored section structure, design guidance, and content density recommendations.

## Requirements

- An AI agent that supports the [Agent Skills](https://agentskills.io) specification
- The [`here-now`](https://github.com/heredotnow/skill) skill installed
- `curl`, `jq` on your system (for here.now publishing)

## License

MIT
