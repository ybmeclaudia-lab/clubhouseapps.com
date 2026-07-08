# ClubhouseApps.com — Complete Site Guide

Everything an AI (or human) needs to understand, maintain, and update this website.

---

## Overview

**clubhouseapps.com** is the public website for Clubhouse Apps, an indie iOS studio. It currently serves two purposes:

1. **Company homepage** — introduces Clubhouse Apps, lists current and upcoming apps
2. **DinnerPilot product page** — marketing landing page for the DinnerPilot iOS app

The site is pure static HTML and CSS. No JavaScript frameworks, no build tools, no package manager. Every file you see is exactly what gets served to the browser.

---

## Hosting

### GitHub Pages

The site is hosted on **GitHub Pages** — GitHub's free static site hosting service.

- **Repository:** `https://github.com/ybmeclaudia-lab/clubhouseapps.com`
- **Branch:** `main` (GitHub Pages serves directly from this branch)
- **Local path:** `~/Desktop/ClubhouseApps/Website/`

### How deployment works

There is no build step and no CI pipeline. Deployment is:

1. Edit files locally
2. `git add` the changed files
3. `git commit -m "description"`
4. `git push origin main`

GitHub Pages picks up the push automatically and the live site updates within ~60 seconds. No dashboard to open, no deploy button to click.

### Custom domain

The file `CNAME` in the repo root contains `clubhouseapps.com`. This is how GitHub Pages knows to serve the site at that domain instead of the default `ybmeclaudia-lab.github.io` URL.

