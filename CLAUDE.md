# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

ScholarOS-based academic website built with **Astro 5**, **Vue 3**, and **Tailwind CSS v4**. Uses pnpm (v9) as package manager and Node 22 (.nvmrc).

## Commands

```bash
pnpm dev              # Dev server at localhost:4321
pnpm build            # Production build
pnpm preview          # Preview production build
pnpm lint             # ESLint + Prettier check
pnpm lint:fix         # Auto-fix lint issues
pnpm format           # Prettier formatting
pnpm check            # Astro type checking
pnpm sync:feeds       # Sync external RSS feeds
pnpm sync:scholar     # Sync Google Scholar publications
pnpm render:cv        # Generate CV PDF (requires Python 3.12 + RenderCV)
pnpm generate:keywords # Auto-generate SEO keywords
```

## Architecture

**Island Architecture:** Pages are static Astro HTML by default. Vue components hydrate only where interactivity is needed (search, theme toggle, filters, forms).

**Key directories:**
- `config/` — YAML site configuration (site.yml, cv.yml, research.yml, feeds.yml, scholar.yml, cms.yml). Most customization happens here, not in code.
- `src/components/astro/` — Static zero-JS components
- `src/components/vue/` — Interactive islands (Search, ThemeToggle, PublicationFilter, forms)
- `src/content/` — Markdown content collections: people, publications, posts, announcements, projects, positions, talks
- `src/layouts/` — Page templates (BaseLayout, PageLayout, ListLayout, MarkdownLayout)
- `src/lib/` — Utilities (config loader, colors, search indexing, types, rehype plugins)
- `src/pages/` — File-based routing
- `scripts/` — Automation scripts (TypeScript for feeds/SEO/migration, Python for scholar/cv)

**Content collections** are defined with Zod schemas in `src/content.config.ts`. Each collection has strict typing.

**Path aliases** (tsconfig.json): `@/*` → src/*, `@components/*`, `@layouts/*`, `@lib/*`, `@content/*`, `@config/*`.

## Code Style

- Prettier: 2-space indent, single quotes, trailing commas, 120 char width
- ESLint flat config with astro and vue plugins
- Plugins: prettier-plugin-astro, prettier-plugin-tailwindcss

## Deployment

Primary: GitHub Pages via `.github/workflows/deploy.yml` (builds Astro + renders CV PDF). Also configured for Netlify (netlify.toml) and Cloudflare.

## Site Modes

Supports two modes configured in `config/site.yml`: **personal** (individual researcher) and **lab** (research group). This affects layout and available features like team directory.
