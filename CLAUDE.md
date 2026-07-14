# randomphonebuilds — Claude Instructions

This repo hosts self-contained HTML documents on GitHub Pages at:
**https://ratfacedgranny.github.io/randomphonebuilds/**

The homepage auto-discovers all project folders using the GitHub API — no manual index updates needed. Add a folder, push, and it shows up on the homepage by itself.

Local working copy lives at: `~/Projects/randomphonebuilds`

## Trigger phrase

When Zach says **"push this to randomphonebuilds"** (or "add this to randomphonebuilds", "publish this", etc.), it means: take the thing we just made — a doc, a page, an idea — turn it into a self-contained HTML page, drop it in a new folder here, and push. Follow the steps below exactly.

## When Zach asks to publish a new document

### 1. Choose a folder name
- Ask Zach what to name it, or derive a short, descriptive kebab-case name from the topic
- Example: `x32-troubleshooting`, `drum-rates`, `studio-gear-list`

### 2. Create the folder and add files
- Create a new folder at the repo root with that name
- Put the HTML file(s) inside as `index.html` (plus any supporting files: images, PDFs, audio, etc.)
- The HTML must be fully self-contained: inline CSS, no build step, no external dependencies beyond Google Fonts
- Give the `<title>` tag a clear, descriptive name — the homepage reads it and shows it as the card subtitle
- **REQUIRED:** Add `<meta name="published" content="YYYY-MM-DD">` in the `<head>` with today's date. The homepage sorts newest-first by this date and displays it on each card. Without it, the project sorts to the bottom.

### 3. Commit and push to main
```
cd ~/Projects/randomphonebuilds
git add FOLDER_NAME/
git commit -m "Add FOLDER_NAME: short description"
git push origin main
```

### 4. Give Zach the link
The live URL will be:
**https://ratfacedgranny.github.io/randomphonebuilds/FOLDER_NAME/**

GitHub Pages deploys automatically — usually 30–60 seconds.

## Design style guide

The house style below is the **default baseline**, not a straitjacket. Zach isn't design-obsessed like Matt — so unless he asks for something specific, use good judgment to make each page look its best, and lean on the house tokens so the site still feels cohesive. If he asks for a different look for a given page, do that instead.

Match the homepage. Apple-inspired, clean, reads great on a phone.

- **Font:** Inter (Google Fonts) with `-apple-system, BlinkMacSystemFont, "SF Pro Display"` fallback
- **Accent:** `#C42020` (red)
- **Background:** `#FAFAFA`
- **Card / surface:** `#FFFFFF`
- **Text:** `#1D1D1F` primary, `#6E6E73` secondary
- **Divider:** `#E5E5E7`
- Generous whitespace, `line-height: 1.7`, max content width around 680px
- A thin 3px accent bar across the very top of the page (`.top-bar`)
- Responsive — must look good on phones first

Reuse the `:root` custom-property block and base styles from the homepage `index.html` so pages stay consistent.

### Dark mode — REQUIRED on every document

Every project page must have a working light/dark toggle. The reference implementation is in `pioneer-point-x32/index.html` — copy that pattern. Build every page with **CSS custom properties for all colors** (never hardcode a hex in a rule — use a token), so a single dark override block re-themes the whole page.

**1. Theme tokens** — light in `:root`, dark in `:root[data-theme="dark"]`:
```css
:root {
  --accent: #C42020; --accent-soft: rgba(196,32,32,0.06); --on-accent: #FFFFFF;
  --bg: #FAFAFA; --card-bg: #FFFFFF;
  --text-primary: #1D1D1F; --text-secondary: #6E6E73;
  --divider: #E5E5E7; --code-bg: #F0F0F2;
  color-scheme: light;
}
:root[data-theme="dark"] {
  --accent: #FF6B5E; --accent-soft: rgba(255,107,94,0.10); --on-accent: #201014;
  --bg: #161619; --card-bg: #1F1F24;
  --text-primary: #F5F5F7; --text-secondary: #A1A1A6;
  --divider: #34343C; --code-bg: #2A2A31;
  color-scheme: dark;
}
```
Note the accent **brightens** in dark (`#C42020` is too dark on a near-black bg), and `--on-accent` is the text/foreground color to use on top of an accent-filled shape (white in light, near-black in dark) — use it anywhere you'd otherwise put `color:#fff` on an accent background.

**2. Anti-flash script in `<head>`** (sets theme before paint):
```html
<script>(function(){try{var s=localStorage.getItem('rpb_theme');var d=window.matchMedia&&window.matchMedia('(prefers-color-scheme: dark)').matches;document.documentElement.setAttribute('data-theme',s||(d?'dark':'light'));}catch(e){document.documentElement.setAttribute('data-theme','light');}})();</script>
```

**3. Toggle button** (first thing in `<body>`) + handler (end of `<body>`):
```html
<button class="theme-toggle" id="themeToggle" type="button" aria-label="Toggle dark mode" title="Toggle dark mode">🌙</button>
...
<script>(function(){var r=document.documentElement,b=document.getElementById('themeToggle');function s(){b.textContent=r.getAttribute('data-theme')==='dark'?'☀️':'🌙';}s();b.addEventListener('click',function(){var t=r.getAttribute('data-theme')==='dark'?'light':'dark';r.setAttribute('data-theme',t);try{localStorage.setItem('rpb_theme',t);}catch(e){}s();});})();</script>
```
Default follows the visitor's OS setting; their manual choice is remembered per-device in `localStorage` under `rpb_theme` (shared key across all pages, so the whole site stays in sync).

## Formatting rules
- Never wrap URLs/links in bold (`**`). Paste them plain.

## Important: everything here is PUBLIC
- The repo is public (required for the free GitHub Pages + auto-discovery to work).
- The homepage password (`letmesee`) is a speed bump, not security — the check runs in the page's own JavaScript, and it only covers the homepage. Direct folder links open with no password.
- So: **never put contracts, invoices, rates tied to a client, SSNs, addresses, or anyone's private info here.** Treat every file as world-readable. If Zach asks to publish something sensitive, flag it before pushing.

## Branch / push rules
- Push straight to `main`.
- Do NOT open pull requests.
- Do NOT edit the root `index.html` — it's dynamic and self-updating. Leave it alone.
- Every project folder must have an `index.html` with a descriptive `<title>` and a `published` meta tag.
