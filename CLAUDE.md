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
