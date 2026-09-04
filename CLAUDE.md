# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A [Slidev](https://sli.dev/) presentation deck — "Carreira Tech / SI 2026" (a career talk for an Information Systems audience, content in Portuguese). It started from the Slidev starter template; `slides.md` is still largely the template content and is the piece to actually rewrite.

## Commands

- `npm install` — install (pnpm also works; `pnpm-workspace.yaml` allowlists the `playwright-chromium` build script needed for exports)
- `npm run dev` — dev server with live reload at http://localhost:3030 (`slidev --open`)
- `npm run build` — static SPA build into `dist/` (what Netlify and Vercel deploy)
- `npm run export` — render the deck to PDF/PNG/PPTX (needs `playwright-chromium`)
- Single slide: append `?print` or navigate to `/<slide-number>` in dev; there is no test suite

## Structure

- `slides.md` — the deck. First `---` block is headmatter (theme `seriph`, `transition`, `duration`, etc.); every subsequent `---` separates a slide, and a per-slide `---`-fenced block at the top of a slide sets that slide's frontmatter (layout, transition, class).
- `components/` — Vue SFCs auto-imported by name into any slide (e.g. `<Counter />`). No import statement needed.
- `snippets/` — external code pulled into slides via Slidev's `<<< @/snippets/external.ts#region` syntax so examples stay runnable.
- `pages/` — extra Markdown included from `slides.md` with `---\nsrc: ./pages/imported-slides.md\n---`.
- `netlify.toml` / `vercel.json` — both publish `dist/` with SPA rewrites to `/index.html`; Netlify pins Node 24.

## Notes

- Styling is UnoCSS utility classes (including attributify, e.g. `border="~ main"`) available directly in slide Markdown and components.
- The last HTML comment (`<!-- ... -->`) in a slide becomes presenter notes.
