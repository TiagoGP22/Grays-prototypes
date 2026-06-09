# Acceptance Team — Prototypes

Static site for sharing clickable prototypes, hosted on GitHub Pages. The home page (`index.html`) is split into five product areas:

- Terminal and Tap
- eCommerce
- Platform and Services
- Gateway
- Host

Each prototype is a standalone HTML file living in the matching folder.

```
/
├── index.html                       # home page (the five areas)
├── .nojekyll                        # serve folders/files with hyphens as-is
├── terminal-and-tap/
│   └── teya-loyalty.html            # first prototype
├── ecommerce/
├── platform-and-services/
├── gateway/
└── host/
```

## One-time setup: publish to GitHub Pages

1. Create a repo under the **AcceptanceTeam** org, e.g. `prototypes`.
2. From the `site/` folder, push these files to `main`:

   ```bash
   cd site
   git init
   git add .
   git commit -m "Initial prototypes site"
   git branch -M main
   git remote add origin https://github.com/AcceptanceTeam/prototypes.git
   git push -u origin main
   ```

3. In the repo: **Settings → Pages → Build and deployment**
   - Source: **Deploy from a branch**
   - Branch: **main** / **/ (root)** → Save.

4. After ~1 minute the site is live at:

   `https://acceptanceteam.github.io/prototypes/`

   Teya Loyalty: `https://acceptanceteam.github.io/prototypes/terminal-and-tap/teya-loyalty.html`

> If you'd rather host it at the org root (`https://acceptanceteam.github.io/`), name the repo `AcceptanceTeam.github.io` instead — same steps otherwise.

## Adding a new prototype

1. Drop the HTML file into the relevant area folder (e.g. `terminal-and-tap/new-flow.html`).
2. In `index.html`, add a card to that area's `<div class="grid">`:

   ```html
   <a class="card" href="terminal-and-tap/new-flow.html">
     <div class="title">New Flow <span class="arrow">→</span></div>
     <div class="desc">Short one-line description.</div>
   </a>
   ```

   For an area's **first** prototype, replace its `<div class="empty">…</div>` block with a `<div class="grid">…</div>` containing the card, and bump the `count` chip.
3. Commit and push — Pages redeploys automatically.

## Notes

- Prototypes are self-contained HTML, so no build step is needed.
- Keep filenames lowercase with hyphens (`teya-loyalty.html`).
- The `.nojekyll` file stops GitHub from filtering folders — keep it.
