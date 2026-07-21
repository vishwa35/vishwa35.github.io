---
name: hugo-site
description: Conventions and workflows for managing vishwashah.com, a Hugo static site. Use this whenever adding/editing blog posts or pages, changing config.toml, working with the hugo-theme-codex theme, adding layouts, or building/previewing/deploying the site.
---

# Managing this Hugo site

This repo is a Hugo static site (config in `config.toml`) deployed to GitHub Pages as `vishwashah.com`. Most edits are markdown content changes; occasionally there are theme/layout or config changes.

## Structure

- `content/` — all markdown content, organized by section. Each section maps to a menu entry in `config.toml` (`[[menu.main]]`).
  - `content/blog/medium/<slug>/index.md` — blog posts, one per directory (page bundles), with local `images/` subfolders alongside `index.md`.
  - `content/portfolio/`, `content/itineraries/`, `content/reading-list/`, `content/ongoing-projects/`, `content/resume/` — single pages or small sections, mostly flat `.md` files or `index.md` bundles.
  - `content/ccoptimizer/index.md` — a page that renders through a fully custom layout (`layouts/ccoptimizer/single.html`), which is a self-contained HTML/CSS/JS document, not a themed page. Use this same pattern (custom `type`/`layout` front matter + matching `layouts/<type>/single.html`) for any other standalone HTML tool pages.
- `layouts/` — repo-level template overrides (`static-page/`, `resume/`, `ccoptimizer/`). These take precedence over the theme's templates of the same name.
- `themes/hugo-theme-codex/` — a git submodule (`vishwa35/hugo-theme-codex`, branch `vish/currenthugo-theme-codex`). Theme changes belong in that submodule's repo, not here, unless doing a local override via `layouts/`.
- `archetypes/default.md` — front matter template used by `hugo new`.
- `static/` — served as-is at site root (currently just compiled CSS/LESS).
- `data/`, `assets/`, `resources/` — Hugo data files, pipeline assets, and generated cache (don't hand-edit `resources/_gen`).

## Front matter conventions

Blog posts (`content/blog/medium/**/index.md`) typically include:

```yaml
---
title: "Post Title"
author: "Vishwa Shah"
date: 2019-08-28T00:13:52.051Z
lastmod: 2020-08-08T18:01:08-04:00
description: ""
tags: [tag1, tag2]
keywords: [seo, keywords, here]
subtitle: "One-line summary shown in listings."
image: "images/1.jpeg"
images:
 - "images/1.jpeg"
aliases:
    - "/old-medium-slug-id"
---
```

- `aliases` preserves old URLs (most posts were migrated from Medium/LinkedIn) — always keep the original slug/ID as an alias when importing external content.
- `image`/`images` point at files in the post's own `images/` bundle directory, referenced in markdown as `![image](images/1.jpeg)`.
- Custom pages (like `ccoptimizer`) use a minimal front matter: `title`, `draft`, `layout`, `type`, `toc`.
- Taxonomies available: `categories`, `tags`, `projTags` (see `[taxonomies]` in `config.toml`).

## Config

`config.toml` holds site title, theme name, social links (`[params]`), nav (`[[menu.main]]`), and markdown rendering options. Notably:
- `markup.goldmark.renderer.unsafe = true` — raw HTML in markdown is allowed.
- `markup.highlight.codeFences = false` — syntax highlighting is handled by PrismJS in the theme, not Hugo's built-in highlighter. Don't re-enable `codeFences` without also removing the PrismJS include in `layouts/blog/single.html` (theme).
- Adding a new top-level section to the nav means adding a `[[menu.main]]` entry here.

## Local development

```bash
hugo server -t hugo-theme-codex
```

Make sure submodules are checked out first (`git submodule update --init --recursive`) or the theme will be missing.

To build a production copy locally:

```bash
hugo -t hugo-theme-codex
```

## Deployment

GitHub Actions workflow `hugo.yml` handles all deployment on push to `master`:
- Installs Hugo + Dart Sass, checks out submodules, builds the site with Hugo.
- Uploads the built artifact and deploys to GitHub Pages via the native `actions/deploy-pages` flow.
- Runs on push to `master` and can be triggered manually via the Actions tab.

This is the only active deployment method; manual `deploy.sh` and the older `deploy.yml` workflow have been removed.

## Adding content

- New blog post: create `content/blog/medium/<slug>/index.md` (plus an `images/` subfolder if it has images), following the front matter shape above.
- New standalone section/page: add a `[[menu.main]]` entry in `config.toml` if it should appear in nav, then add the content file(s) under `content/<section>/`.
- New fully-custom HTML page (like ccoptimizer): add `content/<name>/index.md` with `layout`/`type` set to `<name>`, and `layouts/<name>/single.html` containing the full custom HTML/CSS/JS.
