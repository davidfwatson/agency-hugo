# agency-hugo

Hugo port of the [Start Bootstrap "Agency"](https://startbootstrap.com/theme/agency) one-page theme, derived from the [Jekyll port](https://github.com/raviriley/agency-jekyll-theme) by Ravi Riley. Same look, same data-driven customization surface, no Ruby/Bundler.

- **Bootstrap 4** (CSS + JS) and **FontAwesome 5 free** loaded from jsDelivr CDN with SRI hashes — no vendored copies of upstream libraries
- **Data-driven content** via `data/sitetext.yml`, `data/navigation.yml`, `data/style.yml` (locale-keyed, ports the Jekyll structure verbatim)
- **Portfolio** as a Hugo content section (`content/portfolio/*.md`), rendered as a homepage grid plus per-project modals
- **Sass** compiled via Hugo Pipes (no Node toolchain)

Requires Hugo extended **0.128.0+**.

## Use standalone

```bash
hugo server
```

Opens at `http://localhost:1313/`. Edit `hugo.toml` (site title, email, optional Google Analytics ID, optional Formspree form), then edit `data/sitetext.yml` for all section copy.

## Use as a theme in another Hugo site

Set this up once in the consuming site (e.g. `james4council`):

### Option A — git submodule (simplest)

```bash
cd james4council
git submodule add https://github.com/davidfwatson/agency-hugo themes/agency-hugo
```

Then in `james4council/hugo.toml`:

```toml
theme = "agency-hugo"
title = "James for Council"
# ...everything else (params, etc.)
```

### Option B — Hugo module

```bash
cd james4council
hugo mod init github.com/your-user/james4council
hugo mod get github.com/davidfwatson/agency-hugo
```

Then in `james4council/hugo.toml`:

```toml
[module]
  [[module.imports]]
    path = "github.com/davidfwatson/agency-hugo"
```

### What the consuming site provides

- `hugo.toml` — site identity (title, baseURL, params.email, params.locale, etc.)
- `data/sitetext.yml` — your section copy (overlays the theme's default; missing keys fall back to the theme's defaults)
- `data/navigation.yml` — your nav links
- `content/_index.md` — empty file; the homepage layout assembles the sections
- `content/portfolio/*.md` — one file per portfolio project (optional)
- `content/legal.md` — privacy / legal page (optional; uses the theme's default if absent)
- `static/img/` — your own images (overrides theme defaults at the same paths)

You do **not** copy `layouts/`, `assets/scss/`, or shortcodes — those come from the theme.

## Customizing

- **Section copy**: `data/sitetext.yml`. The file is locale-keyed (`en`, `es`, `de`); change `params.locale` in `hugo.toml` to switch.
- **Nav links**: `data/navigation.yml`. Each entry is either `{title, section: "anchor-id"}` for in-page anchor links or `{title, url: "https://..."}` for external links.
- **Colors / fonts**: edit `assets/scss/agency.scss` (the Jekyll original threaded colors through `data/style.yml` via Liquid; Hugo Pipes doesn't template SCSS, so edit the SCSS directly or refactor to use `resources.ExecuteAsTemplate`).
- **Google Analytics**: set `params.analytics_google = "G-XXXXXXX"` in `hugo.toml`.
- **Contact form**: set `params.email` (sent via Formspree by default) or `params.formspree_form_path = "f/your_id"`.
- **Logo**: set `[params.logo] path = "/img/logo.png", height = 60`. Without one the site title shows in the navbar.

## Project structure

```
agency-hugo/
├── hugo.toml                # site config (replace when used as a theme)
├── theme.toml               # theme metadata
├── archetypes/              # (intentionally empty for now)
├── assets/scss/             # Sass partials — agency.scss is the entry
├── content/
│   ├── _index.md            # triggers the homepage assembly
│   ├── legal.md             # privacy policy
│   └── portfolio/           # one md per project
├── data/                    # navigation / sitetext / style (locale-keyed)
├── layouts/
│   ├── 404.html
│   ├── _default/            # baseof, single, list fallbacks
│   ├── index.html           # one-page assembly: navheader + 6 sections
│   ├── partials/            # one partial per section
│   └── shortcodes/          # site-title, site-email, if-analytics
└── static/
    ├── img/                 # demo images (override in the consuming site)
    └── js/                  # agency-specific JS (3 files)
```

## Credits

- Original Bootstrap theme: [Start Bootstrap — Agency](https://startbootstrap.com/theme/agency)
- Jekyll port: [raviriley/agency-jekyll-theme](https://github.com/raviriley/agency-jekyll-theme) (MIT)
- Hugo port: this repo (MIT)

## License

MIT. See `LICENSE`.
