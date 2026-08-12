---
name: web-quick-builder
description: Builds or restyles complete, responsive websites in a single HTML file using Puzzle Grid, Bold Editorial, or Street Archive visual systems. Use when someone asks for a website, landing page, homepage, portfolio, product page, event page, community site, 官網, 個人網站, 產品頁, 一頁式網站, 作品集, 活動頁, or a redesign of an existing page.
---

# Web Quick Builder

Build a polished, accessible website with no setup. Default to one HTML file with inline CSS and JavaScript; use external files or a framework only when the requirements genuinely need them.

## Workflow

### 1. Collect the material

If the conversation does not already contain enough material, ask once for any available copy, brand or person name, product description, CV, links, images, and reference sites. Read supplied files instead of asking the user to repeat them.

Detect the site's language from the material. Traditional Chinese input produces Traditional Chinese copy while preserving brand names and established English technical terms.

### 2. Ask three decisions

Ask these questions **one at a time in this order**, using the available interactive question tool. Wait for each answer before asking the next. Do not start template selection, copywriting, or implementation until all three are answered.

1. **Primary visitor goal** (single choice): contact/book/inquire; buy/register; view work/learn about the subject; read/subscribe/join; informational display.
2. **Visual system** (single choice): Puzzle Grid (colorful modular collage); Bold Editorial (oversized type and whitespace); Street Archive (tactile street collage). Include a one-line description and suitable use cases.
3. **Required sections**: ask for any combination of hero/media; services/features; work/cases/items; pricing; FAQ; contact/CTA; about; schedule/details; resources/content. Use multi-select when available; otherwise accept a comma-separated freeform answer without splitting it into more questions.

Infer palette, copy tone, exact optional sections, and page count from the answers and supplied material. If an answer conflicts with the material, make the smallest reasonable assumption and disclose it after delivery.

### 3. Load constraints

Read files in this order:

1. `architecture.md` for goal-driven information architecture and output format.
2. The selected `*.manifest.json` for visual constraints, content limits, asset slots, and supported sections.
3. `three-template-preview.html` for visual language and responsive component patterns.
4. `build-checklist.md` and `skeleton.html` for technical, accessibility, SEO, and performance requirements.

Priority when references differ: accessibility and correctness → goal-driven architecture → manifest constraints → preview appearance. The preview is a gallery, not a production DOM or fixed section order.

### 4. Build

Use the goal-specific section order from the manifest. Templates control visual language, not site subject: adapt their components to products, services, events, organizations, communities, content, or portfolios without forcing biography or project sections.

Map supplied assets only to declared manifest slots. For an empty optional slot, use the declared CSS/SVG placeholder; never emit a missing file path. Rewrite copy to fit limits rather than shrinking typography.

Never invent verifiable testimonials, clients, awards, prices, dates, counts, or statistics. Use clearly bracketed placeholders when structurally necessary and list them after delivery. Fictional practice projects may invent content if explicitly identified as fictional.

Write the finished site to the user-requested path. If none was provided, save it as `./<slug>.html` in the current working directory. For an existing page, edit that file unless the user asks for a copy. Run the smallest available validation that covers the generated document.

### 5. Deliver and revise

State the file path, list unresolved placeholders, and give one deployment sentence. On follow-up requests, edit the existing file while preserving confirmed goal, visual system, content, and section choices unless the user changes them.

## Scope boundaries

- Up to five static pages may use separate HTML files with duplicated inline styles.
- Use Astro for larger content collections after explaining the added build step.
- Auth, databases, CMS administration, and server logic require a suitable application stack; do not fake them in static HTML.
- A static shop may link to a real hosted checkout. A static contact form must use a configured provider or a real `mailto:` action.
