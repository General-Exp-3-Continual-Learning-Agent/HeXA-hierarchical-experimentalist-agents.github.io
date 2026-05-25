# HeXA Project Page

Static site for the **Hierarchical Experimentalist Agents** paper, designed to be deployed on GitHub Pages with zero build step.

## Files

```
.
├── index.html      # All content lives here
├── style.css       # All styling
├── assets/         # (create this) Put teaser.png, paper.pdf, etc. here
└── README.md
```

## Deploy to GitHub Pages — 3 steps

1. **Push these files to your repo** (root of the `main` branch is easiest):
   ```bash
   git add index.html style.css README.md
   git commit -m "Initial project page"
   git push origin main
   ```

2. **Enable Pages**: Repo → *Settings* → *Pages* → under *Build and deployment*, set **Source** to *Deploy from a branch*, **Branch** to `main`, **Folder** to `/ (root)`. Save.

3. **Wait ~30 seconds**. Your site will be live at:
   ```
   https://<your-username>.github.io/<your-repo-name>/
   ```
   (For a user/org site at `<username>.github.io`, the repo must be named exactly that — and it lives at the root URL.)

## Customize — where to edit what

Everything you need to change is in `index.html`. Search for these landmarks:

| You want to change…              | Find this in `index.html`                                       |
|----------------------------------|------------------------------------------------------------------|
| Paper / arXiv / Code / Data URLs | The `<nav class="hero__cta">` block — replace each `href="#"`   |
| Author names & affiliations      | The `<div class="authors">` and `<div class="affiliations">`    |
| Conference / venue badge         | The `.hero__eyebrow` span                                       |
| Abstract text                    | `<section id="abstract">`                                        |
| Headline statistics              | `<div class="stats">` — four `.stat` blocks                     |
| Method pillars                   | `<div class="method__pillars">` — three `.pillar` articles      |
| InterPhyre bullets               | `<ul class="features">`                                         |
| BibTeX                           | The `<pre><code id="bibtex-code">` block                        |
| Color accent (orange → ?)        | `style.css` — change `--accent` and `--accent-soft` at the top  |
| Display font                     | `style.css` — change the `--serif` variable and the Google Fonts `<link>` in `<head>` |

## Add your teaser figure

1. Create an `assets/` folder and drop in your `teaser.png` (export Figure 1 from the paper as PNG, ~1600px wide).
2. In `index.html`, replace the entire `<div class="teaser__placeholder">…</div>` SVG block with:
   ```html
   <img src="assets/teaser.png" alt="HeXA framework overview" style="width:100%; display:block; border:1px solid var(--rule); border-radius:6px;">
   ```

## Add the PDF

Drop your paper PDF at `assets/paper.pdf` and update the Paper button's `href`:
```html
<a class="btn btn--primary" href="assets/paper.pdf" target="_blank" rel="noopener">
```

## Optional polish

- **Favicon**: add `<link rel="icon" href="assets/favicon.png">` inside `<head>`.
- **Custom domain**: drop a `CNAME` file at the repo root with your domain name.
- **Analytics-free, JS-free fallback**: the page already works with JS disabled — only the BibTeX *Copy* button needs JS.
- **Dark mode**: not included by default to keep the file simple; happy to add it if you want.

## Local preview

You don't strictly need a server — opening `index.html` in your browser works — but for the cleanest preview:
```bash
python3 -m http.server 8000
# then open http://localhost:8000
```