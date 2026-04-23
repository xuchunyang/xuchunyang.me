# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Personal website for xuchunyang (徐春阳). Built with Astro, deployed as a fully static site to Cloudflare Pages. No SSR, no server functions — `output: 'static'` throughout.

## Commands

```sh
pnpm install       # install deps
pnpm dev           # dev server at http://localhost:4321
pnpm build         # build to dist/
pnpm preview       # preview the built output
```

Package manager is `pnpm` (not npm or yarn).

## Architecture

The site uses Astro's Content Collections for blog posts:

- `src/content.config.ts` — defines the `blog` collection schema (title, description, pubDate, updatedDate, tags, draft)
- `src/content/blog/*.md` — each file is a blog post; filename becomes the URL slug (`foo.md` → `/blog/foo/`)
- `src/pages/blog/[...slug].astro` — dynamic route that renders individual posts; filters out `draft: true` entries
- `src/pages/index.astro` — homepage, shows 8 most recent non-draft posts
- `src/layouts/Base.astro` — single shared layout wrapping all pages; accepts `title` and `description` props for `<head>`
- `src/pages/rss.xml.js` — RSS feed generated from all non-draft posts

## Writing blog posts

Add a `.md` file to `src/content/blog/` with this frontmatter:

```yaml
---
title: "标题"
description: "简介（可选）"
pubDate: 2026-04-23
updatedDate: 2026-04-24   # optional
tags: ["linux", "pi"]     # optional
draft: false              # optional, omit to default false
---
```

## Styling

All styles live in `src/styles/global.css` — no CSS framework, no component-scoped styles. Uses CSS custom properties (`--bg`, `--fg`, `--muted`, `--accent`, `--rule`, `--code-bg`) for light/dark theming via `prefers-color-scheme`. Layout is monospace-font, single-column, max 72ch wide.

Code syntax highlighting uses Shiki (built into Astro) with `github-light` / `github-dark` themes.

## Deployment

Push to GitHub → Cloudflare Pages auto-deploys. Build command: `pnpm build`, output: `dist/`, `NODE_VERSION=20`.
