# CLAUDE.md — Acceptance Team Prototypes

Instructions for Claude when working in this repo. Humans should read `README.md` instead.

## What this repo is
A static GitHub Pages site that hosts the Acceptance Team's clickable prototypes, organised by product area. Live at https://tiagogp22.github.io/Acceptance-Prototypes/. Each prototype is a single self-contained HTML file. The home page (`index.html`) is a hand-maintained index of cards plus a client-side password gate.

## Structure
```
/
├── index.html        # home page: password gate + one section per area
├── README.md         # human contributor guide
├── CLAUDE.md         # this file
└── <area>/           # one folder per product area, each holds prototype .html files
```
**Areas (canonical names + folder slugs):**
| Area (display) | Folder slug |
|---|---|
| Terminal and Tap | `terminal-and-tap` |
| eCommerce | `ecommerce` |
| Platform and Services | `platform-and-services` |
| Gateway | `gateway` |
| Host | `host` |

If the user names an area loosely (e.g. "tap", "ecomm", "platform"), map it to the closest canonical area above. If it matches none, ask which area — do not invent a new one unless explicitly asked (see "Add a new area").

## Golden rules
1. **Never modify the contents of a prototype HTML file.** Treat prototypes as opaque artefacts — only add, move, replace, or remove the whole file.
2. **Keep the password gate intact.** Do not remove or bypass the gate in `index.html`, and never weaken it unless explicitly told to.
3. **The home page is hand-maintained.** `index.html` does not auto-discover files — every prototype must be added to it manually as a card, or it won't appear.
4. **No confidential content.** This is a public, static site with a deterrent-only password. Flag to the user if a prototype looks like it contains secrets, real customer data, or anything sensitive.
5. **Preserve conventions** (below) on every change.

## Conventions
- One **self-contained** HTML file per prototype (inline CSS/JS, no build step, no external repo assets).
- Filenames: **lowercase, hyphenated, `.html`** (e.g. `tap-refunds.html`). No spaces, no capitals.
- Files live **inside their area folder**, never in the repo root (root is reserved for `index.html`, `README.md`, `CLAUDE.md`, and `.nojekyll`).
- Replacing a prototype: reuse the **same filename** so it overwrites cleanly.

## Playbook: add a prototype
1. Place the file at `<area-slug>/<lowercase-hyphen-name>.html`.
2. Edit `index.html` for that area's `<section class="category">`:
   - If the area still shows a "coming soon" box, **replace** its `<div class="empty">…</div>` with a `<div class="grid">…</div>`.
   - Add a card inside that area's `<div class="grid">`:
     ```html
     <a class="card" href="<area-slug>/<file>.html">
       <div class="title"><Prototype Name> <span class="arrow">→</span></div>
       <div class="desc"><One-line description.></div>
     </a>
     ```
   - Update the area's count chip: `<span class="count">N prototypes</span>` (use "1 prototype" singular).
3. Tell the user it goes live ~1 min after they commit/push to `main`.

## Playbook: replace a prototype
Overwrite the existing file with the same name. Update the card's `desc`/title only if the user asks. No count change.

## Playbook: remove a prototype
1. Delete the file from its area folder.
2. Remove its card from `index.html` and decrement the count chip.
3. If it was the area's only prototype, restore the empty state:
   ```html
   <div class="empty">No prototypes yet. Drop them into <code>/<area-slug></code> and add a card here.</div>
   ```
   and set the count to "0 prototypes".

## Playbook: add a new product area (only if explicitly requested)
1. Pick a lowercase-hyphen slug for the folder.
2. Add a new `<section class="category">` in `index.html` in the desired order, mirroring the existing markup (head, count chip, and an `.empty` box until it has a prototype).
3. Create the folder by adding the first file (empty folders aren't stored by GitHub).
4. Add the area to the table in this file and in `README.md`.

## Playbook: change the password
Edit the single line near the top of `<body>` in `index.html`:
```html
<script>window.SITE_PASSWORD = "...";</script>
```
Remind the user this is a **deterrent only** — visible in page source, and prototype URLs are directly reachable without it. If they need real protection, propose switching to encrypted pages (AES) instead.

## Gotchas (learned the hard way)
- **Empty folders disappear on GitHub** — a folder only exists once it contains a file. The home page shows all areas regardless, because they're hard-coded in `index.html`, not derived from folders.
- **Overwrite, don't duplicate** — uploading a file with the same path/name replaces it; no need to delete first.
- **`.nojekyll`** at the root keeps hyphenated paths serving cleanly — don't delete it.
- **Session unlock** — after a correct password the gate stays open for that browser session (`sessionStorage`); use a private window to test the gate fresh.
- **Two-folder confusion** — there is exactly one site folder; don't create nested `site/site` copies.

## Deploy
GitHub Pages serves `main` at the root. Any commit to `main` redeploys automatically in ~1 minute. There is no build step. For users on the web-only flow, "commit" = the **Commit changes** button after an upload/edit.

## Working style for this repo
- Default to making the change end-to-end (file + index card + count) so the user only has to commit.
- If editing `index.html`, change the minimum needed and keep the existing structure/styles.
- Offer to hand the user the ready-to-paste card snippet when they're doing the upload themselves.
