# CLAUDE.md — TapleySignsWebsite

## 1. Project Overview

Tapley Signs is a Dublin, Ireland sign-making company, family-run since 2004. This repository is a **static GitHub Pages website** with no build step, no Node.js, and no package manager. Everything is plain HTML, CSS, and JavaScript.

**Live site:** Served from `index.html` at the repo root via GitHub Pages.

**File roles:**
- `index.html` — the production page. This is what visitors see.
- `gallery.html` — standalone gallery page, custom CSS (no Bootstrap).
- `home.html`, `Carousel.html`, `fullIndexTemplate.html` — drafts/experiments, not production pages.

**Known gaps in `index.html`:**
- The Services section still has placeholder lorem ipsum copy and generic glyphicon labels (POWER, LOVE, JOB DONE) — these need real content.
- The contact form has no `action` attribute and does nothing when submitted.

---

## 2. Quick Reference — Common Tasks

### Add a new page
1. Copy the entire `<head>` block from `index.html` exactly (all 5 CDN links, viewport meta, charset, favicon links).
2. Copy the `<nav>` block for consistent navigation.
3. Copy the `<footer>` block.
4. Update `<title>` to be page-specific (e.g. `<title>Gallery — Tapley Signs</title>`).
5. Add a link to the new page in the navbar of `index.html` and on the new page itself.

### Add a new service item (Services section)
```html
<div class="col-sm-4 text-center">
  <span class="glyphicon glyphicon-[name] logo-small"></span>
  <h4>SERVICE NAME</h4>
  <p>One or two sentences describing the service.</p>
</div>
```
Find available glyphicon names at: https://getbootstrap.com/docs/3.4/components/#glyphicons

### Add a portfolio carousel category
See Section 10 for the full step-by-step.

### Update the navbar
- Same-page anchor links: `href="#sectionid"`
- Links to other pages: `href="gallery.html"` (relative, no leading slash)
- Keep labels short — the existing letter-spacing/uppercase style is set by `.navbar a { letter-spacing: 4px; }` in `index.html`

---

## 3. Tech Stack and CDN Conventions

### Required CDN load order — reproduce this in every page `<head>`:
```html
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css">
<link href="https://fonts.googleapis.com/css?family=Montserrat" rel="stylesheet" type="text/css">
<link href="https://fonts.googleapis.com/css?family=Lato" rel="stylesheet" type="text/css">
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"></script>
```

For performance, add these preconnect hints before the CDN links:
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
```

### Hard rules
- **Never introduce npm, package.json, webpack, Vite, Parcel, or any build tooling.** The project's simplicity is intentional.
- **Never upgrade Bootstrap or jQuery versions** without explicit instruction. Bootstrap 3 → 5 is a breaking change (grid classes, component API, Glyphicons removed).
- **Never add Font Awesome, Heroicons, or other icon libraries.** Bootstrap 3.4.1 Glyphicons are available and in use.
- **Never add new CDN libraries** (Tailwind, Alpine.js, GSAP, etc.) without being asked.
- jQuery is already loaded — use it. No need for `document.querySelector` workarounds.

---

## 4. Branding Guidelines

### Colors
| Usage | Value |
|-------|-------|
| Primary brand blue | `#1e8df4` |
| Dark headings | `#303030` |
| Body text | `#818181` |
| Grey section backgrounds | `#f6f6f6` |
| White (panels, button hover) | `#ffffff` |

### Typography
- **Montserrat** — navbar links, jumbotron/hero headings, section headings. Letter-spacing: 4px in navbar.
- **Lato** — all body copy. `font: 400 15px Lato, sans-serif`, `line-height: 1.8`
- `h2`: 24px, uppercase, `#303030`, `font-weight: 600`, `margin-bottom: 30px`
- `h4`: 19px, `line-height: 1.375em`, `#303030`, `font-weight: 400`, `margin-bottom: 30px`

### Voice and tone
- Professional but approachable — this is a family business, not a corporate enterprise.
- Be **specific**, not vague. "Installation of high-quality graphics for Primark, Intel, and Aviva" is better than "working with top brands nationwide".
- Avoid superlatives and hype. Named clients speak louder than marketing adjectives.
- Dublin, Ireland identity — mention location naturally where it adds credibility.
- The About Us paragraph in `index.html` is the canonical tone reference for new copy.