**DNS is configured separately** (in the domain registrar's DNS settings, not in this repo). The DNS A records point to GitHub Pages' servers. If you need to change the domain, update both the `CNAME` file and the DNS records.

### Email

Contact email referenced throughout the site: `dave@clubhouseapps.com`

---

## Repository

```
clubhouseapps.com/          ← repo root
├── CNAME                   ← custom domain declaration
├── index.html              ← company homepage (clubhouseapps.com/)
├── assets/
│   └── shared.css          ← shared stylesheet used by ALL pages
└── dinnerpilot/
    ├── index.html          ← DinnerPilot product page (/dinnerpilot/)
    ├── privacy/
    │   └── index.html      ← Privacy Policy (/dinnerpilot/privacy/)
    ├── terms/
    │   └── index.html      ← Terms of Service (/dinnerpilot/terms/)
    └── data-deletion/
        └── index.html      ← Data Deletion Request (/dinnerpilot/data-deletion/)
```

URL structure mirrors folder structure exactly. `index.html` files serve as the default for each folder, so `/dinnerpilot/` loads `dinnerpilot/index.html`.

---

## Commit History

| Date | Hash | Description |
|------|------|-------------|
| 2026-05-16 | `5bedc1a` | Initial site — ClubhouseApps.com + DinnerPilot landing page |
| 2026-05-16 | `12f6686` | Create CNAME (added custom domain) |
| 2026-05-17 | `34288cf` | Add Privacy Policy, Terms of Service, Data Deletion pages; update footers |
| 2026-05-17 | `3403e0d` | Move legal pages under /dinnerpilot/ to reflect org structure |
| 2026-05-17 | `9599ff0` | Full visual redesign — modern, premium look |

The major work happened on **2026-05-17**: legal pages were added, then immediately reorganized under `/dinnerpilot/` (they had initially been at the root), then the entire site got a full visual redesign in one large commit that touched all three primary files.

---

## Design System

All visual tokens live in `assets/shared.css`. Every page links to this file. Do not define brand colors or core styles inline — add them here and reference the CSS variables.

### Brand colors

```css
--dp-orange:        #D4713B;   /* Primary brand color — used for CTAs, accents, active states */
--dp-orange-deep:   #B85E2A;   /* Darker orange — used in gradients */
--dp-orange-light:  #F5E6DB;   /* Light orange tint */
--dp-orange-pale:   #FDF4EE;   /* Very pale orange — backgrounds, hover states */
--dp-green:         #3D7A5F;   /* Secondary — "live" badge, success states */
--dp-green-light:   #E8F0EB;   /* Green tint background */
--dp-purple:        #7B6B9E;   /* Accent — used sparingly */
```

### Ink (text) scale

```css
--ink:        #1A1917;   /* Primary text */
--ink-mid:    #4A4845;   /* Body text, descriptions */
--ink-soft:   #8A8885;   /* Secondary labels, captions */
--ink-faint:  #C4C2BE;   /* Placeholders, disabled */
```

### Surfaces and borders

```css
--surface:        #FAFAF8;   /* Page background */
--surface-warm:   #F7F4F0;   /* Slightly warmer background */
--card:           #FFFFFF;   /* Card background */
--card-warm:      #FDFCFA;
--border:         #E8E6E2;
--border-warm:    #E2DDD7;
```

### Shadows (warm-tinted)

```css
--shadow-soft:    0 1px 4px rgba(212,113,59,0.06), 0 2px 10px rgba(0,0,0,0.04);
--shadow-card:    0 2px 16px rgba(212,113,59,0.08), 0 4px 24px rgba(0,0,0,0.06);
--shadow-float:   0 8px 40px rgba(212,113,59,0.15), 0 16px 60px rgba(0,0,0,0.1);
--shadow-orange:  0 8px 32px rgba(212,113,59,0.35);
```

### Border radius

```css
--radius-sm:   8px;
--radius-md:   14px;
--radius-lg:   22px;
--radius-xl:   32px;
```

### Typography classes (defined in shared.css)

| Class | Size | Weight | Usage |
|-------|------|--------|-------|
| `.display` | clamp(2.8rem–4.8rem) | 800 | Hero headlines |
| `.headline` | clamp(1.6rem–2.4rem) | 700 | Section headings |
| `.title` | 1.2rem | 600 | Card titles |
| `.body` | 1.05rem | 400 | Body text |
| `.caption` | 0.875rem | 400 | Small supporting text |
| `.overline` | 0.75rem | 700 | Uppercase labels |

Font: **Inter** (400, 500, 600, 700, 800) loaded from Google Fonts.

### Button classes (defined in shared.css)

| Class | Appearance | Usage |
|-------|-----------|-------|
| `.btn` | Base styles only | Always combine with a variant |
| `.btn-primary` | Orange gradient, white text | Primary CTAs |
| `.btn-outline` | Transparent, orange border | Secondary actions |
| `.btn-dark` | Dark background, white text | Dark-section CTAs |

The DinnerPilot page adds `.btn-sm` (locally) for compact nav buttons and `.btn-pro` for the gold Pro CTA.

### Card class

`.card` — white background, `--radius-lg` corners, `--border`, `--shadow-card`. Used as a base; pages add additional classes on top.

### Layout

`.container` — max-width 1100px, centered, 28px horizontal padding. Applied to section wrappers.

### Nav (shared.css)

`nav` is sticky, top: 0, z-index: 100, with `backdrop-filter: blur(16px)` for the frosted glass effect. `.nav-inner` is the 64px tall flex container inside.

---

## Pages

### `index.html` — Company Homepage

**URL:** `clubhouseapps.com/`

**Sections:**

1. **Nav** — "ClubhouseApps" wordmark (orange `<span>` on the s), links to #apps and #about
2. **Hero** — "CA" monogram watermark, warm radial gradient + dot-grid background, headline "Apps built for real life."
3. **Apps section** — 3-column grid with one live app card (DinnerPilot) and two placeholder cards ("Something New", "In the Works")
4. **About section** — 2-column layout: left is company description, right is 3 value cards (Focused, Private, Polished)
5. **Stats row** — 4 stats: 1 App, $0 VC funding, ∞ Passion, 1 Person
6. **Footer** — copyright, links to DinnerPilot and contact email

**Known issue:** The DinnerPilot card has `class="badge badge-live"` but displays text "Coming Soon". When the app launches on the App Store, change the badge text to "Live" (the styling already uses the green dot).

---

### `dinnerpilot/index.html` — DinnerPilot Product Page

**URL:** `clubhouseapps.com/dinnerpilot/`

**Sections:**

1. **Nav** — back arrow to `/`, DinnerPilot wordmark with 🍽️ icon, "Get Notified" CTA button
2. **Hero** — pulsing orange dot eyebrow, "Your family's meals. Planned in a minute." headline, email capture form (Formspree), CSS phone mockup showing a sample week plan
3. **Features** — 6-column bento grid layout with 5 feature cards: Personalized Meal Plans, Smart Grocery Lists, Budget Tracking, One-Tap Swaps, Likes & Dislikes, Traditions Built In
4. **How it works** — dark card section with 3 numbered steps and an orange connector line
5. **Pro section** — 2-column: left lists Pro features, right is the gold-gradient pricing card ($6.99/mo)
6. **Bottom CTA** — second email capture form
7. **Footer** — copyright, links to all legal pages and contact

**Phone mockup** — the "phone" visible in the hero is pure CSS (no images). It's a `.phone-frame` div styled to look like an iPhone with a dynamic island, side buttons, and a mock weekly plan inside. The dates shown are hardcoded ("May 18–24") — update if they become obviously stale.

**Email capture forms** — there are TWO forms on this page (hero and bottom CTA). Both currently have a placeholder:
```html
action="https://formspree.io/f/REPLACE_WITH_FORMSPREE_ID"
```
**This must be replaced before the page is useful.** Sign up at formspree.io, create a form, and replace both instances of `REPLACE_WITH_FORMSPREE_ID` with the real form ID. Both forms must use the same ID (they go to the same inbox).

---

### `dinnerpilot/privacy/index.html` — Privacy Policy

**URL:** `clubhouseapps.com/dinnerpilot/privacy/`

Standard privacy policy for the DinnerPilot iOS app. References:
- `dave@clubhouseapps.com` as the contact email
- Supabase as the backend/database provider
- Google Sign-In and Apple Sign-In as auth providers
- AdMob for advertising
- Anthropic Claude API for AI features

The stylesheet is referenced as `../../assets/shared.css` (two levels up from `dinnerpilot/privacy/`).

---

### `dinnerpilot/terms/index.html` — Terms of Service

**URL:** `clubhouseapps.com/dinnerpilot/terms/`

Terms of Service for DinnerPilot. References $6.99/month Pro subscription pricing, App Store billing, and Clubhouse Apps as the legal entity.

---

### `dinnerpilot/data-deletion/index.html` — Data Deletion Request

**URL:** `clubhouseapps.com/dinnerpilot/data-deletion/`

Required by Apple App Store guidelines for apps that collect user data. Provides instructions for how users can request deletion of their account and data. References `dave@clubhouseapps.com` for deletion requests.

---

## Relative asset paths by folder depth

Every page links to `shared.css`. The path changes by folder depth:

| Page location | shared.css path |
|--------------|-----------------|
| `index.html` (root) | `assets/shared.css` |
| `dinnerpilot/index.html` | `../assets/shared.css` |
| `dinnerpilot/privacy/index.html` | `../../assets/shared.css` |
| `dinnerpilot/terms/index.html` | `../../assets/shared.css` |
| `dinnerpilot/data-deletion/index.html` | `../../assets/shared.css` |

If you add a new page, adjust the path accordingly.

---

## Adding a new app

When Clubhouse Apps ships a second app, the homepage needs two things:

1. **Replace a placeholder card** in the `apps-grid` with a real app card. The placeholder cards use `.app-card-placeholder` class which grays them out. A live card uses just `.app-card` plus `.card`.

2. **Create a new subfolder** at the root level (e.g. `newappname/`) with its own `index.html` landing page, and legal pages under `newappname/privacy/`, `newappname/terms/`, `newappname/data-deletion/`.

3. **Update the footer** on `index.html` to link to the new app.

The grid is `grid-template-columns: 1fr 1fr 1fr` so three cards fill the row evenly. At ≤860px it collapses to single column.

---

## What to update when DinnerPilot launches

- [ ] `index.html` — change DinnerPilot badge text from "Coming Soon" → "Live"
- [ ] `index.html` — stats row "1 App in the App Store" is already correct but verify
- [ ] `dinnerpilot/index.html` — replace both `REPLACE_WITH_FORMSPREE_ID` with the real Formspree form ID
- [ ] `dinnerpilot/index.html` — consider updating the hero eyebrow from "iOS App — Coming Soon" to a real App Store badge/link
- [ ] `dinnerpilot/index.html` — the "Get Notified at Launch" Pro card CTA can become a real App Store link
- [ ] Phone mockup dates — "May 18–24" hardcoded in the mockup; update if stale

---

## Making changes — workflow

```bash
# Navigate to the site folder
cd ~/Desktop/ClubhouseApps/Website

# Make your edits to HTML/CSS files

# Stage and commit
git add index.html dinnerpilot/index.html   # list changed files explicitly
git commit -m "Brief description of what changed"

# Push to deploy
git push origin main
```

The site goes live at clubhouseapps.com within about 60 seconds of the push.

**Never use `git add .` or `git add -A`** — it can accidentally commit `.DS_Store` files or other junk. Always stage named files.

---

## Third-party services referenced

| Service | Purpose | Where referenced |
|---------|---------|-----------------|
| **GitHub Pages** | Hosting | CNAME file + GitHub repo settings |
| **Formspree** | Email capture form submissions | `dinnerpilot/index.html` — two `<form action>` attributes |
| **Google Fonts** | Inter typeface | `<link>` in `<head>` of every page |
| **Supabase** | App backend (mentioned in Privacy Policy only) | `dinnerpilot/privacy/index.html` |
| **AdMob** | App advertising (mentioned in Privacy Policy only) | `dinnerpilot/privacy/index.html` |
| **Anthropic Claude** | App AI features (mentioned in Privacy Policy only) | `dinnerpilot/privacy/index.html` |

---

## Notes for AI agents updating this site

- **No build step.** Edit `.html` and `.css` files directly. What you write is what ships.
- **shared.css is global.** A change there affects every page. Test changes against all pages before committing.
- **Inline styles exist.** Some one-off styles are written inline in `<style>` blocks within each HTML file. This is intentional — they're page-specific. Only move something to `shared.css` if it's genuinely reused across pages.
- **The phone mockup is CSS-only.** Don't try to replace it with an image unless explicitly asked. The CSS mock is intentional and renders consistently.
- **Legal page content is deliberate.** Don't rewrite Privacy Policy or Terms content without being asked — those have specific legal obligations.
- **The Formspree placeholder is broken.** Until `REPLACE_WITH_FORMSPREE_ID` is replaced, form submissions go nowhere. This is a known pending task.
- **Copyright year is 2026.** Update annually.
