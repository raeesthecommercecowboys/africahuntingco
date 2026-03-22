# Africa Hunting Co — Project Context
**Site:** africahuntingco.com  
**Repo:** raeesthecommercecowboys/africahuntingco  
**Hosting:** Cloudflare Pages (auto-deploys from GitHub, ~60s)  
**Pipeline:** Edit here → GitHub Desktop (commit/push) → Live  
**Form endpoint:** https://formspree.io/f/mlgpzjbg  

---

## Tech Stack

- **Pure HTML5 + CSS + vanilla JS** — no frameworks, no build tools, no npm
- **No CMS, no WordPress, no React** — every page is a standalone `.html` file
- **Fonts:** Google Fonts — Cormorant Garamond + Barlow + Barlow Condensed (loaded via CDN link in `<head>`)
- **Analytics:** Cloudflare Web Analytics beacon (already in every page, do not remove)
- **Hosting:** Cloudflare Pages — static files only

---

## File & Folder Structure

```
/
├── index.html                        ← Homepage (LIVE — do not restructure)
├── sitemap.xml                       ← Update whenever a new page is added
├── CNAME / _redirects                ← Cloudflare routing (do not touch)
│
├── cape-buffalo-hunting/
│   └── index.html
├── plains-game-safari/
│   └── index.html
├── hunting-safari-south-africa/
│   └── index.html
├── halaal-safari-hunting/
│   └── index.html
├── bow-hunting-south-africa/
│   └── index.html
│
├── phasa-cites-compliance/
│   └── index.html
├── trophy-export-guide/
│   └── index.html
├── south-africa-hunting-seasons/
│   └── index.html
│
├── de/
│   └── jagdsafari-sudafrika/
│       └── index.html
├── fr/
│   └── chasse-safari-afrique-du-sud/
│       └── index.html
├── no/
│   └── jakt-safari-sor-afrika/
│       └── index.html
├── da/
│   └── jagtsafari-sydafrika/
│       └── index.html
├── ar/
│   └── رحلات-صيد-جنوب-افريقيا/
│       └── index.html
│
└── assets/
    ├── css/         ← shared styles if extracted (currently inline per page)
    └── images/      ← all images go here with descriptive filenames
```

Every page lives in its own folder with an `index.html`. This gives clean URLs without `.html` extensions (e.g. `/cape-buffalo-hunting/` not `/cape-buffalo-hunting.html`).

---

## Design System (DO NOT DEVIATE)

These CSS variables are established on the homepage and must be used on every page:

```css
:root {
  --earth: #1a1410;   /* Page background — darkest */
  --bark:  #2c2018;   /* Section background — dark brown */
  --sand:  #c9a96e;   /* Primary accent — gold/sand */
  --dust:  #e8d5b0;   /* Hover state for sand elements */
  --ivory: #f5efe4;   /* Primary text */
  --blood: #8b1a1a;   /* Reserve — do not use unless specified */
  --sage:  #4a5240;   /* CTA band background */
  --sky:   #d4cfc8;   /* Secondary/muted text */
  --white: #faf8f4;   /* Near-white */
}
```

**Typography:**
- Headings: `Cormorant Garamond` (serif, italic for emphasis)
- UI / labels / nav: `Barlow Condensed` (condensed, uppercase, letter-spaced)
- Body copy: `Barlow` (300 weight for body, 400–600 for emphasis)

**Never introduce:** Bootstrap, Tailwind, Material UI, or any CSS framework. All styling is custom.

---

## SEO Rules — CRITICAL

Every page must include all of the following. Do not omit any item.

### 1. `<head>` meta block
```html
<meta name="robots" content="index, follow, max-image-preview:large, max-snippet:-1, max-video-preview:-1" />
<link rel="canonical" href="https://www.africahuntingco.com/[page-path]/" />
<meta name="geo.region" content="ZA-GP" />
<meta name="geo.placename" content="Johannesburg, Gauteng, South Africa" />
<meta name="geo.position" content="-26.2041;28.0473" />
<meta name="ICBM" content="-26.2041, 28.0473" />
```

### 2. Open Graph + Twitter Card
All pages must have full OG and Twitter Card tags. Use the page's unique title and description — do not copy the homepage values.

### 3. JSON-LD Schema — Multiple separate `<script>` blocks
Follow the Tony Peacock / LinkDaddy entity-based SEO methodology:
- **Do NOT combine all schema into one block** — use multiple separate `<script type="application/ld+json">` tags
- Every page gets: WebSite reference + Organization reference + WebPage block + FAQPage block (if FAQs present)
- Content pages get DefinedTerm blocks with `sameAs` linking to Wikipedia and Wikidata
- Location pages get Place entities with Wikidata `sameAs`
- The SEO copy, schema content, and FAQ questions are provided by the project owner — do not generate schema content yourself

