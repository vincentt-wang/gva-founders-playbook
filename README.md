# GVA Founders Playbook

Taiwan-to-Global Pre-Accelerator for Deep Tech Founders — Landing Page

## Live URL

> **Will be:** `https://vincentt-wang.github.io/gva-founders-playbook/`

## What this is

One-page landing site for the GVA Founders Playbook program. Connects to the full methodology at:
`https://vincentt-wang.github.io/marketing-strategy-course/`

## Stack

Pure static HTML/CSS/JS — no build step, no dependencies. Works directly on GitHub Pages.

## Deploy to GitHub Pages

### Step 1 — Create the GitHub repo

Go to github.com → New repository → name it exactly: `gva-founders-playbook`
Set to **Public**. Do NOT initialize with README (we already have one).

### Step 2 — Push from this folder

```bash
cd "/Users/admin/Downloads/0｜Other/gva-founders-playbook"
git remote add origin https://github.com/vincentt-wang/gva-founders-playbook.git
git branch -M main
git push -u origin main
```

### Step 3 — Enable GitHub Pages

On GitHub: Settings → Pages → Source: `Deploy from a branch` → Branch: `main` / `/ (root)` → Save

Your site will be live at:
`https://vincentt-wang.github.io/gva-founders-playbook/`
(takes ~2 minutes to propagate)

## Password

Curriculum unlock password: `founders2026`

## TODO before production

- [ ] Replace testimonial with real founder quote
- [ ] Add real OG image (1200×630px) at `/og-image.png`
- [ ] Connect form to systeme.io webhook (see `// TODO` comment in index.html)
- [ ] Update social media links (LinkedIn, Twitter)
- [ ] Replace `vincentt-wang` with actual GitHub username if different

## Content credits

- Methodology: Vincent Wang
- IP Owner: Bonhope Capital / GVA
