# UBCON General Suppliers — Static Website

A pre-rendered, multi-page static export of the UBCON website.
Every page is real HTML (good for SEO + sharing), and the JavaScript
bundles power animations, the WhatsApp FAB, light/dark mode, and the
mobile navigation.

## Folder structure

```
ubcon-static/
├── index.html          ← Home
├── about.html          ← About + team
├── services.html       ← Services / sectors
├── portfolio.html      ← Portfolio
├── events.html         ← Upcoming events
├── contact.html        ← Contact form (prefills WhatsApp)
│
├── assets/             ← All bundled CSS, JS, and images
│   ├── styles-*.css        → global stylesheet (Tailwind v4)
│   ├── router-*.js         → TanStack Router runtime
│   ├── index-*.js          → Home page chunk
│   ├── about-*.js          → About page chunk
│   ├── services-*.js       → Services page chunk
│   ├── portfolio-*.js      → Portfolio page chunk
│   ├── events-*.js         → Events page chunk
│   ├── contact-*.js        → Contact page chunk
│   ├── AnimatedScene-*.js  → Hero animation
│   ├── logo-*.png          → UBCON logo
│   └── *.jpg               → Sector / team / hero images
│
├── docs/
│   └── UBCON-Company-Profile-2026.pdf
│
├── favicon.ico
└── README.md           ← this file
```

## How to run it locally

Modern browsers block ES modules when you double-click an .html file
(`file://` protocol). Serve the folder over HTTP instead — pick any one:

```bash
# Python (already installed almost everywhere)
python3 -m http.server 8080

# Node.js
npx serve .

# PHP
php -S localhost:8080
```

Then open http://localhost:8080.

## How to deploy

Drag-and-drop the entire folder to any static host:

- **Netlify** — drop the folder onto https://app.netlify.com/drop
- **Vercel** — `vercel deploy` from inside the folder
- **GitHub Pages** — commit the folder to a repo and enable Pages
- **Cloudflare Pages** — connect the repo or upload via the dashboard
- **AWS S3 + CloudFront** — `aws s3 sync . s3://your-bucket`

## Editing tips

- **Text changes** → open the relevant `*.html` file and edit the
  text inside the rendered HTML. Each page is fully self-contained.
- **Colors / theme** → edit `assets/styles-*.css` (search for `oklch(`
  to find token definitions).
- **Logo** → replace `assets/logo-*.png` with a same-named PNG, or
  swap the `<img src="./assets/logo-...">` references in each HTML.
- **Phone / address / email** → search-and-replace across the HTML
  files; current values are `+260 769 055 719`, `Kitwe, Zambia`,
  `ubconsuppliers@gmail.com`.
- **Adding a page** → copy any existing `*.html` as a template and
  add a matching link in the header navigation in every file.
- **Big structural changes** → edit the React source in the original
  Lovable project and re-export — the JS bundles are minified and
  not designed to be hand-edited.

## Notes

- The contact form prefills a WhatsApp message; it does not POST
  to a backend. To collect emails, wire the form to a service like
  Formspree, Web3Forms, or Netlify Forms.
- The floating WhatsApp button uses `wa.me/260769055719`.
- All asset and link paths are relative, so the site works from any
  subdirectory.

## Deploying to Vercel (clean URLs, no 404 on refresh)

This bundle includes a `vercel.json` that:
- Enables `cleanUrls` so visitors see `/about` instead of `/about.html`.
- Rewrites every clean URL to its underlying `.html` file, so refreshing
  on `/about`, `/services`, `/portfolio`, `/events`, or `/contact` works.
- Adds a 1-year cache header for hashed files in `/assets/*`.

### Deploy steps
1. Drag-and-drop the unzipped folder onto https://vercel.com/new, or run
   `npx vercel` from inside this folder.
2. Vercel auto-detects it as a static project — no build command needed.
3. After deploy, refresh any inner page (e.g. `/services`) to confirm.

If you ever add a new HTML page, add a matching entry to the `rewrites`
array in `vercel.json`.
