# AGENTS.md

Source of the evilcat.games website — a static Hugo site for Evil Cat Games.

> This repository is **public**. Never commit secrets, tokens, personal data,
> local machine paths or private notes — in code, content, commit messages or
> this file.

## Stack

- Hugo **extended 0.151.0** (pinned in `.github/workflows/hugo.yml`).
- Theme: `hugo-coder`, a git submodule in `themes/coder`.
- Deploy: GitHub Actions → GitHub Pages on every push to `main`.
  The custom domain `evilcat.games` is configured in the repository's Pages
  settings; CI passes the real URL via `--baseURL`.

## Commands

```bash
git submodule update --init --recursive   # fetch the theme
hugo server                               # local preview at http://localhost:1313
hugo --minify                             # production build into ./public
```

## Layout

- `hugo.toml` — site config, menu, custom CSS list and home page content:
  `params.games` (one `[[params.games]]` block per game), `params.about`,
  `params.contactEmail`.
- `layouts/_partials/` — overrides of theme partials (home page, footer).
  `home.html` composes `home/avatar`, `home/games`, `home/studio` (About),
  `home/contact`; `home/section-title` renders a section heading.
- `assets/css/custom.css` — all custom styles (loaded via `params.customCSS`).
  The theme uses `1rem = 10px`.
- `assets/images/games/` — game icons; Hugo resizes them to WebP/PNG at build time.
- `content/legal/` — Privacy Policy and Terms & Conditions for the Guess Word app.
- `static/images/` — images served as-is; store badges are in `static/images/badges/`.

## Rules

- Do not edit `themes/coder`. Override a theme template by copying it into
  `layouts/` with the same relative path.
- Keep the URLs `/legal/privacy/` and `/legal/terms/` stable — store listings
  link to them. Change legal texts only when explicitly asked.
- `public/` and `resources/_gen/` are build output; never commit them.
- Do not change the deploy workflow, `baseURL` or domain setup unless asked.
- GitHub Actions in workflows are pinned by full commit SHA with the version
  in a comment. Keep it that way when updating them.
- Pushing to `main` deploys to production. Build locally with `hugo` and check
  for errors before proposing a push.
- Keep the site dependency-free: no npm packages or external JS without a reason.
- Do not modify store badge artwork (colours, proportions, elements) and keep
  clear space around a badge of at least 1/4 of its height.
- Serve images, fonts and badges from this repository, not from third-party hosts.
