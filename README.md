# ysmouhib.github.io — academic homepage

The academic homepage of **Younes Mouhib** (MSc Mathematics, ETH Zürich).
Clean, white, minimal, research-focused — one self-contained page, no
external requests, no build step, no JavaScript frameworks.

**Live (once deployed):** https://ysmouhib.github.io/

```
index.html                 the whole site (single file: HTML + CSS + inline SVG)
Younes_Mouhib_CV.pdf       the exact CV the "Curriculum Vitae (PDF)" button opens
assets/
  headshot.jpg             round portrait in the hero
  alps.jpg                 photo beside the research section
.nojekyll                  serve files as-is on GitHub Pages (no Jekyll)
.gitignore
```

Sections: **hero · research · publications · teaching · contact**.
"About" and "Research" are now a single minimalist section; the old
"Projects" section has been removed. The Hales–Jewett lattice motif is drawn
as inline SVG in the hero (the two coloured combinatorial lines meeting at a
shared apex) — there is no separate banner image anymore. Prose is
deliberately minimal; the CV carries the detail.

## The CV button

The nav and hero buttons open `Younes_Mouhib_CV.pdf` in the repo root. **This
file is the authoritative, current CV** — it is byte-for-byte the PDF you
provided. If you keep the LaTeX source elsewhere and recompile, copy the new
PDF over this file (same name) so the button always serves the latest.

## Run locally
```bash
python3 -m http.server 8000     # then open http://localhost:8000
```

## Deploy to ysmouhib.github.io — the "root switch"

This is a GitHub **user site**, which is why the "switch for the root" matters:
a user site is served from the **root** of a repository that is named *exactly*
after your account, `ysmouhib.github.io`. Two things have to line up:

1. **The repo name must be exactly `ysmouhib.github.io`** (not "academic-site").
   Only then does GitHub publish it at the root URL `https://ysmouhib.github.io/`.
2. **Pages source must point at the branch root**, i.e. `main` / `/ (root)` —
   this is the actual toggle in the UI.

If your current repo is named `academic-site`, either rename it
(**Settings → General → Repository name → `ysmouhib.github.io`**) or create a
new public repo with that exact name and push there.

First deploy:
```bash
cd path/to/this/folder
git init
git add .
git commit -m "Rebuild academic homepage"
git branch -M main
# create a PUBLIC repo named exactly ysmouhib.github.io at https://github.com/new
git remote add origin https://github.com/ysmouhib/ysmouhib.github.io.git
git push -u origin main
```
(When git asks for a password, use a Personal Access Token: GitHub → Settings →
Developer settings → Personal access tokens → Tokens (classic) → tick `repo`.)

Then flip the switch:

> **Settings → Pages → Build and deployment → Source: “Deploy from a branch” →
> Branch: `main` and folder `/ (root)` → Save.**

The site is live at **https://ysmouhib.github.io/** about a minute later.

Update later:
```bash
git add -A && git commit -m "Update site" && git push
```

### User site vs. project site — don't break the explorer

Your Hales–Jewett Explorer lives at a **project-site** path,
`https://ysmouhib.github.io/hales-jewett-explorer/`, served from its **own**
`hales-jewett-explorer` repo. It is completely independent of this one:

- This repo (`ysmouhib.github.io`) controls only the **root** `/`.
- The `hales-jewett-explorer` repo controls the `/hales-jewett-explorer/` subpath.

So deploying this homepage does **not** touch or override the explorer — they
coexist. For that reason this site ships **no catch-all `404.html` redirect**
(one would risk hijacking the explorer's URLs) and **no `CNAME`** (no custom
domain — you're using the default `ysmouhib.github.io`). Keep `.nojekyll` so
GitHub serves the files as-is.
