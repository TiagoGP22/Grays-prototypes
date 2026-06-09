# Acceptance Team — Prototypes

A shared site for our clickable prototypes, hosted on GitHub Pages.

🔗 **Live site:** https://tiagogp22.github.io/Acceptance-Prototypes/
🔑 For the Password - check the Acceptance Slack Channel!

The home page is split into five areas: **Terminal and Tap, eCommerce, Platform and Services, Gateway, Host.** Each prototype is a standalone HTML file in its area's folder.

```
/
├── index.html                       # home page + password gate
├── terminal-and-tap/
│   └── teya-loyalty.html
├── ecommerce/
├── platform-and-services/
├── gateway/
└── host/
```

---

## Getting access (one-time)

The repo lives under a personal GitHub account, so to upload you need to be added as a collaborator.

- Ping **Tiago** with your GitHub username.
- He adds you via **Settings → Collaborators → Add people**.
- You'll get an email invite — accept it, and you can then edit/upload.

(No access yet? You can still view the live site with the password — you just can't add prototypes.)

---

## How to add your prototype (no command line)

Everything is done in the GitHub web UI. The site redeploys automatically ~1 minute after you commit.

### 1. Upload your file
1. Open the repo and click the **area folder** your prototype belongs in (e.g. `terminal-and-tap`).
2. Click **Add file → Upload files**.
3. Drag in your **standalone HTML file**, then click **Commit changes**.

> Adding to an area that has no folder yet? Use **Add file → Create new file** and type `area-name/your-file.html` — the `/` creates the folder.

### 2. Add it to the home page
Uploading makes the file live at its URL, but it won't show on the home page until you add a card.

1. Open **`index.html`** → click the **pencil icon** (Edit).
2. Find your area's `<div class="grid"> … </div>` and paste a card inside it:

   ```html
   <a class="card" href="terminal-and-tap/your-file.html">
     <div class="title">Your Prototype Name <span class="arrow">→</span></div>
     <div class="desc">One-line description of the flow.</div>
   </a>
   ```

3. If your area still shows the "No prototypes yet" box, replace that whole `<div class="empty"> … </div>` with a `<div class="grid"> … </div>` containing your card, and update the count chip (e.g. `1 prototype`).
4. Scroll down → **Commit changes**.

> Not comfortable editing the HTML? Just upload your file (step 1) and ping Tiago — he'll add the card.

### 3. Check it
Wait ~1 min, hard-refresh the live site (**Cmd/Ctrl+Shift+R**), enter the password, and your card should be there.

---

## Conventions (please follow)

- **One self-contained HTML file** per prototype — no separate CSS/JS or build steps.
- **Filenames:** lowercase, hyphenated, `.html` (e.g. `tap-refunds.html`). No spaces.
- **Put it in the right area folder** — don't drop files in the repo root.
- **Replacing a prototype?** Upload a file with the **same name** to the same folder — it overwrites on commit (no need to delete first).

---

## Password & security — read this

To change the password: open `index.html`, edit this line near the top of `<body>`:

```html
<script>window.SITE_PASSWORD = "teya-prototypes";</script>
```

⚠️ The password is a **deterrent, not real protection**. Because the site is static:
- The password is visible to anyone who views page source.
- Prototype files are reachable by direct URL without the password.

It stops casual snooping but won't keep determined viewers out. **Don't put anything genuinely confidential here.** If we ever need real protection, we can switch to encrypted pages (AES — content unreadable without the password).
