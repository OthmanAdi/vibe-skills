# vibe

> **Your AI agent. One sentence. A website that looks like a $2,000 freelancer built it.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-1.0.0-brightgreen)](https://github.com/OthmanAdi/vibe-skills/releases)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-Spec-blue)](https://agentskills.io)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-green)](https://claude.ai/code)
[![Cursor](https://img.shields.io/badge/Cursor-Skills-purple)](https://docs.cursor.com/context/skills)
[![Gemini CLI](https://img.shields.io/badge/Gemini%20CLI-Skills-4285F4)](https://geminicli.com/docs/cli/skills/)
[![Codex](https://img.shields.io/badge/Codex-Skills-000000)](https://openai.com/codex)
[![SkillCheck Validated](https://img.shields.io/badge/SkillCheck-Validated-4c1)](https://getskillcheck.com)

Generate production-grade websites from natural language and deploy them live in seconds — via [here.now](https://here.now), the instant web host for AI agents.

No accounts. No config files. No build pipeline. No subscriptions.

---

## Quick Install

```bash
# 1. Install the deployment layer (here.now)
npx skills add heredotnow/skill --skill here-now -g

# 2. Install vibe
npx skills add OthmanAdi/vibe-skills --skill vibe -g
```

Works with Claude Code, Cursor, Codex, Gemini CLI, and 40+ other agents.

Then just talk to your agent:

```
"Build me a portfolio site for a senior ML engineer and publish it"
"Vibe a landing page for an AI dog food startup called BarkBrain"
"Create a restaurant site for Luigi's Italian in Berlin with menu and hours, then ship it"
```

---

## Why vibe?

Most AI-generated websites are instantly recognizable:

- Purple or indigo gradient hero
- Inter font, always
- Three-column feature grid: icon + heading + two lines of text
- "Transform your workflow. Empower your team. Unlock your potential."
- Generic stock photos in cropped circles

vibe was built to fix that. It enforces a design decision phase **before any code is written** — aesthetic direction, font pairing, color palette, and layout strategy all chosen deliberately for the specific brief. The result looks like a freelancer spent a day on it, not like an AI ran a template.

---

## The Problem

Every AI website generator has the same output. The model defaults to:

| Default AI behavior | What it produces |
|--------------------|-----------------|
| Primary color | Purple `#7c3aed` or Indigo `#6366f1` |
| Font | Inter, Roboto, or system-ui |
| Layout | Hero → 3-col features → testimonials → CTA |
| Copy | "Streamline your workflow", "AI-powered", "Seamless" |
| Code | `<div onClick>`, no focus states, no dark mode |

The output is technically functional. It just looks like every other AI website.

---

## The Solution: 4-Phase Workflow

### Phase 0 — Design Decision (before any code)

The agent reads `references/DESIGN_SYSTEM.md` and commits to:

1. **Site type** — matched to one of 9 archetypes in `references/SITE_TYPES.md`
2. **Aesthetic direction** — one of: Brutally minimal, Luxury/refined, Editorial/magazine, Brutalist/raw, Art deco/geometric, Retro-futuristic, Organic/natural, Dark cinematic, Warm earthy, Monochrome high-contrast
3. **Font pairing** — selected from 12 curated pairings. Inter, Roboto, Arial, and Space Grotesk are banned.
4. **Color palette** — one dominant color, one sharp accent. Purple/indigo gradients are banned.
5. **Layout strategy** — breaks from the default template. Asymmetry, overlap, and grid-breaking encouraged.

The agent presents this plan in 2–3 sentences before writing a single line of HTML.

### Phase 1 — Generate

Creates a self-contained static site in `./vibe-output/`:

```
vibe-output/
  index.html          # Always
  styles.css          # If CSS exceeds 50 lines
  app.js              # Only if interactive behavior is needed
```

For simple sites, a single `index.html` with embedded `<style>` is preferred.

**Enforced rules:** Google Fonts via `<link>`, CSS custom properties for all colors and spacing, real content (never lorem ipsum), mobile-first responsive, semantic HTML, dark mode via `prefers-color-scheme`, and real Unsplash photo IDs or inline SVG (no placeholder services).

### Phase 2 — Review

Before deploying, the agent verifies:

- [ ] No purple/indigo gradients as primary palette
- [ ] No Inter, Roboto, Arial, or system-ui as primary font
- [ ] CSS custom properties for all colors and spacing
- [ ] All interactive elements have `:focus-visible` states
- [ ] Touch targets at least 44×44px
- [ ] `prefers-reduced-motion` respected
- [ ] No `transition: all` — specific properties listed
- [ ] No `<div onClick>` — `<button>` for actions, `<a>` for navigation
- [ ] All images have explicit `width` and `height`
- [ ] Responsive at 375px, 768px, and 1024px

Failures are fixed before deployment.

### Phase 3 — Deploy

```bash
cd ./vibe-output && ~/.agents/skills/here-now/scripts/publish.sh .
```

Returns a live URL in seconds. Anonymous deploys expire in 24 hours; claim the URL to make it permanent.

### Phase 4 — Iterate

```bash
cd ./vibe-output && ~/.agents/skills/here-now/scripts/publish.sh . --slug {slug}
```

Updates the existing URL in place. No new link needed.

---

## Design System

The built-in design system in `references/DESIGN_SYSTEM.md` covers:

### Font Pairings (12 curated, mood-matched)

| Display | Body | Mood |
|---------|------|------|
| Playfair Display | Source Sans 3 | Editorial, luxury |
| Fraunces | Outfit | Warm, approachable |
| Sora | DM Sans | Tech, contemporary |
| Libre Baskerville | Karla | Classic, trustworthy |
| Space Mono | Work Sans | Developer, technical |
| Cormorant Garamond | Montserrat | Elegant, refined |
| Bricolage Grotesque | Geist | Sharp, editorial |
| Instrument Serif | Inter Tight | Contrast, sophisticated |
| DM Serif Display | Manrope | Bold, contemporary |
| Lora | Nunito Sans | Warm, readable |
| Bitter | Raleway | Sturdy, professional |

**Banned:** Inter, Roboto, Arial, Helvetica, system-ui, Space Grotesk, Poppins.

### Color Palettes (7 by mood)

| Mood | Background | Primary | Accent |
|------|-----------|---------|--------|
| Warm professional | `#faf9f6` cream | Forest `#2d5016` | Burnt orange `#c44e1b` |
| Cool minimal | `#f8f9fa` | Slate `#334155` | Teal `#0d9488` |
| Dark cinematic | `#0a0a0a` | Warm white `#f5f0eb` | Gold `#d4a843` |
| Bold editorial | `#fffff0` ivory | Crimson `#b91c1c` | Near-black |
| Soft natural | `#f5f1eb` sand | Sage `#7c9473` | Terracotta `#c67b5c` |
| Monochrome punch | `#ffffff` | Black | Electric `#ff3b00` |
| Tech/dark | `#111111` | Neon green `#4ade80` | White |

**Banned:** Purple/indigo/violet gradients, Tailwind blue-500 as primary, evenly distributed rainbow palettes.

### Also Included

- 8px spacing grid as CSS custom properties
- Two modular typography scales (compact 1.2:1 ratio, spacious 1.333:1 ratio)
- Fluid font sizes with `clamp()`
- Animation rules — one orchestrated entry, only `transform` and `opacity`, `prefers-reduced-motion` respected
- WCAG AA contrast requirements (4.5:1 body, 3:1 large text)
- Dark mode implementation via `prefers-color-scheme`
- Image strategy for static deploys (Unsplash direct URLs with real photo IDs, inline SVG, CSS-only)
- Full meta/SEO template

---

## Site Types

`references/SITE_TYPES.md` defines 9 archetypes, each with section structure, design guidance, and content density recommendations:

| Type | Purpose |
|------|---------|
| Portfolio / Personal | Showcase work, skills, personality |
| Landing Page / Product | Explain a product, drive one action |
| Restaurant / Food Service | Menu, hours, location, reservation |
| Event / Conference | Date, speakers, schedule, registration |
| Business / Professional | Establish credibility, generate inquiries |
| Blog / Publication | Read articles, subscribe |
| SaaS Dashboard (Preview) | Show the product in use |
| Coming Soon / Pre-Launch | Capture emails before launch |
| Documentation / Technical | Find and read technical information |

---

## File Structure

```
vibe-skills/
├── skills/
│   └── vibe/
│       ├── SKILL.md                  # Core: routing triggers + 4-phase workflow
│       ├── references/
│       │   ├── DESIGN_SYSTEM.md      # Font pairings, palettes, spacing, animation, a11y
│       │   └── SITE_TYPES.md         # 9 site archetypes with guidance
│       └── scripts/                  # Reserved for future automation
├── .gitignore
├── LICENSE
└── README.md
```

---

## Anti-Patterns

| Don't | Do Instead |
|-------|-----------|
| Generate code before deciding on aesthetics | Complete Phase 0 design decision first |
| Default to purple/indigo | Pick a bold, context-appropriate palette |
| Use Inter/Roboto/Arial/system-ui | Pick a distinctive Google Font pairing |
| Use `hero → 3-col features → testimonials → CTA` | Design an unconventional layout for the context |
| Add animation to every element | One orchestrated page-load animation |
| Write placeholder/lorem text | Generate realistic content for the site type |
| Use `<div onClick>` | Use `<button>` for actions, `<a>` for navigation |
| Skip mobile testing | Design mobile-first, verify at 375px |

---

## Requirements

- An AI agent that supports the [Agent Skills](https://agentskills.io) specification
- The [`here-now`](https://github.com/heredotnow/skill) skill installed (`npx skills add heredotnow/skill --skill here-now -g`)
- `curl` and `jq` available on your system

---

## License

MIT License — use, modify, and distribute freely.

---

**Author:** [Ahmad Othman Ammar Adi](https://github.com/OthmanAdi)

## Star History

[![RepoStars](https://repostars.dev/api/embed?repo=OthmanAdi%2Fvibe-skills&theme=copper)](https://repostars.dev/?repos=OthmanAdi%2Fvibe-skills&theme=copper)
