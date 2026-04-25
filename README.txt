UBCON — Static Site
===================

This folder contains the full static export of the UBCON website with all
animations, dark/light mode, and the floating WhatsApp button included.

HOW TO RUN LOCALLY
------------------
Modern browsers BLOCK JavaScript modules when opened directly from the
filesystem (file://). You MUST serve the folder over HTTP. Any of these work:

  # Python (easiest, comes preinstalled on macOS / Linux)
  python3 -m http.server 8080

  # Node.js
  npx serve .

  # PHP
  php -S localhost:8080

Then open http://localhost:8080 in your browser.

HOW TO DEPLOY
-------------
Just upload the entire folder to any static host:
  - Netlify  (drag & drop the folder onto app.netlify.com/drop)
  - Vercel   (vercel deploy)
  - GitHub Pages
  - Cloudflare Pages
  - Any shared hosting / cPanel public_html

All paths are relative, so it works at the domain root or in a subfolder.

PAGES
-----
  index.html     — Home
  about.html     — About
  services.html  — Services
  portfolio.html — Portfolio
  events.html    — Events
  contact.html   — Contact

