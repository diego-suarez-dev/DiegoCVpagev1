# Systems Under Tension — CV site

Static one-page CV for Diego Suarez. No build step, no framework, no runtime
dependencies beyond Google Fonts.

## Files

- `index.html` — the entire page. **All content lives here** — text, roles,
  bullets, tags, education, footer.
- `styles.css` — visual system (colours, type, layout).
- `Diego_Suarez_CV.pdf` — the file the three "Download CV" buttons serve.
- `.gitignore`, `README.md` — repo housekeeping.

## How to update content

There is **one path**:

1. Open `index.html` in any editor.
2. Edit the text in place.
3. Save.

That's it. To preview, double-click `index.html` (it opens in your browser).

### Updating the downloadable CV

Replace `Diego_Suarez_CV.pdf` with a new file using the **same name**. The
download buttons reference the filename directly, so they'll pick up the
new file automatically.

### Adding a new role

In `index.html`, find the `<section id="experience">` block. Each role is an
`<article class="role">…</article>` — copy one, paste it in chronological
position, edit the employer / dates / title / bullets / tags.

Tags get an amber treatment automatically when their text matches
`safety`, `nuclear`, or `radiation` (case-insensitive) — this is a CSS
class, so add `class="tag amber"` instead of just `class="tag"` for any
new tag you want flagged.

## Maintenance notes

### Stylesheet versioning
The stylesheet link in `index.html` uses a version parameter (e.g., `styles.css?v=20260503`). This is intentional to prevent browsers from serving a stale cached version of the CSS after updates. Always increment this version when making major visual changes.

### Dependencies
- **Google Fonts:** The site loads "Inter Tight" and "JetBrains Mono" from Google Fonts at runtime.
- **No Build Step:** This remains a plain HTML/CSS/JS site. Do not add bundlers or frameworks.

### Section Syncing
If you change section IDs or add new sections:
1. Update the `id` attribute on the `<section>`.
2. Update the `href` and `data-jump` attributes in the `<nav>` links.
3. Update the `ids` array in the `<script>` at the bottom of `index.html` to ensure the scroll-spy (IntersectionObserver) continues to track the active section correctly.

## How to commit changes

```bash
cd "/Users/diegosuarez/Documents/Diego CV/website"
git add -u
git commit -m "describe what changed"
```

## Deferred — when you're ready to publish

The repo is local-only for now. To put it on the web:

1. **Push to GitHub.** `gh repo create diego-cv --public --source=. --push`
   (or pick another name). Public is required for free GitHub Pages; private
   needs GitHub Pro.
2. **Enable GitHub Pages.** In the repo on github.com: Settings → Pages →
   Source: "Deploy from a branch", Branch: `main`, Folder: `/ (root)`. The
   site goes live at `https://<your-username>.github.io/diego-cv/` within
   ~1 minute.
3. **Custom domain (optional).** Once you own a domain, add a `CNAME` file
   to this folder containing the domain (one line, no protocol), then point
   the domain's DNS at `<your-username>.github.io` and enable "Enforce HTTPS"
   in GitHub Pages settings.

After that, every `git push` redeploys the site automatically.

## Provenance

Visual design ported from a Claude Design prototype (`Systems Under Tension.html`,
calmer revision). The prototype used React via CDN and Babel-in-the-browser;
this implementation strips that runtime layer and renders the same design as
plain HTML.
