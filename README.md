# KofC626.com Website

The website for **Knights of Columbus Council 626** (Norwalk, Ohio) and
**Fr. Stephen Badin Fourth Degree Assembly 823**.

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

### 1. Pull the latest changes first

**Before you start editing**, always get the latest version — someone else may
have updated the site since you last opened this folder. Skipping this step is
the most common way to accidentally undo someone else's edit.

**Using GitHub Desktop:** open it and click **Fetch origin** (it becomes
**Pull origin** if there's anything new) at the top of the window.

**Using the command line**, from inside the project folder:
```
git pull --rebase
```

Do this every single time, even if you *just* pushed a change yourself
minutes ago — someone else may have pushed in between.

> **More than one person edits this site.** If you already have changes you
> haven't committed yet, **commit them first (step 4's commit, without the
> push), then pull.** Git never overwrites committed work — when two people
> changed different parts of a file, it combines them automatically.

### 2. Open the project folder and edit files

- **`index.html`** — the main Council 626 page (About, officers photo, Special
  Events, Regular Events, Calendar, Hall Rental, Contact). This is where most
  updates happen — new event dates, prices, descriptions, etc.
- **`assembly823.html`** — the Fourth Degree Assembly 823 page (About,
  Meetings, Officers, Contact). It has its own look; see
  [Site look: Council vs. Assembly](#site-look-council-vs-assembly).
- **`dues.html`** — the "Pay Dues" page.
- **`styles.css`** — colors, fonts, spacing, layout. Only edit this if you're
  changing the look of the site.
- **`script.js`** — small bits of interactive behavior (smooth scrolling, cards
  that fade in as you scroll, the footer year). Rarely needs changes.
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

### 3. Preview your changes before publishing

Just double-click `index.html` (or `assembly823.html`) in the project folder — it
opens in your browser and shows exactly what visitors will see. Refresh the page after each edit.
Nothing is public yet at this point — you're only looking at the file on your
own computer. Check things over carefully here — this is the "testing" step,
before anything gets pushed.

Things worth checking every time:
- **Make the browser window narrow** (or use a phone) as well as wide. Some
  CSS only applies at one size, so a page can look fine on one and broken on
  the other.
- **No sideways scrollbar.** If the page scrolls left-to-right, something
  (usually a big image) is wider than the page.
- Cards fade in as you scroll to them, so a card that looks blank for a
  split second is normal.

### 4. Publish the change (push to GitHub) — only after testing

**Using GitHub Desktop:**
1. Open GitHub Desktop — it will show your changed files automatically.
2. Type a short summary of what you changed (bottom-left box), e.g. "Update pork dinner date".
3. Click **Commit to master**.
4. Click **Push origin** (top toolbar).

**Using the command line**, from inside the project folder:
```
git add .
git commit -m "Update pork dinner date"
git pull --rebase
git push
```

The `git pull --rebase` right before pushing picks up anything someone else
pushed while you were editing. If `git push` is still rejected ("fetch first"
or "non-fast-forward"), someone pushed in the last few seconds — run
`git pull --rebase` again, then `git push` again.

**If Git reports a conflict** (you both changed the same lines): Git stops
instead of overwriting anything. If you can't sort it out, run
`git rebase --abort` to go back to where you were and ask the website
administrator for help. **Never use `git push --force`** — it erases other
people's changes from the live site.

That's it. Cloudflare picks up the push automatically and the live site updates
within a minute or two — no further action needed.

### 5. Verify it went live

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
| Officers group photo (`.officers-photo`) | 2026-2027-officers.webp | **1200–1600 px wide** | under 150 KB |
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
5. Reference it in the HTML:
   `<img src="your-file-name.webp" alt="Describe the photo" loading="lazy">`.
   Always fill in `alt="..."` with a short description — it's what screen
   readers announce and what shows up in search results. `loading="lazy"`
   makes the browser wait to download the image until the visitor scrolls
   near it; use it on every image except the emblems at the very top of a page.

### Choosing the right file format

| What it is | Use | Why |
|---|---|---|
| Photo or event flyer (from a camera, phone, Canva, Publisher) | **WebP** (or JPG) | Small files; flyer text stays sharp at quality 80–85 |
| Logo or emblem with a see-through background | **PNG** | Keeps transparency and crisp edges |
| Icons in `kofc_favicon_io/` and `assembly_favicon/` | PNG / ICO | Leave as they are |

**Don't save photos or flyers as PNG.** PNG is meant for logos and simple
graphics; for a photo or a colorful flyer it makes files 5–10 times bigger
with no visible gain. Example from this site: an 800×436 fish dinner flyer
saved as PNG was **799 KB**; the same flyer as WebP is **54 KB**, about 15 times smaller.
When exporting from Canva or Publisher, choose **JPG**, then run it through
https://squoosh.app to make a WebP.

After converting, open the new file and zoom in on any small text (dates,
prices, phone numbers) to make sure it's still easy to read. If it's fuzzy,
raise the quality a little and try again.

**Quick size check:** in File Explorer, look at the file's size before you
add it. Over **300 KB** for one image means it still needs resizing or
converting.

### Keep originals out of the website folder

Only the web-ready version belongs in this folder. Keep the full-size original
(the camera photo, the Canva download) in your own Pictures or Documents
folder. Everything in this folder is published to the live site and stored in
Git forever, even after it's deleted.

**Clean up when an event ends.** When you remove an event card, delete its
image file in the same commit, unless the card is only commented out
(`<!-- ... -->`) to reuse later. Old versions stay in Git history, so a
deleted image can always be recovered.

**A photo wider than about 1200 px must sit inside something that limits its
width** (an `.event-image`, `.rental-image`, or `.officers-photo` block, which
all scale images to fit). A bare `<img>` straight from a camera or phone shows
at full size and makes the whole page wider than the screen.

**Removing an old photo:** once no `<img src="...">` in `index.html`,
`assembly823.html`, or `dues.html` refers to a file anymore, you can delete that file from the folder
too (right-click → delete, then commit/push as usual) so the repo doesn't
accumulate unused images.

---

## Editing styles.css safely

- **Put new rules above the `@media (max-width: 768px) {` line** near the
  bottom of the file. Everything inside that block applies **only to phones**.
  Rules pasted inside it by mistake silently do nothing on computers.
  (This happened with the officers photo in October 2026 — the photo showed
  at full size on desktops and pushed the whole page sideways.)
- **Use the color variables, not color codes.** The site's colors are set
  once at the top of the file (`--primary-color`, `--secondary-color`,
  `--accent-color`). Write `color: var(--primary-color);` instead of `#142965`
  so everything stays matched and each page keeps its own theme.
- Every `{` needs a matching `}`. One missing brace can break all the rules
  after it.

---

## Site look: Council vs. Assembly

Both pages share `styles.css` and the same layout, but each has its own colors
and emblem so visitors can tell them apart.

| Page | Emblem file | Colors | How it's set |
|---|---|---|---|
| Council 626 (`index.html`, `dues.html`) | `images/kofc-emblem.png` | Emblem navy `#142965`, gold `#f6b618` | `:root` at the top of `styles.css` (the default) |
| Assembly 823 (`assembly823.html`) | `images/4th-degree-emblem.png` | Deeper navy `#0b2545`, gold `#fdb913`, red `#d6312a` | `<body class="assembly">` + the `body.assembly` rules in `styles.css` |

- Any rule starting with `body.assembly` affects only the Assembly page.
- The Assembly page has its own browser-tab icons in `assembly_favicon/`; the
  Council pages use `kofc_favicon_io/`.
- **Emblem rules (Knights of Columbus brand guidelines):** don't recolor,
  stretch, crop, or add effects to the emblems, keep the ® mark, and leave some
  empty space around them. Change the page colors around an emblem, never the
  emblem itself.
- The original high-resolution logo files (EPS) aren't in this repository; the
  website administrator has them.

---

## Recurring updates

### Officers (new terms start July 1)

Officers are listed in two places, and many Sir Knights hold offices in both:

- **Council officers:** the `officer-list` under the officers photo in
  `index.html`. Replace the photo file when a new one is taken (see
  [Working with images](#working-with-images-and-sizing) for sizing).
- **Assembly officers:** the `officer-table` in `assembly823.html`.

Conventions:
- Use names **exactly as on the official roster**, with middle initials:
  *Joseph R. Lesch*, not *Joe Lesch*. When someone changes on one page, check
  whether they're also listed on the other.
- **Never put member numbers or start dates on the site** — it's public.
- List officers in roster order. Assembly titles differ from Council titles
  (e.g. the chaplain is *Faithful Friar* in the Assembly).

### Meeting times

Each page lists its meeting time **in two places** — update both:

- `index.html`: the "3rd Degree Meetings" card under Regular Events, **and**
  "Meeting Times" in the Contact section.
- `assembly823.html`: the "4th Degree Meetings" card under Meetings, **and**
  "Meeting Times" in the Contact section.

As of October 2026: Council meets the 2nd Monday at 7:00 PM; the Assembly
meets right after, usually about 8:00 PM.

### Footer year

`script.js` updates the © year in every page's footer automatically. Leave
the footer text itself alone.

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
index.html                  Council 626 main page (About, Events, Hall Rental, Contact)
assembly823.html            Fourth Degree Assembly 823 page
dues.html                   Pay Dues page
styles.css                  All site styling (Council theme + Assembly overrides)
script.js                   Smooth scrolling, fade-ins, footer year
wrangler.jsonc              Cloudflare deployment config — don't need to touch this
images/                     Emblems (kofc-emblem.png, 4th-degree-emblem.png)
kofc_favicon_io/            Council browser-tab icons — don't need to touch these
assembly_favicon/           Assembly browser-tab icons — don't need to touch these
*.jpg / *.webp / *.png      Photos used throughout the site (main folder)
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

---

## Keep this README up to date

When you learn something the hard way — a gotcha, a convention, a "don't do
this" — add a line to the relevant section above, in the same commit as the
fix. The next person editing the site will thank you.
