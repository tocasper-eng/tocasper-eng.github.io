# CLAUDE.md

Guidance for Claude Code when working in this repository.

## What this is

Casper's personal portfolio website, served by **GitHub Pages** at
**https://tocasper-eng.github.io**. It is a GitHub *user site*, so the repo is
named exactly `tocasper-eng.github.io` and is published from the **root** of
the `main` branch.

Casper is an **ERP / SAP developer** (T-SQL, ABAP, Python/FastAPI). The site
content reflects that focus.

## Stack

- **Plain HTML + CSS — no build step, no dependencies, no framework.**
- A small inline `<script>` in `index.html` powers the dark/light theme toggle.
- `.nojekyll` is present so GitHub Pages serves the files as-is (no Jekyll).

## Files

| File | Purpose |
|------|---------|
| `index.html` | All page content and structure (single page, anchor-nav sections). |
| `styles.css` | All styling. Theming via CSS custom properties on `:root` / `:root[data-theme="light"]`. |
| `.nojekyll` | Disable Jekyll processing. |
| `README.md` | Human-facing project readme. |
| `.gitignore` | Excludes `.claude/` and `.DS_Store`. |

## Conventions

- **No frameworks or build tooling.** Keep it dependency-free. Don't introduce
  npm, bundlers, Tailwind, or Jekyll without being asked.
- **Theming:** add new colors as CSS variables in *both* the `:root` (dark) and
  `:root[data-theme="light"]` blocks so light mode stays consistent.
- **Sections** in `index.html` are numbered (`01.`, `02.`, …) and linked from
  the nav by `id`. Keep the numbering and nav links in sync when adding/removing
  sections.
- **Projects** are hand-written `<article class="card">` blocks. Each links to a
  real repo under `https://github.com/tocasper-eng`.
- Do **not** commit the `.claude/` directory (it's gitignored).

## Deploying

GitHub Pages auto-deploys on every push to `main`. The flow is:

```sh
git add -A
git commit -m "..."
git push origin main
```

Then the Pages build runs (~30–60s). To verify it finished and the site is
live:

```sh
gh api repos/tocasper-eng/tocasper-eng.github.io/pages/builds/latest   # status: "built"
curl -s -o /dev/null -w "%{http_code}" https://tocasper-eng.github.io/  # expect 200
```

There is a `deploy` skill that automates this commit → push → verify loop.

## Local preview

```sh
python -m http.server 8000   # then open http://localhost:8000
```
