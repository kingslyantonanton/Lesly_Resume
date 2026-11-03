# Lesly Anton — SAP Consultant Portfolio

A single-page, static personal portfolio. No build step, no framework, no package manager, no backend.

## Files

```
.
├── index.html            # Entire site: HTML + CSS + vanilla JS (self-contained)
├── resume.pdf            # Downloaded by the "Download Resume" button
├── assets/
│   └── profile.jpg       # Hero profile photo
├── vercel.json           # Optional Vercel settings (clean URLs)
├── .gitignore
└── README.md
```

`index.html` has exactly one external dependency: Google Fonts (Inter). If that fails to load, it falls back to the system sans-serif stack. Everything else — icons, styles, scripts, favicon — is inline or local.

## Run locally

Any static file server works. From this folder:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000`. Opening `index.html` directly with `file://` also works, but a local server is closer to how Vercel will serve it.

## Deploy with GitHub + Vercel

1. Create a new GitHub repository (e.g. `lesly-anton-portfolio`).
2. Put **all the files above at the repository root** — `index.html` must be at the root, not inside a subfolder.
   ```bash
   git init
   git add .
   git commit -m "Add SAP consultant portfolio"
   git branch -M main
   git remote add origin https://github.com/<your-username>/lesly-anton-portfolio.git
   git push -u origin main
   ```
3. Go to [vercel.com/new](https://vercel.com/new) → **Import** the GitHub repo.
4. Framework Preset: **Other**. Leave **Build Command** empty and **Output Directory** empty (defaults to the repo root). No environment variables are needed.
5. Click **Deploy**. Vercel serves `index.html` at `/` and `resume.pdf` at `/resume.pdf`. Every push to `main` redeploys automatically.

`vercel.json` only enables clean URLs; the site deploys fine without it.

## Customising

| What | Where |
| --- | --- |
| Profile photo | Replace `assets/profile.jpg` with another **square** photo, keeping the same filename. If you rename it, update the `<img class="portrait__img" src="...">` in the Hero section. |
| Resume | Replace `resume.pdf` with his official PDF, keeping the same filename. The button is `<a href="resume.pdf" download>` in the Hero. |
| Contact details | Search `index.html` for `leslyantonofficial@gmail.com`, `+1-267-678-9919`, and `linkedin.com/in/leslyanton`. Also update the Person JSON-LD in `<head>`. |
| Certifications | Search for `CERTIFICATIONS PLACEHOLDER` — there is an HTML comment in the Education section marking where to add a card. The resume listed no certifications, so none were invented. |
| Accent colour | The `--accent*` variables at the top of the `<style>` block. There is one light palette and one dark palette (`[data-theme="dark"]`). |
| Default theme | By default the site follows the visitor's OS setting, then remembers their choice once they click the sun/moon button (stored in `localStorage` under `la-theme`). To force light as the default, change the boot script in `<head>` to always set `t = 'light'`. |
| SEO / social preview | Edit the `<title>`, `<meta name="description">`, Open Graph tags, and JSON-LD in `<head>`. Add an `og:image` with a full deployed URL once the site has a domain. |

## Important note about `resume.pdf`

The attached resume was supplied as **pasted text**, not as a DOCX file, so `resume.pdf` here is a clean 2-page PDF **rebuilt from that text** — it is not a conversion of his original document. It contains only facts from the pasted resume, including all roles, bullets, projects, skills, education, and languages. One tense was updated: the text said "currently completing an MS", which is now "Completed an MS", consistent with the Sep 2024 – May 2026 education dates.

**Before publishing**, open his DOCX, export it as PDF, and overwrite `resume.pdf` with that official version so formatting and any extra details match his own file exactly.

## Features

- Light / dark toggle in the sticky nav, applied before first paint (no flash), persisted per visitor, with `prefers-color-scheme` and `prefers-reduced-motion` support
- Fully responsive: desktop, tablet, and phone, with a mobile hamburger menu
- Sticky nav with anchor links and scroll-based active-link highlighting
- Subtle scroll-reveal animations via `IntersectionObserver` (plain CSS fallback if JS is off)
- Semantic HTML, accessible labels/focus states, skip link, print stylesheet, and print-safe light theme
- No forms, no tracking, no analytics, no cookies
