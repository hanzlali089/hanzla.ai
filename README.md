# Hanzla Ali — Portfolio Website

A premium, responsive AI Engineer portfolio built with plain HTML, CSS, and JavaScript. No build step, no framework — fully static and ready for GitHub Pages.

## File structure

```
.
├── index.html          # All page content and structure
├── css/
│   └── style.css       # Design system, layout, animations
├── js/
│   └── script.js       # Scroll reveal, mobile nav, typing effect, contact form fallback
├── assets/
│   └── hanzla-profile.jpg
└── README.md
```

## Run it locally

No build tools required. Either:

1. Double-click `index.html` to open it directly in a browser, **or**
2. Serve it locally (recommended, avoids any relative-path quirks):
   ```bash
   cd portfolio
   python3 -m http.server 8000
   ```
   Then visit `http://localhost:8000`.

## Deploy to GitHub Pages

1. Create a new GitHub repository (or use an existing one).
2. Push this folder's contents to the repository root (or to a `docs/` folder — see step 4):
   ```bash
   git init
   git add .
   git commit -m "Portfolio site"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<repo-name>.git
   git push -u origin main
   ```
3. On GitHub, go to **Settings → Pages**.
4. Under **Build and deployment → Source**, choose **Deploy from a branch**, pick `main` and `/ (root)` (or `/docs` if you used that folder).
5. Save. GitHub will give you a live URL, typically:
   `https://<your-username>.github.io/<repo-name>/`
6. It can take a minute or two for the first deploy to go live.

All asset paths in this project are relative (`css/style.css`, `js/script.js`, `assets/...`), so it works whether the site is served from the repo root or a subpath.

## Customizing content

- **Text content**: everything lives directly in `index.html` — search for the section you want (`<section id="...">`) and edit the text between tags.
- **Colors / fonts / spacing**: all design tokens are defined once at the top of `css/style.css` inside `:root`. Change a value there (e.g. `--signal: #35e6c4;`) and it updates everywhere.
- **Profile photo**: replace `assets/hanzla-profile.jpg` with a new image of the same filename, or update the `src` in the About section of `index.html`.
- **Stats**: the animated counters in the "stats band" use `data-count` and `data-suffix` attributes — edit the numbers directly on the `<span>` elements.
- **Hero rotating role text**: edit the `roles` array near the top of `js/script.js`.

## Updating project links

Currently no GitHub repo or live-demo links are included for individual projects, since none were confirmed as available. To add them:

1. Find the relevant `.project-card` or `.featured-card` in `index.html`.
2. Add a link/button, for example:
   ```html
   <a href="https://github.com/hanzlali089/your-repo" target="_blank" rel="noopener" class="btn btn-outline" style="margin-top: 1rem; font-size: 0.8rem; padding: 8px 16px;">View on GitHub →</a>
   ```
3. Only add real, working links — the site is written to avoid placeholder or fake links.

## Configuring the contact form

GitHub Pages is static hosting — it cannot process form submissions on its own. The contact form currently falls back to opening the visitor's email client (`mailto:`) when submitted, so it never silently pretends to work.

To make it submit properly instead:

1. Sign up at [Formspree](https://formspree.io) (free tier available) and create a new form. You'll get an endpoint like `https://formspree.io/f/abc12345`.
2. In `index.html`, find the `<form id="contact-form" ...>` element in the Contact section.
3. Replace both instances of `CONFIGURE_ME` with your real Formspree endpoint ID:
   ```html
   <form id="contact-form" class="contact-form" action="https://formspree.io/f/abc12345" method="POST" data-endpoint="abc12345">
   ```
4. Once `data-endpoint` no longer equals `CONFIGURE_ME`, the JavaScript fallback in `js/script.js` stops intercepting the submit — the form will POST to Formspree directly and show their default success page (or you can configure a redirect in your Formspree dashboard).

Alternatively, you can remove the `<form>` entirely and keep only the `mailto:` link and contact cards already present in the Contact section.

## Pre-launch checklist

- [x] Semantic HTML5 with a single `<h1>` and logical heading order
- [x] Responsive from mobile through large desktop
- [x] Keyboard-focusable nav, links, and form fields with visible focus states
- [x] `prefers-reduced-motion` respected (disables scroll reveal, typing effect, counters)
- [x] All social/contact links point to real profiles from the source resume — no invented links
- [x] No fake project demo/GitHub links — add real ones when available (see above)
- [x] Age removed; replaced with a "6+ AI Agents Developed" achievement stat
- [x] Relative file paths throughout — safe for GitHub Pages root or subpath hosting