### Confirmed clients (never invent others)
Primark, Aviva, Intel, Brown Thomas, Bord Bia, Dyson, OPW, RTE, Vodafone

### Confirmed services
In-store graphics, vinyl banners, mesh banners, window graphics, building wraps, lightboxes, stickers, construction signage, installation.

---

## 5. File Structure and GitHub Pages Rules

```
/
├── index.html                    ← production entry point
├── gallery.html
├── home.html                     ← draft, not linked
├── Carousel.html                 ← draft
├── fullIndexTemplate.html        ← draft
├── CLAUDE.md
├── README.md
└── Images/
    ├── Building.jpg
    ├── Building Smaller.jpg
    ├── Tapley Signs Sign.jpg
    ├── 770x578/                  ← portfolio images (4:3, 770×578px)
    │   ├── 3.jpg
    │   ├── Brown Thomas 1.jpg
    │   ├── Brown Thomas 2.jpg
    │   ├── Dyson 1.jpg
    │   ├── Building Wraps/
    │   │   ├── Bloom.jpg
    │   │   ├── Intel 1.jpg
    │   │   └── Pop.jpg
    │   ├── Mesh Banners/
    │   │   ├── Aviva 1.jpg
    │   │   ├── Aviva 2.jpg
    │   │   └── Aviva 3.jpg
    │   └── Window Graphics/
    │       ├── Bord Bia.jpg
    │       ├── Marvel Room.jpg
    │       ├── Primark 1.jpg
    │       ├── Primark 2.jpg
    │       └── Primark 3.jpg
    ├── Logos/
    │   ├── Aviva_Colour.png
    │   ├── Aviva_Grey.png
    │   ├── Brown Thomas_Colour.png
    │   ├── Primark_Colour.png
    │   ├── Primark_Grey.png
    │   ├── Logo_no_ring.png
    │   ├── Logo_ring.png
    │   └── Grayscale/
    │       ├── Aviva.png
    │       ├── Bord Bia.png
    │       ├── Brown Thomas.png
    │       ├── Dyson.png
    │       ├── Intel.png
    │       ├── OPW.png
    │       ├── Primark.png
    │       ├── RTE.png
    │       └── Vodafone.png
    └── X Icons/
        ├── Favicon.png
        └── apple touch icon.png
```

### GitHub Pages path rules
- Paths are **case-sensitive** on GitHub Pages (Linux servers) even though Windows development is not. `Images/Building%20Smaller.jpg` is correct; `images/building smaller.jpg` will 404 in production.
- Use `%20` for spaces in file paths within HTML attributes: `src="Images/Building%20Smaller.jpg"`
- The `index.html` at the repo root is the required entry point — do not rename it.

### Adding new portfolio images
- Place in `Images/770x578/[CategoryName]/` using the naming convention `Client Name 1.jpg`
- Target dimensions: **770×578px** (approximately 4:3 ratio) — crop or resize new images to match
- New client logos: add both Colour and Grayscale variants to `Images/Logos/`

### GitHub Pages limitations
- No server-side processing. No PHP, Node.js, or Python backends.
- Contact forms must use a third-party service — see Section 9.
- All dependencies must be via CDN or committed to the repo — no npm installs at runtime.

---

## 6. Design and Layout Guidelines

### Single-page scroll pattern
`index.html` uses Bootstrap's `data-spy="scroll"` with anchor-linked navbar items. New homepage sections must:
1. Have a unique `id` on the container (e.g. `id="clients"`)
2. Have a corresponding `<li><a href="#clients">Clients</a></li>` added to the navbar

### Section structure
- **White sections**: bare `.container-fluid` with `padding: 60px 50px`
- **Grey sections**: `.container-fluid.bg-grey` (background: `#f6f6f6`)
- Alternate white/grey — current order: navbar (blue) → jumbotron (blue) → About (white) → Services (white) → Portfolio (grey) → Contact (grey)
- Section heading pattern: `<h2>SECTION TITLE</h2>` followed by a `<hr>` then content

### Hero/Jumbotron
```html
<div class="jumbotron text-center">
  <h1>HEADING TEXT</h1>
  <p>Subtitle text here.</p>
  <p><a href="#section" class="btn btn-default btn-lg">Button Label</a></p>
</div>
```
The `.jumbotron` class applies `background-color: #1e8df4; color: #fff; padding: 100px 25px; font-family: Montserrat`.

