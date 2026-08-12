# Architecture — 每個網站都適用的部分

Read this before the selected manifest and preview. This file determines what to build and in what order; the template controls visual language, not the website's subject or information architecture.

## Template role

Puzzle Grid, Bold Editorial, and Street Archive are general visual systems. Any of them may present a product, service, event, organization, community, publication, or person when the content fits the style. Do not force portfolio concepts such as biography, experience, or projects into unrelated sites.

Choose section order from the visitor goal below. Then map each section to the selected manifest's component language. If a preview composition conflicts with semantic order, accessibility, or the chosen visitor goal, preserve its visual character while changing the DOM and section structure.

## Choosing the output format

Default to **one single-file HTML document**. Inline CSS and JavaScript remove build-time dependencies. Remote fonts are optional enhancements and must have suitable system fallbacks, so the page remains usable offline.

Escalate only for real reasons:

| Situation | Format |
|---|---|
| One page, any complexity | Single `.html` |
| 2–5 pages, shared header/footer | Separate `.html` files, same inline `<style>` duplicated in each |
| Content collections (blog, docs, many products) | Astro scaffold — explain the tradeoff before doing it |
| Needs auth, a database, or server logic | Say so plainly and scope down, or hand off to a framework |

Duplicating a `<style>` block across four pages feels wrong but costs nothing: it gzips away, and it beats introducing a build step for a site that will be edited twice a year.

## Section anatomy by goal

Every section does exactly one job for one decision the visitor is making. When two sections compete for the same job, the visitor hesitates and the page underperforms. Order the page by the answer to Q1:

**聯絡／預約／詢價**
hero → 服務或專長 → 實績或案例 → 信任訊號 → 聯絡（大而明確）
The CTA repeats at hero, mid-page, and footer. Same wording all three times.

**購買／註冊**
hero → 解決什麼問題 → 怎麼運作（3 步） → 特色（bento 最適合這裡） → 價格 → FAQ → 最終 CTA
FAQ near the bottom is where objections get answered. Real objections, not marketing questions.

**看作品／了解我是誰**
hero → 精選作品（大） → 其餘作品 → 關於 → 聯絡
Work first, biography second. Nobody arrives wanting the biography.

**讀內容／訂閱／社群**
hero（觀點，不是介紹） → 精選內容 → 內容清單 → 關於 → 訂閱
The subscribe box needs one field. Every extra field costs sign-ups.

**純資訊展示**
hero → 重點摘要 → 分區內容 → 延伸資源
No CTA pressure. The job is comprehension, so favor scannable structure over persuasion.

### The first screen

One focused headline, one supporting line that names the concrete outcome, one confidence cue, one primary action. That's the whole budget. Most first-screen failures come from stacking three claims in the same space — the visitor remembers none of them.

The headline names what this is and who it's for. The supporting line says what changes for them. The confidence cue is whatever's true and checkable: years operating, a real client name they gave you, an open-source star count, a location. If there's no honest confidence cue, leave it out rather than manufacturing one.

### Trust placement

Put trust signals next to friction, not in a testimonial ghetto at the bottom. A price is friction — put the guarantee beside it. A contact form is friction — put the response-time promise above it.

## Modern CSS platform

These shipped across browsers in 2025–2026 and replace most of what JS libraries used to do. Use them, with fallbacks where support is still landing.

**Scroll-driven animations** — `animation-timeline: view()` gives reveal-on-scroll with zero JavaScript, running on the compositor rather than the main thread. Support is roughly 84% (Chrome 115+, Edge 115+, Firefox 132+, Safari 18+), so gate it and keep IntersectionObserver as the fallback path:

```css
@supports (animation-timeline: view()) {
  [data-reveal] {
    animation: reveal linear both;
    animation-timeline: view();
    animation-range: entry 10% cover 32%;
  }
}
```

Animate only `transform` and `opacity`. Animating `width`, `height`, or `margin` forces layout on every frame and undoes the benefit. Don't set `will-change` preemptively — the browser promotes layers on its own.

**Container queries** — universal support now. Any component that should adapt to *its container* rather than the viewport (a card that sits in both a wide grid cell and a narrow sidebar) uses `container-type: inline-size` and `@container`. This is what makes bento cells work at every breakpoint without a pile of media queries.

**`:has()`** — style a parent from its children. Useful for "card that contains an image gets different padding" without adding classes.

**`color-mix()` and `oklch()`** — derive hover and border colors from one accent token instead of hand-picking five hex values. `color-mix(in oklch, var(--accent) 12%, transparent)` for tints stays perceptually even in a way `rgba()` doesn't.

**View Transitions** — only relevant for multi-page builds. `@view-transition { navigation: auto; }` gives cross-document transitions in supporting browsers and degrades to a normal navigation elsewhere. One line, no downside.

**`text-wrap: balance`** on headlines and `text-wrap: pretty` on body copy. Two declarations that make typography look considered.

## Trends worth following, and the ones that aren't

From current practice, the things that reliably improve a page:

- **Bento / modular layout** where content genuinely varies in importance. Size encodes hierarchy, which means uniform cells defeat the purpose — that's just a card wall with rounded corners. Cap it at 5–7 cells per grid; past a dozen, the organizing benefit inverts.
- **Typography as the primary structure.** Viewport-scaled display type and variable fonts carry a page with no imagery at all, which is also the lightest thing you can ship.
- **Off-black and off-white instead of `#000` / `#FFF`.** Pure-black-on-pure-white edges cause visual vibration that's genuinely uncomfortable for readers with astigmatism. Charcoal on cream costs nothing and reads better.
- **Anti-grid and organic shapes** where the subject is human or tactile. On a fintech dashboard it reads as noise; on a bakery it reads as warmth.
- **Grain and texture overlays** as a cheap, effective counter to the flat generated look. One SVG `feTurbulence` at low opacity.

The things that mostly add weight without paying for themselves: WebGL and 3D scenes on a marketing page, full-page scroll-hijacking, autoplaying video heroes, cursor trails, preloader animations, and AI-personalized content on a static site. Skip them unless the subject is literally about that.

## AEO / structured data

Pages now get read by answer engines as often as by people. Cheap wins:

- JSON-LD for the actual entity: `Organization`, `LocalBusiness`, `Person`, `Product`, `Event`, `SoftwareApplication` — whichever fits.
- `FAQPage` schema on the FAQ section, if there is one.
- Headings that read as answers to real questions, not as labels ("多久可以拿到成品" beats "服務流程").
- A real `<title>` and description written for a human, since that's what gets quoted.

## Performance floor

- ≤ 2 font families, ≤ 4 weights, `display=swap`, `preconnect` to both Google Fonts origins.
- No CDN framework tags. Tailwind's CDN build flashes unstyled content and ships a compiler to the browser.
- `loading="lazy"` and explicit `width`/`height` on below-fold images — the dimensions prevent layout shift.
- Inline SVG for icons. No icon-font requests.
- Target under ~60KB of hand-written code for a single page. If it's ballooning, the page has too many sections, not too much CSS.
