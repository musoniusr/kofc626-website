# KofC626.com Website

The website for **Knights of Columbus Council 626** (Norwalk, Ohio).

Live site: https://kofc626.com
GitHub repo: https://github.com/musoniusr/kofc626-website

This is a **plain static website** — just HTML, CSS, and images. No build tools, no
frameworks, nothing to install to make it run. If you can edit a text file, you can
update this site.

---

## How updates get to the live site

```
You edit files  →  git push to GitHub  →  Cloudflare deploys automatically
```

Every time changes are pushed to the `master` branch on GitHub, Cloudflare
automatically rebuilds and publishes the live site at kofc626.com within about
1–2 minutes. **You never upload files anywhere manually** — pushing to GitHub is
the entire deployment process.

You can watch a deploy happen (or check its status) at:
Cloudflare Dashboard → Workers & Pages → `kofc626-website` → **Deployments** tab.

---

## One-time setup (only do this once, on each computer you edit from)

You need two things: **Git** installed, and a copy of the repository on your
computer.

### Option A — GitHub Desktop (recommended for beginners)

1. Download and install **GitHub Desktop**: https://desktop.github.com
2. Sign in with the GitHub account that has access to this repo.
3. File → Clone Repository → search for `kofc626-website` → choose a folder on
   your computer → Clone.
4. That folder now contains the full website. Open it in File Explorer any time.

### Option B — Command line Git

1. Install Git: https://git-scm.com/downloads
2. Open a terminal (PowerShell on Windows) and run:
   ```
   git clone https://github.com/musoniusr/kofc626-website.git
   cd kofc626-website
   ```

---

## Everyday workflow: making a change

### 1. Open the project folder and edit files

- **`index.html`** — the main page (About, Special Events, Regular Events, Hall
  Rental, Contact). This is where most updates happen — new event dates, prices,
  descriptions, etc.
- **`dues.html`** — the "Pay Dues" page.
- **`styles.css`** — colors, fonts, spacing, layout. Only edit this if you're
  changing the look of the site.
- **`script.js`** — small bits of interactive behavior (menu toggle, etc.).
  Rarely needs changes.