### Scroll reveal animation
Add `class="row slideanim"` to any new content row and it will automatically animate in when scrolled into view (the `.slideanim`/`.slide` jQuery handler is already in `index.html`).

### Bootstrap 3 grid patterns in use
- 3-column layout: `col-sm-4` (used in Services and Portfolio sections)
- 2-column layout: `col-sm-8` + `col-sm-4` (used in About section)
- Always wrap columns in a `<div class="row">`

### What NOT to do
- Do not use CSS Grid or Flexbox as the primary layout mechanism — Bootstrap 3's float-based grid is established and adding Grid/Flexbox would require careful isolation.
- Do not use Bootstrap 4/5 utility classes (`d-flex`, `mb-3`, `text-muted`, etc.) — they don't exist in Bootstrap 3.4.1.
- Do not add another `position: fixed` element beyond the existing navbar.
- Do not use `vh` units for jumbotron height — padding-based height is the established pattern.
- Do not use CSS custom properties (`--color: ...`) — the project targets older browser compatibility via Bootstrap 3.

---

## 7. Code Quality Standards

### CSS
- All custom styles go in the `<style>` block inside `<head>`. **Do not create separate `.css` files.**
- Do not use `style=""` inline attributes for anything reusable — define a class in the `<style>` block instead.
- One-off overrides (e.g. `style="margin-top: 20px"` on a single element) are acceptable.
- Add new media queries to the existing `@media` blocks at the bottom of the `<style>` section — do not scatter breakpoints.
- Primary breakpoints already in use: `768px` (tablet), `480px` (mobile).

### JavaScript
- Custom JS goes in a `<script>` block at the bottom of `<body>`, before `</body>`.
- Wrap all jQuery code in `$(document).ready(function() { ... })` as the existing pattern shows.
- Do not use ES6 modules, `import`/`export`, or `async`/`await`.
- Do not add `<script type="module">` tags.
- Vanilla `document.querySelector` is fine for simple one-off DOM reads; use jQuery for anything involving event handling or animation.

### Accessibility
- Every `<img>` must have a meaningful `alt` attribute. Describe what's in the image: `alt="Primark window graphics installation, Dublin"` not `alt="image"` or `alt=""`.
- Form inputs must have associated `<label>` elements or at minimum a descriptive `placeholder`.
- Preserve `class="sr-only"` text on carousel controls (already present) — do not remove screen-reader-only text.
- White text on `#1e8df4` blue passes WCAG AA contrast — do not introduce color combinations that reduce this.

### SEO
- Every page needs a unique, descriptive `<title>`: `<title>Sign Installation Services — Tapley Signs Dublin</title>`
- Add `<meta name="description" content="...">` to every page, 150–160 characters, describing that specific page.
- The `lang="en"` attribute on `<html>` is required — maintain it on all pages.
- `<h1>` appears exactly once per page.
- Image `alt` text is also an SEO signal — describe content specifically.

### HTML structure
- Use semantic elements where natural: `<nav>`, `<footer>`, `<section>`, `<main>`.
- Section comments like `<!-- Container (About Section) -->` are the established convention — add them when creating new sections.
- Use HTML entities for special characters: `&amp;`, `&mdash;`, `&copy;`.

---

## 8. Web Research Workflow

Use the `WebFetch` tool to research competitor and reference websites before building new content.

### When to research
- Before building a new page section or feature — fetch 2–3 reference sites first.
- When you need copy for a service Tapley Signs offers but have no existing text — fetch industry competitors to understand how they describe it.
- When the user says "make it look like X" or "research how others do Y".
- When adding a new service category — research to understand standard naming, typical descriptions, and common CTAs in the signage industry.

### Research workflow — follow in order
1. **Fetch the target site's homepage** — understand their structure, key messaging, and calls to action.
2. **Fetch their services or about page** — gather copy patterns and service descriptions.
3. **Summarise findings in a short bullet list** before writing any code.
4. **Confirm the direction with the user** if the research points toward a significant design or copy change.
5. Only then write code, using the research to inform the content.

### What to extract from a fetched page
- `<h1>` and `<h2>` text — reveals how they position their business
- Navigation labels — reveals what pages/services they consider primary
- CTA button text — "Get a Quote", "Request a Callback", "View Our Work", etc.
- Service names and how they're categorised
- Footer content — phone format, email, address patterns
- Any testimonials or client lists

