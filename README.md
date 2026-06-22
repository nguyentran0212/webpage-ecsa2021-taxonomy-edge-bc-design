# webpage-ecsa2021-taxonomy-edge-bc-design

Public landing page for the ECSA 2021 paper "Taxonomy of Edge Blockchain Network Designs"
(Tran & Babar, European Conference on Software Architecture, Springer LNCS, pp. 172–180, 2021).

Hosted via GitHub Pages at: `https://nguyentran0212.github.io/webpage-ecsa2021-taxonomy-edge-bc-design/`

## Layout

- `index.md` — page content (Markdown, processed by Jekyll)
- `_layouts/default.html` — base HTML template
- `assets/css/style.css` — single stylesheet
- `assets/pdf/main.pdf` — downloadable copy of the paper
- `assets/figures/*.png` — converted from the paper's `figures/` (taxonomy diagram, reference infrastructure, read/write availability, update availability)
- `_config.yml` — site config (`baseurl` set to `/webpage-ecsa2021-taxonomy-edge-bc-design`)
- `Gemfile` — Jekyll dependency pinned to `~> 4.3`

## Local preview

Requires Ruby + Bundler.

```bash
bundle install
bundle exec jekyll serve --host 127.0.0.1 --port 4004
# → http://127.0.0.1:4004/webpage-ecsa2021-taxonomy-edge-bc-design/
```

## Editing content

The page is one Markdown file. Sections (in order):
Hero → TL;DR → At a glance → Research method → Taxonomy → Availability findings → Abstract → Cite.

`baseurl` in `_config.yml` is set to `/webpage-ecsa2021-taxonomy-edge-bc-design`. If you ever move
this to a custom domain or root, set `baseurl: ""` and `url: "https://yourdomain.com"`.