# AGENTS.md

## Stack

- **Jekyll 4** static site — no Node.js, no npm, no build step beyond `jekyll build`
- **Hosting**: GitHub Pages at `sundana.github.io` (remote: `origin https://github.com/sundana/sundana.github.io`)
- **Styling**: vanilla CSS in `styles/style.css` — no Tailwind, no preprocessor
- **Templating**: Liquid via Jekyll layouts
- **Plugins**: `jekyll-feed`, `jekyll-seo-tag`

## Commands

```sh
bundle exec jekyll build    # build to _site/
bundle exec jekyll serve    # dev server at http://localhost:4000
```

Always use `bundle exec` — do not invoke `jekyll` directly.

## Architecture

- **Layouts**: `_layouts/default.html` (base wrapper), `_layouts/post.html` (blog posts with article semantics), `_layouts/project.html` (project pages)
- **Pages**: root `.html` files (`index.html`, `blog.html`, `404.html`) and `projects/*.html`
- **Posts**: `_posts/YYYY-MM-DD-slug.md` with front matter `layout: post`
- **Projects**: `_projects/*.html` or `.md` — Jekyll collection, same pattern as posts. Add a file with front matter (`title`, `desc`, optional `external`/`external_url`/`subtitle`), it auto-appears on homepage and `/projects/`.
- **Config**: `_config.yml` — `url` must be `"https://sundana.github.io"` for correct SEO, feeds, and canonicals

### Directory map

| Path | Purpose |
|---|---|
| `_layouts/` | Liquid layouts |
| `_posts/` | Blog posts (date-prefixed `.md`) |
| `_projects/` | Project pages (Jekyll collection, `.html` or `.md`) |
| `_research/` | Research pages (Jekyll collection, `.html` or `.md`) |
| `projects/` | Generated project index page (`projects/index.html`) |
| `research/` | Generated research index page (`research/index.html`) |
| `styles/` | Single `style.css` with all styles |
| `img/` | Images |
| `_site/` | Build output — **gitignored, never edit directly** |

## Conventions

- Blog posts use `layout: post`, not `layout: default`
- Project pages go in `projects/` as standalone HTML, linked from the projects index and homepage
- CSS uses custom properties defined in `:root` — use them, don't hardcode colors
- No inline styles — everything goes in `styles/style.css`
- The `_config.yml` `exclude` list is for stale Astro/migration leftovers — it's fine as-is

## Gotchas

- The site was migrated from Astro. Stale exclude entries in `_config.yml` (e.g. `src/`, `dist/`, `.astro/`) are intentional and harmless.
- There is no CI/CD — pushes to `main` deploy via GitHub Pages automatically.
- Jekyll auto-generates post URLs as `/YYYY/MM/DD/slug.html` — link accordingly.