- Image files (`.jpg` / `.webp` / `.png`) — see [Working with images](#working-with-images-and-sizing) below.

You can edit `.html` and `.css` files with any plain text editor — Notepad
works, but **VS Code** (https://code.visualstudio.com, free) is much nicer and
recommended if you'll be doing this more than once.

**Example — this is what one "Special Event" card looks like in `index.html`:**

```html
<div class="special-event-card">
    <h3>
        <span class="event-icon food">🍽️</span>
        Smoked Pork Dinner Fundraiser Dinner to Benefit Catholic Education
    </h3>
    <div class="event-image">
        <img src="smoked pork plate - web.jpg" alt="Smoked Pork Dinner Fundraiser Dinner to Benefit Catholic Education">
    </div>
    <p><strong>Date:</strong> Monday, August 3, 2026<br>
    <strong>Time:</strong> 5:00–7:00 P.M.<br>
    <strong>Cost:</strong> $15.00 per person<br>
    <strong>Location:</strong> KofC Social Counter, 254 West Main Street, Norwalk, OH 44857</p>

    <p><strong>Menu:</strong> Smoked Pulled Pork, Mac and Cheese, Baked Beans, Coleslaw, and Corn Cake.</p>

    <div class="event-actions">
        <a href="https://buy.stripe.com/28E8wQ0qr9xAbyy4Nh2kw0B" target="_blank" class="btn btn-primary">Buy Tickets Online</a>
    </div>
</div>
```

To add a **new** event, copy one of these entire `<div class="special-event-card">...</div>`
blocks, paste it, and change the text, image filename, date/time/cost, and link.
To remove an event, delete its whole block (from `<div class="special-event-card">`
down to its matching closing `</div>`).

### 2. Preview your changes before publishing

Just double-click `index.html` in the project folder — it opens in your browser
and shows exactly what visitors will see. Refresh the page after each edit.
Nothing is public yet at this point — you're only looking at the file on your
own computer.

### 3. Publish the change (push to GitHub)

**Using GitHub Desktop:**
1. Open GitHub Desktop — it will show your changed files automatically.
2. Type a short summary of what you changed (bottom-left box), e.g. "Update pork dinner date".
3. Click **Commit to master**.
4. Click **Push origin** (top toolbar).

**Using the command line**, from inside the project folder:
```
git add .
git commit -m "Update pork dinner date"
git push
```

That's it. Cloudflare picks up the push automatically and the live site updates
within a minute or two — no further action needed.

### 4. Verify it went live

Open https://kofc626.com (hard-refresh with `Ctrl+Shift+R` if you don't see the
change — browsers cache pages) or check the **Deployments** tab in the
Cloudflare dashboard mentioned above to confirm the new deployment succeeded.

---

## Working with images and sizing

Adding photos is the most common update, and the most common way to
accidentally slow the site down, so a few rules of thumb:

| Use case | Example | Recommended width | Target file size |
|---|---|---|---|
| Event/card photo (`.event-image`) | pork dinner, rosary, football crazr | **900–1200 px wide** | under 200 KB |
| Hall rental photo (`.rental-image`) | hall rental.jpg | **1000–1200 px wide** | under 250 KB |
| Any photo, in general | — | never wider than **1600 px** | under 300 KB |

Why: these images display at roughly 400–500px wide on screen, but phones and
retina displays need ~2x that in the source file to look sharp — anything much
bigger than the numbers above is wasted file size that just makes the page
slower to load, without looking any better.

**Before adding a new photo:**
1. **Resize** it so the longer side is around 1000–1200 pixels (Windows Photos
   app, Preview on Mac, or https://squoosh.app for a free browser-based tool).
2. **Compress/convert** it — `.webp` format gives noticeably smaller files than
   `.jpg` at the same quality. https://squoosh.app can convert and compress in
   one step; just drag your photo in, pick WebP, and adjust quality until the
   file size looks reasonable (aim for the targets in the table above).
3. **Name the file** something short and descriptive, e.g. `chicken-dinner-2027.webp`.
   Avoid spaces in new filenames if you can (use hyphens instead) — it keeps
   the `src="..."` references in the HTML simpler to type correctly.
4. Put the file in the main project folder (same place as `index.html`).
5. Reference it in the HTML: `<img src="your-file-name.webp" alt="Describe the photo">`.
   Always fill in `alt="..."` with a short description — it's what screen
   readers announce and what shows up in search results.

**Removing an old photo:** once no `<img src="...">` in `index.html` or
`dues.html` refers to a file anymore, you can delete that file from the folder
too (right-click → delete, then commit/push as usual) so the repo doesn't
accumulate unused images.

---

## Undoing a mistake

**Before you've pushed:** just re-edit the file back, or in GitHub Desktop
right-click the changed file → "Discard changes."

**After you've pushed and the live site looks wrong — anyone with GitHub
access can fix this, no Cloudflare login needed:** just edit the file back to
how it was (or fix the mistake) and commit/push again, the same way you'd make
any other change. A new push always overwrites whatever's live, so pushing a
correction fixes the site the same way pushing the mistake broke it — usually
within a minute or two.

**If you have Cloudflare access** (currently just the council's website
administrator): there's also a faster shortcut — Cloudflare Dashboard →
Workers & Pages → `kofc626-website` → **Deployments**, find the last
deployment that was correct, and use its **rollback / redeploy** option to
instantly revert the live site to that version while the underlying file gets
fixed at your own pace.

---

## Project structure

```
index.html                  Main page (About, Events, Hall Rental, Contact)
dues.html                   Pay Dues page
styles.css                  All site styling
script.js                   Menu/interactive behavior
wrangler.jsonc               Cloudflare deployment config — don't need to touch this
kofc_favicon_io/            Site icon files — don't need to touch these
*.jpg / *.webp / *.png      Photos used throughout the site
.gitignore                  Tells git to ignore backup .zip files, etc.
```

Backup `.zip` snapshots of the site are kept **outside** this folder (in a
sibling `kofc626.com backups` folder), not in this repository — they don't need
to be, and shouldn't be, tracked by git.

---

## Where things live

- **Live site:** https://kofc626.com
- **GitHub repo:** https://github.com/musoniusr/kofc626-website
- **Cloudflare project:** Workers & Pages → `kofc626-website` (deploys, custom
  domains, logs)
- **Domain registrar:** Namecheap (DNS is managed through Cloudflare; email
  forwarding for `@kofc626.com` addresses is still handled by Namecheap — don't
  delete the `MX` or `TXT` records in Cloudflare's DNS settings)