### WebFetch limitations
- CSS and JavaScript **do not execute** via WebFetch — you receive raw HTML. Extract text content and semantic structure, not visual design details.
- Many modern sites are React/Vue SPAs — the fetched HTML may be mostly `<div id="root"></div>` with no useful content. Note this and try a different source.
- Do not attempt to fetch image files via WebFetch.
- If a site returns a 403 or bot-detection page, move on — do not retry.

### Useful reference points
- Bootstrap 3.4 documentation (for component API): `https://getbootstrap.com/docs/3.4/`
- Bootstrap 3.4 Glyphicon list: `https://getbootstrap.com/docs/3.4/components/#glyphicons`

---

## 9. Contact Form and GitHub Pages Limitations

The contact form in `index.html` currently has **no `action` attribute and does nothing**. This is a known gap.

### Recommended fix — Formspree (free tier, no backend required)
```html
<form action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
```
The user needs to create a free account at formspree.io to get a form ID. Once set, submissions arrive by email.

### Alternative — mailto link
Replace the form entirely with a direct email CTA:
```html
<a href="mailto:infotapleys@gmail.com" class="btn btn-default btn-lg">Email Us</a>
```

### Never suggest
- PHP `mail()` functions
- Node.js or Express backends
- Python/Django/Flask
- Any server-side processing

These cannot run on GitHub Pages, which serves only static files.

---

## 10. Adding New Portfolio Work

### Add a new portfolio category (e.g. "Floor Graphics")

**Step 1 — Images**
Create the directory `Images/770x578/Floor Graphics/` and add images named `Client Name 1.jpg`, `Client Name 2.jpg`, etc. Resize/crop to 770×578px.

**Step 2 — Carousel HTML**
Copy an existing carousel block from the Portfolio section in `index.html`. Give it a **unique `id`**:

```html
<div class="col-sm-4">
  <div id="myCarouselFloorGraphics" class="carousel slide" data-ride="carousel">
    <!-- Indicators -->
    <ol class="carousel-indicators">
      <li data-target="#myCarouselFloorGraphics" data-slide-to="0" class="active"></li>
      <li data-target="#myCarouselFloorGraphics" data-slide-to="1"></li>
    </ol>
    <!-- Wrapper for slides -->
    <div class="carousel-inner" role="listbox">
      <div class="item active">
        <img src="Images/770x578/Floor%20Graphics/Client%20Name%201.jpg" alt="Floor graphics installation for Client Name" width="770" height="578">
      </div>
      <div class="item">
        <img src="Images/770x578/Floor%20Graphics/Client%20Name%202.jpg" alt="Floor graphics installation for Client Name" width="770" height="578">
      </div>
    </div>
    <!-- Left and right controls -->
    <a class="left carousel-control" href="#myCarouselFloorGraphics" role="button" data-slide="prev">
      <span class="glyphicon glyphicon-chevron-left" aria-hidden="true"></span>
      <span class="sr-only">Previous</span>
    </a>
    <a class="right carousel-control" href="#myCarouselFloorGraphics" role="button" data-slide="next">
      <span class="glyphicon glyphicon-chevron-right" aria-hidden="true"></span>
      <span class="sr-only">Next</span>
    </a>
  </div>
  <p><strong>Floor Graphics</strong></p>
</div>
```

**Critical:** Every `data-target`, `href`, and `id` inside the carousel block must reference the **same unique id**. Mixing ids from different carousels causes them to control each other.

**Step 3 — Layout adjustment**
- 3 categories: `col-sm-4` each (current layout — no change needed)
- 4 categories: switch to `col-sm-6` for 2×2 grid, or add a second `<div class="row slideanim">`
- 6 categories: two rows of three `col-sm-4`

### Add client logos to a clients section
Use the grayscale logos from `Images/Logos/Grayscale/` — available for: Aviva, Bord Bia, Brown Thomas, Dyson, Intel, OPW, Primark, RTE, Vodafone.

Display pattern: greyscale by default, colour on hover:
```css
.client-logo {
  filter: grayscale(100%);
  opacity: 0.6;
  transition: filter 0.3s, opacity 0.3s;
}
.client-logo:hover {
  filter: grayscale(0);
  opacity: 1;
}
```
