# ShiftNote by Goemon Technologies

Static landing page for https://shiftnote.mndn.dev.

- `/` — Japanese (`index.html`)
- `/en/` — English (`en/index.html`); `/en` redirects to this directory on standard static hosts.
- `assets/site.css` — shared responsive styles and language navigation
- `assets/og-ja.png`, `assets/og-en.png` — 1200 × 630 sharing cards
- `favicon.ico`, `assets/favicon.svg`, `assets/apple-touch-icon.png` — site icons

Preview locally with `python3 -m http.server 4173`, then visit http://localhost:4173.
Deploy the repository root as the static web root, with directory index serving enabled. No build step is required. Both pages include server-readable Open Graph, Twitter card, canonical and alternate-language metadata; sharing previews require these files to be deployed on the public domain. Font and Tailwind CSS loading still use the original external CDNs.

Keep the Japanese and English HTML in sync when changing content. Existing login, signup and demo buttons and legal-link placeholders remain presentation-only.
