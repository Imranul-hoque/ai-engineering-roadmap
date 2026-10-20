# AI Engineering Roadmap

A visual, 15-level learning map for AI engineering, built as a static Astro site for CampusX. The homepage is the map; `/level/[n]` is the detail page for each level.

## Tech Stack

- **Astro 7** — static, content-driven, minimal client JS
- **Tailwind CSS v4** — utilities + design tokens (`src/styles/tokens.css` mirrored via `@theme inline`)
- **Lucide icons** — inlined at build time from `@iconify-json/lucide`
- **TypeScript** — typed level data
- **Sharp / resvg** — build-time OG share images
- **Vercel** — static hosting

## Architecture

```
AI ENGINEER ROADMAP/level*.txt   (content source of truth)
        ↓ npm run parse
src/data/levels.json             (generated)
        ↓
src/data/levels.ts               (typed)
        ↓
src/pages/index.astro            (roadmap map)
src/pages/level/[n].astro        (level detail)
```

- **Content pipeline:** `scripts/parse-levels.mjs` parses `.txt` files into `levels.json`; `scripts/sign-topics.mjs` signs topic labels. Never edit `levels.json` directly.
- **Design tokens:** `src/styles/tokens.css` holds brand + dark-mode tokens; mirrored into Tailwind in `global.css`.
- **Components:** `src/components/` — UI primitives + roadmap-specific (`RoadmapMap`, `LevelNode`, `ModuleRow`, `ShipItCallout`, etc.).
- **Client JS:** single `src/scripts/app.ts` (~3KB) — progress (localStorage), scroll reveals, analytics.

## Phases

Foundations (0–3) → Retrieval (4) → Agentic (5–6) → Evaluation & Trust (7–8) → Production (9–11) → Frontier & Proof (12–14) → Interview (15)

## Commands

```bash
npm install
npm run dev      # parse + serve
npm run build    # parse + build to ./dist
npm run preview  # serve ./dist
npm run verify   # assert objectives render verbatim
npm run topics   # re-sign topic labels
```

## Deployment

Static output, no adapter. `vercel.json` pins framework preset, build command, output dir, and cache headers for OG images. Set `SITE_URL` for canonicals/sitemap domain.
