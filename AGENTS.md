# Repository Guidelines

## Project Structure & Module Organization
- Root Jekyll site; layouts in `_layouts/`, shared HTML in `_includes/`, data in `_data/`.
- Styles live in `assets/css/` (`tailwind.css` source → `main.css` built). Generated CSS is committed.
- Static assets: `assets/img/`, `assets/fonts/`, PDFs recommended in `assets/docs/`.
- Content pages: `index.html` (landing), auto-generated use-case pages in `use-cases/` via `_data/use_cases.json` + `_layouts/use_case.html`.
- Config: `_config.yml` (plugins, page_gen); Gemfile for Jekyll plugins; `package.json` for Tailwind CLI.

## Build, Test, and Development Commands
- `npm run build:css` — compile Tailwind (`assets/css/tailwind.css`) to `assets/css/main.css` minified.
- `npm run build` — alias for `build:css`.
- `bundle exec jekyll serve --livereload` — local dev server (serves `_site/`, rebuilds on change).
- `bundle exec jekyll build` — production Jekyll build.

## Coding Style & Naming Conventions
- HTML/CSS/JS: 2-space indentation. Keep Tailwind utility classes readable (grouped by layout → spacing → color).
- Data files: JSON with camelCase keys except slug fields (`slug`).
- Paths: link assets via `{{ "/assets/…" | relative_url }}`. Use `use-cases/:slug/` for generated pages.

## Testing Guidelines
- No automated test suite currently. Before pushing, run `npm run build:css` and `bundle exec jekyll build` to catch template or data errors.
- For data-driven pages, validate JSON with `jq . _data/use_cases.json` (ensure trailing commas absent).

## Commit & Pull Request Guidelines
- Commits: concise, imperative subject (e.g., “Add data-driven use case pages”, “Update hero stats”).
- Include what changed and why in the body when non-trivial (e.g., note new data fields or build steps).
- PRs: summarize user-facing changes, list build commands run, and include screenshots for visual updates (desktop + mobile when feasible).

## Security & Configuration Tips
- Keep secrets out of repo; Jekyll site is static—no runtime secrets should be required.
- Pin runtime: prefer Node 22+ (for Tailwind CLI) and Ruby matching `Gemfile` (3.4.8). Consider adding `.nvmrc` / `.ruby-version` for consistency.