### 4. hreflang (language pages only)
Language pages (`/de/`, `/fr/`, `/no/`, `/da/`, `/ar/`) must include:
```html
<link rel="alternate" hreflang="[lang]" href="https://www.africahuntingco.com/[lang]/[slug]/" />
<link rel="alternate" hreflang="en" href="https://www.africahuntingco.com/[english-equivalent]/" />
<link rel="alternate" hreflang="x-default" href="https://www.africahuntingco.com/" />
```

### 5. Heading hierarchy
- One `<h1>` per page only
- `<h2>` for major sections
- `<h3>` for subsections and FAQ questions
- Never skip levels

### 6. Image rules
- All images in `/assets/images/`
- Descriptive filenames: `cape-buffalo-hunting-limpopo-south-africa.jpg` not `image1.jpg`
- Every `<img>` must have a descriptive `alt` attribute
- Use `loading="lazy"` on all images below the fold
- Use `loading="eager"` + `fetchpriority="high"` on hero images

---

## Page Template Structure

Every page follows this section order:

```
1. <head> — full meta, canonical, OG, Twitter, schema scripts, font imports
2. <nav> — fixed navigation matching homepage
3. <section class="hero"> — page-specific hero
4. <section> — main content (varies by page type)
5. <section class="faq-section"> — FAQ section (if applicable)
6. <section class="cta-section"> — request a package CTA
7. <footer> — matching homepage footer
8. <div class="footer-bottom"> — copyright bar
9. <script> — form handling only (if contact form present)
10. Cloudflare analytics beacon
```

---

## Navigation (Copy Exactly)

The nav must match across all pages. Current nav links:

```html
<nav>
  <a href="/" class="nav-logo">Africa Hunting <span>Co</span></a>
  <ul class="nav-links">
    <li><a href="/plains-game-safari/">Plains Game</a></li>
    <li><a href="/cape-buffalo-hunting/">Cape Buffalo</a></li>
    <li><a href="/bow-hunting-south-africa/">Bow Hunting</a></li>
    <li><a href="/hunting-safari-south-africa/">Safari Hunting</a></li>
    <li><a href="/south-africa-hunting-seasons/">Seasons</a></li>
  </ul>
  <a href="/#request" class="nav-cta">Request a Package</a>
</nav>
```

Update this nav across all pages when new top-level pages are added.

---

## Contact Form

The homepage form uses Formspree. Endpoint: `https://formspree.io/f/mlgpzjbg`

Standard submission handler (copy to any page with a form):

```javascript
async function handleSubmit(e) {
  e.preventDefault();
  const form = document.getElementById('huntForm');
  const btn = form.querySelector('.form-submit');
  btn.textContent = 'Sending...';
  btn.disabled = true;
  try {
    const res = await fetch('https://formspree.io/f/mlgpzjbg', {
      method: 'POST',
      body: new FormData(form),
      headers: { 'Accept': 'application/json' }
    });
    if (res.ok) {
      form.style.display = 'none';
      document.getElementById('formSuccess').style.display = 'block';
    } else {
      btn.textContent = 'Something went wrong — please try again';
      btn.disabled = false;
    }
  } catch {
    btn.textContent = 'Something went wrong — please try again';
    btn.disabled = false;
  }
}
```

---

## Sitemap

`sitemap.xml` must be updated every time a new page is added. Format:

```xml
<url>
  <loc>https://www.africahuntingco.com/[page-path]/</loc>
  <changefreq>monthly</changefreq>
  <priority>0.8</priority>
</url>
```

Priority guide:
- Homepage: `1.0`
- Core commercial pages: `0.9`
- Location + species pages: `0.8`
- Informational pages: `0.7`
- Language pages: `0.8`

---

## What Antigravity Should NOT Do

- Do not generate SEO copy, page copy, or schema content — this comes from the project owner
- Do not change the colour palette or typography system
- Do not introduce CSS frameworks or JS libraries
- Do not restructure the homepage (`index.html`)
- Do not modify the Cloudflare analytics beacon
- Do not add pages for: leopard hunting, lion hunting, rhino hunting
- Do not combine multiple JSON-LD schema blocks into one
- Do not use `.html` extensions in internal links — always use trailing-slash folder URLs

---

## Build Queue (Current)

Pages to build next, in order. Full copy + schema provided by project owner before build starts.

| Priority | URL | Status |
|---|---|---|
| 1 | `/cape-buffalo-hunting/` | Copy + schema ready — BUILD |
| 2 | `/plains-game-safari/` | Planned |
| 3 | `/hunting-safari-south-africa/` | Planned |
| 4 | `/halaal-safari-hunting/` | Planned |
| 5 | `/de/jagdsafari-sudafrika/` | Planned |
| 6 | `/phasa-cites-compliance/` | Planned |
| 7 | `/trophy-export-guide/` | Planned |
| 8 | `/south-africa-hunting-seasons/` | Planned |

---

*This file is the master build reference for Antigravity. SEO strategy, keyword research, and schema content are managed separately. When in doubt, ask before building.*
