# Portfolio

The source of my personal site: **<https://portfolio-production-f8b6.up.railway.app/>**

A single static page — my CV, and the projects it points at, with the results
stated in full.

## What's here

```
index.html            the whole page
assets/css/style.css  hand-written CSS, dark and light themes
assets/js/main.js     ~200 lines of vanilla JS, no dependencies
404.html              fallback page
robots.txt            crawl policy
sitemap.xml           one URL, but search engines like being told
.nojekyll             serve the files as they are, no Jekyll build
```

No framework, no build step, no bundler, no tracking. The page is three files
and a couple of Google Fonts; open `index.html` in a browser and it works.

## The projects it links to

| Project | What it is | Live |
|---|---|---|
| [opslab](https://github.com/pr1317/opslab) | Operations analytics for BFSI back-office processes — process mining, SPC, SLA survival analysis and a Power BI model linter, on the standard library alone | — |
| [handwritten-digit-recognition](https://github.com/pr1317/handwritten-digit-recognition) | 98.48% on MNIST; the finding is that deskewing beats model choice | [draw a digit](https://pr1317.github.io/handwritten-digit-recognition/) |
| [customer-churn-analytics](https://github.com/pr1317/customer-churn-analytics) | ROC-AUC 0.846, and whether acting on the prediction pays for itself | [try the scorer](https://pr1317.github.io/customer-churn-analytics/) |
| [smart-traffic-management](https://github.com/pr1317/smart-traffic-management) | YOLOv4-tiny and a centroid tracker turning a highway camera into telemetry | [watch it run](https://pr1317.github.io/smart-traffic-management/) |

## Publishing it

Deployed on Railway from `main`. There is no build step: Railpack detects the
static site and serves the repository root with Caddy, so a push to `main`
redeploys it.

It is equally happy on GitHub Pages (**Settings → Pages → Deploy from a branch
→ `main` / `/ (root)`**); every path in the page is relative, so it works at a
domain root or under a `/Portfolio/` prefix without changes.

## Working on it locally

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

Opening `index.html` straight off the filesystem works too; the local server
only matters if you want paths to behave exactly as they do in production.

## Notes on the build

- **Responsive** from 320px up. Fluid type via `clamp()`, grids via
  `auto-fit`/breakpoints — no fixed widths anywhere, and no horizontal scroll
  at any viewport.
- **Themes.** Dark by default; the toggle persists a choice in `localStorage`
  and every read and write is wrapped, so private-browsing mode can't break it.
  An inline script in `<head>` applies the stored theme before first paint, so
  there's no flash of the wrong colours.
- **Degrades safely.** Section content is visible by default and only hidden
  for the entrance animation once the boot script has run — a blocked or failed
  `main.js` can never leave the page blank.
- **`prefers-reduced-motion`** is honoured: the aurora stops drifting, the
  counters stop counting, and the reveal animations resolve immediately.
- **Accessibility.** Skip link, labelled controls, `aria-expanded` on the menu,
  visible focus rings, and a keyboard-dismissable mobile menu.
- **Print** produces a clean CV-style document, with link targets expanded.

## A note on the numbers

Every figure on the page traces to a source: the workplace metrics come from my
CV, and each project metric is the one its own repository measures and can
defend. Where a rounder number was available I used the defensible one instead —
the traffic project, for example, reports near-field recall rather than an
overall "detection accuracy", because the clip it runs on ships without labels
and there is nothing to measure such a figure against.
