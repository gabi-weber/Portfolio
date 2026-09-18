# Gabi Weber — Portfolio · Source of Truth

This is the single reference file for the project. PRODUCT.md and DESIGN.md do not exist — everything lives here.

---

## Project & Brand

**What it is:** Personal design portfolio for Gabi Weber, product designer based in Brazil. Showcases UX/UI case studies and communicates her design philosophy to recruiters, collaborators, and clients.

**Register:** brand — design IS the product.

**Users:**
- Primary: Recruiters scanning fast, deciding within 60 seconds
- Secondary: Product designers, PMs, devs who landed via referral or LinkedIn
- Tertiary: Potential freelance clients or collaborators

**Tone:** Warm, direct, a little playful. First-person, clear sentences. Not corporate, not hustle-culture. Gabi's voice should be present and specific — not generic designer-portfolio prose.

**Anti-references:** Generic SaaS portfolio templates (white bg + electric blue CTA + hero-image-plus-case-grid), overly dark "creative director" aesthetics, Swiss-grid minimalism with no personality, hustle-tone copy, glassmorphism cards, gradient text.

**Strategic principles:**
1. First impression in 5 seconds — hero must land immediately
2. Personality present — this is a brand page, not a product tool
3. One clear job per section — hero: who + why hire. Cases: what she ships. About: who outside work. Footer: one CTA
4. Audience-aware — hero switcher speaks directly to each visitor type
5. The UI is itself a design artifact — sloppy UI signals sloppy design

---

## Tech Stack

- **Plain HTML + CSS + JS only.** No frameworks, no npm, no build tools.
- Each page is a **single self-contained `.html` file**.
- All CSS lives in `<style>` inside the file's `<head>`.
- All JS lives in `<script>` at the bottom of `<body>`.
- Files open directly in a browser — no server required.

---

## File Structure

```
gabi-portfolio/
├── CLAUDE.md              ← this file (single source of truth)
├── Mode 1.tokens.json     ← exported color ramps (gray/brown, with hex)
├── index.html             ← homepage (landing page — in progress)
├── about.html             ← About Me page (done)
├── resume.html            ← résumé page (built)
├── ghost-hunt.html        ← Case 01 (built)
├── reports.html           ← Case 02 (not created yet)
├── tokens.html            ← Case 03 (not created yet)
├── themes.html            ← Case 04 (not created yet)
├── portfolio.html         ← Case 05 (not created yet)
├── CV.pdf
├── assets/
│   └── ghost-hunt/        ← case imagery
│       ├── Animation/     ← modal .mp4 + .svg
│       ├── Ghosts/        ← the five conclusion ghosts (3x exports)
│       └── Screens/       ← the five carousel screens
├── files/
│   └── Halloween Campaign case.pdf
└── fonts/
    ├── Bropella.woff      ← nav logo font
    └── Bropella.woff2
```

**Shared components are duplicated per page, not imported.** The nav, footer, email dropdown and toast exist in full in `index.html`, `about.html`, `resume.html` and every case page. A fix to one does not propagate — change all of them.

---

## Color Tokens

All tokens live in `:root` inside each page's `<style>`. Copy exactly — never hardcode these values outside the token.

```css
--color-bg:      #F7EAE7   /* page background — warm blush-off-white */
--color-primary: #09636C   /* brand teal — CTAs, active states, links */
--color-text:    #1A1B1B   /* near-black — headings, important text */
--color-muted:   #585A5A   /* secondary text, nav links, inactive states */
--color-accent:  #E9BAAE   /* warm blush — placeholders, tag backgrounds */
--color-border:  #C4CBCB   /* dividers, pill borders, subtle separators */
--color-white:   #FEFAF9   /* warm-tinted white — button text, dropdowns, toast */
```

**Color strategy:** Restrained. Warm tinted neutrals dominate; teal accent at ≤10% surface area.

### Case-page additions

Case pages add these to the same `:root`. They are scoped to case pages — do not introduce them on `index.html`, `about.html` or `resume.html`.

```css
--case-dark: #250035   /* case hero banner surface */
--gray-200:  #DFE2E2   /* hero secondary copy on the dark banner */
--gray-500:  #717272   /* meta labels, subsection titles */
--gray-700:  #2D2D2D   /* case body copy and meta values */
```

The gray ramp comes from `Mode 1.tokens.json`, which is the source of truth for any ramp value this file does not list. Grep it before inventing a gray.

---

## Typography

### Nav logo — Bropella only

```css
@font-face {
  font-family: 'Bropella';
  src: url('./fonts/Bropella.woff') format('woff');
  font-weight: 400;
  font-style: normal;
  font-display: swap;
}
/* Applied ONLY to .nav-logo — never anywhere else */
font-family: 'Bropella', cursive;
font-size: 28px; font-weight: 700; color: var(--color-primary);
letter-spacing: -0.2px; line-height: 1;
```

Neulis Cursive was the original intent — replace Bropella when the file is available.

### Case hero title — ABeeZee only

```css
--font-display: 'ABeeZee', sans-serif;   /* Header/1 */
/* Applied ONLY to .cs-title, the <h1> on a case hero. Never elsewhere. */
font-size: 40px; font-weight: 400; color: var(--color-white); line-height: 1.2;
```

This is the one sanctioned exception to Poppins, and it exists only on case pages. Loaded from Google Fonts in the same request as Poppins.

### Body — Poppins everywhere else

Loaded from Google Fonts, weights 300 400 500 600 700. **No exceptions besides the nav logo and the case hero title above.**

| Role | Weight | Size | Color | Notes |
|---|---|---|---|---|
| About page hero title | 300 | `clamp(28px, 3.2vw, 46px)` | `--color-muted` | `letter-spacing: -0.5px`, `line-height: 1.18` |
| Homepage hero headline | 400 | `clamp(28px, 3.2vw, 46px)` | `--color-text` | `letter-spacing` adjusted by JS to equalize line count |
| Section title | 600 | `clamp(32px, 4vw, 52px)` | `--color-text` | `letter-spacing: -0.5px` |
| Section eyebrow | 500 | 11px | `--color-muted` | Uppercase, `letter-spacing: 0.15em` |
| Bio lead paragraph | 400 | 18px | `--color-text` | `line-height: 1.7`, `max-width: 65ch` |
| Bio body paragraphs | 400 | 16px | `--color-muted` | `line-height: 1.8`, `max-width: 65ch` |
| Skill name / list title | 600 | 16px | `--color-text` | — |
| Skill sub / list context | 400 | 12px | `--color-muted` | `line-height: 1.5` |
| Case number | 500 | 12px | `--color-muted` | `letter-spacing: 0.1em` |
| Case title | 600 | 28px | `--color-text` | `letter-spacing: -0.3px`, `line-height: 1.25` |
| Case description | 400 | 14px | `--color-muted` | `line-height: 1.65`, `max-width: 400px` |
| Hero tag / pill | 400 | 14px | `#373939` | — |
| Case tag | 400 | 12px | `--color-muted` | — |
| Nav link | 400 | 14px | `--color-muted` | Active/hover: `--color-primary` |
| Footer greeting | 400 | 20px | `--color-text` | Links: `--color-primary`, weight 500 |
| Footer copy | 400 | 12px | `--color-muted` | — |

### Case page roles

| Role | Class | Weight | Size / line-height | Color |
|---|---|---|---|---|
| Case hero eyebrow | `.cs-eyebrow` | 400 | 16px | `--gray-200` |
| Case hero title | `.cs-title` | 400 | 40px / 1.2 | `--color-white` (ABeeZee) |
| Case hero tags | `.cs-hero-tags` | 400 | 20px / 1.6 | `--gray-200` |
| Metric number | `.cs-metric-number` | 600 | 48px / 1 | `--color-primary`, `letter-spacing: -1px` |
| Metric label | `.cs-metric-label` | 400 | 14px / 1.5 | `--color-muted` |
| Overview lead | `.cs-overview-text` | 400 | 20px / 30px | `--gray-700` |
| Meta label | `.cs-meta-label` | 600 | 14px / 21px | `--gray-500`, uppercase |
| Meta value | `.cs-meta-value` | 400 | 16px / 24px | `--gray-700` |
| Subsection title | `.cs-ps-title` | 600 | 20px / 30px | `--gray-500` |
| Result title | `.cs-kpi-title` | 600 | 20px / 30px | `--gray-700` |
| Case body copy | `.cs-ps-body`, `.cs-kpi-body` | 400 | 16px / 24px | `--gray-700`, `letter-spacing: 0.04em` |
| Figure caption | `.cs-kpi-caption` | 400 | 16px / 24px | `--gray-700`, centered |
| Next-case label | `.cs-next-label` | 400 | 24px / 1.3 | `--color-white` |

---

## Button System

### Base — `.btn`

```css
display: inline-flex; align-items: center; justify-content: center; gap: 8px;
font-family: var(--font); font-weight: 400; text-decoration: none;
cursor: pointer; border: none; white-space: nowrap; user-select: none;
transition: background-color 200ms ease, box-shadow 200ms ease,
            border-color 200ms ease, color 200ms ease;
```

### Sizes

| Class | Font | Line-height | Border-radius | Padding |
|---|---|---|---|---|
| `.btn-huge` | 20px | 30px | 12px | 12px 16px |
| `.btn-large` | 16px | 24px | 8px | 12px 16px |
| `.btn-medium` | 14px | 21px | 8px | 8px 12px |
| `.btn-small` | 12px | 18px | 6px | 4px 8px |

### Types and states

| State | primary | secondary | reverse |
|---|---|---|---|
| default | bg `#09636C`, color `#FEFAF9` | bg `rgba(9,99,108,.10)`, border `2px solid #09636C`, color `#1A1B1B` | bg transparent, color `#373939` |
| hover | bg `#085057` + shadow `2px 2px 10px rgba(26,27,27,.25)` | bg `rgba(9,99,108,.25)` + same shadow | bg `#F7EAE7` + shadow `4px 4px 10px rgba(26,27,27,.05)` |
| active | bg `#085057`, no shadow | bg `rgba(9,99,108,.25)`, no shadow | transparent, no shadow |
| focus-visible | bg `#09636C` + border `2px solid #043F45` | bg `rgba(9,99,108,.20)` + border `rgba(9,99,108,.5)` | border `2px solid rgba(233,186,174,.5)` |
| disabled | bg `#585A5A` | bg `rgba(88,90,90,.25)` + border `#585A5A` | color `#585A5A` |

### btn-overlay (case image hover only)

`border: 2px solid #FFFFFF`, `color: #FFFFFF`, transparent bg, `border-radius: 8px`, `padding: 8px 12px`, 14px. Hover: `background: rgba(255,255,255,.15)`. Never used outside `.case-overlay`.

### Button usage map

| Location | Variant |
|---|---|
| Nav "Contact" | primary · medium |
| Hero "Get in Touch" | primary · large |
| Hero "See My Cases" | secondary · large |
| About section (homepage) "Wanna know more?" | primary · medium |
| About section (homepage) "See my work" | secondary · medium |
| About page "See my work" | primary · medium |
| About page "Get in touch" | secondary · medium |
| Case image overlay | btn-overlay |
| Case page next-case banner | `.btn-banner` |

### btn-banner (next-case banner only)

`background: --color-white`, `color: --color-primary`, `border-radius: 8px`, `padding: 12px 20px`, 16px/24px. Hover: `background: #EDE5E2` + `box-shadow: 2px 2px 12px rgba(0,0,0,.18)`. It sits on the teal strip, where neither primary nor secondary reads. Never used outside `.cs-next-banner`.

---

## Motion System

### Reveal — `.reveal`

```css
opacity: 0; transform: translateY(24px);
transition: opacity 0.6s cubic-bezier(0.22, 1, 0.36, 1),
            transform 0.6s cubic-bezier(0.22, 1, 0.36, 1);
```

Triggered by `IntersectionObserver` (threshold 0.12–0.15), fires once, then unobserved. `.revealed` → `opacity: 1; transform: translateY(0)`.

### Stagger — `.reveal-stagger`

Same curve on children, 80ms delay increments: `nth-child(1)` = 0ms, `(2)` = 80ms, `(3)` = 160ms.

### Nav underline

`width: 0 → 100%`, `transition: width 250ms ease`.

### Hero typewriter

JS-driven, 12ms/character via `setInterval`. Cursor `<span class="hl-cursor">|</span>` blinks via `@keyframes blink` at 530ms step-end infinite. Cursor removes itself when typing completes.

### Case overlay

`opacity: 0 → 1` on `:hover`, `250ms ease`. Hidden on mobile (≤640px) via `display: none`.

### Light/dark crossfade — `.cs-crossfade`

Two stacked stills, no JS. The top one runs `cs-crossfade-loop 8s ease-in-out infinite`, holding each state then dissolving. The two images overlap during the fade, which is the point: it reads as one screen changing theme.

### Sequential ghost dissolve — `.cs-conclusion-ghost`

The opposite rule to the crossfade, and the reason it is its own system: **no two ghosts are ever on screen at once.** Each fully dissolves out before the next starts dissolving in.

Five stacked images on one `cs-ghost-cycle 13.5s ease-in-out infinite` keyframe, offset by `animation-delay` in 2.7s steps. Each 2.7s slot is 0.6s in, 1.5s hold, 0.6s out, and then sits empty until its turn comes round again:

```css
@keyframes cs-ghost-cycle {
  0%       { opacity: 0; }
  4.4444%  { opacity: 1; }   /* 0.6s in   */
  15.5556% { opacity: 1; }   /* 1.5s hold */
  20%      { opacity: 0; }   /* 0.6s out  */
  100%     { opacity: 0; }
}
```

To retime it, pick the slot length, multiply by the number of images for the duration, and re-derive the four percentages. `prefers-reduced-motion: reduce` kills the animation and holds the first image.

### Screens carousel

Slides are positioned by `data-offset` from the active one (`0`, `±1`, `±2`), so every transition falls out of the same rules: `transform` and `opacity` over `520ms cubic-bezier(0.22, 1, 0.36, 1)`. Autoplay advances every **4000ms** and steps back after **9000ms** of user quiet. The whole carousel is one tab stop driven by arrow keys; the dots stay individually reachable. `prefers-reduced-motion: reduce` drops the slide transition.

### Fixed-stage rule

Any element that swaps images in place gets a **fixed box** the art is fitted into, never a box the art sizes. The Conclusion uses a 200×200 stage with the art inset to 186×186 and `object-fit: contain`, so the five ghosts (which range from 341×564 to 567×364) all land at exactly 186px on their long edge and nothing below them shifts as they cycle.

---

## Layout System

### Nav

Fixed, `height: 64px` (`--nav-h`), `padding: 0 48px`, `background: rgba(247,234,231,0.62)`, `backdrop-filter: blur(14px)`, `z-index: 200`.

### Max-widths

| Context | Max-width |
|---|---|
| index.html hero inner, case rows | 1400px |
| about.html all sections | 1100px |
| case pages | per frame — see the table under Section rhythm |

### Horizontal padding

`index.html` / `about.html`: 48px desktop → 24px at ≤600px.
Case pages: 60px desktop → 24px at ≤768px (metric cards are 48px).

### Section rhythm — index.html

| Section | Padding |
|---|---|
| Hero | 100vh min-height, `padding-top: 64px` |
| Case rows | `64px 48px` each |
| About section | `64px 48px 120px` |
| Footer | `56px 48px` |

### Section rhythm — about.html

| Section | Padding |
|---|---|
| Page hero | top `nav-h + 80px`, bottom `64px` |
| Bio section | `0 48px 96px` |
| Skills section | `0 48px 120px` |
| Footer | `56px 48px` |

### Section rhythm — case pages

**140px between every section**, as the bottom padding of each one. Horizontal page margin is **60px** (the metric-cards section is the lone exception at 48px). Both collapse to `0 24px 80px` at ≤768px.

| Section | Padding |
|---|---|
| Case hero | `nav-h + 600px` tall, no padding (absolute composition) |
| Metric cards | `0 48px 140px`, inner pulled up `margin-top: -64px` |
| Overview | `0 60px 140px` |
| Problem & Solution / Process | `0 60px 140px` |
| Screens carousel | `0 60px 140px` |
| KPI trio | `0 60px 140px` |
| Conclusion | `0 60px 140px` |
| Next-case banner | `56px 48px` |
| Footer | `56px 48px` |

### Body measure — `--copy-w: 432px`

One token in `:root` governs the line length of every body column on a case page: Problem, Solution, Process, the KPI results and the Conclusion. Change it there, never per section. Each frame is then built around it:

| Frame | Width | Composition |
|---|---|---|
| Overview row | 1320px | 668px lead + 71px gap + 544px meta stack |
| Metric cards | 1200px | 3 equal cards, 24px gap |
| Screens carousel | 1200px | — |
| KPI trio | 1098px | email figure (shrinks to 634px) + 32px gap + 432px copy |
| Problem & Solution / Process | 846px | 287px phone mock + 127px gap + 432px copy |
| Conclusion | 692px | 200px ghost stage + 60px gap + 432px copy |

**127px is the standard asset-to-copy gap.** The Conclusion deliberately breaks it at 60px: its ghost stage is a fixed 200px box whose art is narrower still, so the standard gap read as a hole. Any section whose asset does not fill its own box should expect the same correction.

### Responsive breakpoints

| Breakpoint | Changes |
|---|---|
| ≤1100px | Case: KPI trio stacks, copy column capped at `--copy-w` |
| ≤1024px | `.btn-overlay` shrinks to 13px, padding 6px 10px |
| ≤966px | Case: Problem & Solution, Process and Conclusion stack, 52px gap, copy capped at `--copy-w` |
| ≤900px | Bio grid → 1-column; photo → 4:3 max 420px; skills → 2-column |
| ≤768px | Case: all section padding → `0 24px 80px`; nav padding 24px; hero de-absolutes and stacks; decorative hero ghosts hidden |
| ≤640px | Case overlay hidden (touch devices tap the image directly) |
| ≤600px | Nav padding 24px; index/about section horizontal padding 24px; skills → 1-column |

Case pages run their own breakpoint ladder (1100 / 966 / 768). `index.html` and `about.html` run the 1024 / 900 / 640 / 600 ladder. Do not mix them.

---

## Surface Treatments

### Grain texture (every page)

```html
<svg class="grain" aria-hidden="true">
  <filter id="grain-filter">
    <feTurbulence type="fractalNoise" baseFrequency="0.65" numOctaves="3" stitchTiles="stitch" />
    <feColorMatrix type="saturate" values="0" />
  </filter>
  <rect width="100%" height="100%" filter="url(#grain-filter)" />
</svg>
```

```css
.grain { position: fixed; inset: -50%; width: 200%; height: 200%;
         pointer-events: none; z-index: 9999; opacity: 0.04; }
```

### Image / photo placeholders

`background: var(--color-accent)`. Case images: `border-radius: 12px`. Bio photo: `border-radius: 16px` + diagonal stripe:

```css
background: repeating-linear-gradient(45deg,
  transparent, transparent 12px,
  rgba(255,255,255,0.15) 12px, rgba(255,255,255,0.15) 13px);
```

---

## Design Absolute Bans

Never write these — rewrite the element if you're tempted:

- `border-left` or `border-right` > 1px as a colored accent on list items or cards
- `background-clip: text` with a gradient (gradient text)
- `transition: all` — always list explicit properties
- `#000` or `#fff` — use `--color-text` and `--color-white`
- Glassmorphism decoratively (nav blur is functional — it sits over scrolling content)
- Gradient text, hero-metric templates (big number + stat grid), identical card grids
- Em dashes in copy — use commas, colons, semicolons, or parentheses instead
- `justify-content: space-between` to spread a fixed set of blocks down a column. It turns whatever slack the neighbouring asset happens to leave into the gap, so the spacing is an accident of image height and the group stops reading as a group. Set the gap you want and center it.
- A swapping image sized by its own art. The box is fixed, the art is fitted into it — otherwise the page reflows every few seconds.
- A second body measure. Case page body copy is `--copy-w`, full stop.

---

## index.html — Component Map

### Nav

Glass blur, Bropella logo left, links + Contact button right. Active state on current page nav link: `color: --color-primary` + underline always on.

### Hero (100vh)

Two-column grid: `26fr 74fr`. Left: audience switcher (dot indicator, 5 options, 15px Poppins 400). Right: tags → headline → CTA buttons.

- Switcher inactive: `--color-muted` | Active: `--color-text` | Hover: `--color-primary`
- Headline heights locked by JS on load + resize (binary-search letter-spacing to equalize line count)
- All headlines `position: absolute`; only `.active` has `opacity: 1`
- Typewriter fires on each switch

### Audience options

| # | Label | Headline | Tags |
|---|---|---|---|
| 0 | For everyone | "I design with intention — so that real people's lives are a little better. That's the whole point." | 👩‍💻 Product designer · ✨ AI-Augmented Workflow · 🖼️ Illustrator · 🇧🇷 Brazil |
| 1 | Recruiters | "3+ years in B2B. I bridge design and dev, communicate clearly, and make collaboration feel easy." | 💼 Open to work · 🖥️ Remote-first · 🏢 Big company experience · 🏆 Team player |
| 2 | Product designers | "Every designer has a love-hate relationship with Figma. I just made sure the love always wins." | 🧮 Design systems · 📄 UX driven · 🎀 Detailed UI · 😎 Vibe coding |
| 3 | Product managers | "I design to get it right the first time — clean handoff, clear rationale, no surprises in QA." | 📊 Metrics-driven · 🚢 Shipped products · 🕵️ Edge-case hunter · 💬 Multitrack teams |
| 4 | Developers | "I give you tokens, documentation, and a handoff that makes your life easier — not harder." | 🧬 Token architecture · 🫴 Clean handoff · 📣 Open communication · 🛠️ AI tooling |

### Cases section (zigzag, no header)

- Odd rows: image left 55% / text right 45%
- Even rows: text left 45% / image right 55%
- Gap: 56px. Image = `<a href="case.html" class="case-image">` — entire image is the link
- Hover overlay: `rgba(9,99,108,0.80)` + description + `btn-overlay`
- Scroll reveal: `IntersectionObserver`, threshold 0.15, fires once

| # | Title | Tags | Link |
|---|---|---|---|
| 01 | Boosting feature engagement through whimsical interventions | 💡 Engagement · 📣 Campaign · ✏️ Illustration · 🎨 Creative | ghost-hunt.html |
| 02 | Redesigning the Reports Engine | 🔍 Discovery · 📊 Dashboard · 🤝 B2B · 📈 Scalability | reports.html |
| 03 | Scaling Design Infrastructure | 🧩 Design System · 🌙 Dark Mode · 🏷️ Tokens · 📄 Documentation | tokens.html |
| 04 | Thematic Expression at Scale | 🌿 Seasonal · ✏️ Illustration · 🎭 Identity · ✨ Delight | themes.html |
| 05 | This Portfolio | 🎨 Branding · 💻 Coding · 📱 Responsive · ✍️ Copywriter | portfolio.html |

### About Me section (homepage)

- Centered, `max-width: 700px`
- Two-column: photo left (200px) / bio right
- Bio text (short version): "Hi, I'm Gabi! I'm a product designer based in Brazil who makes things — digital and otherwise."
- Buttons: primary · medium "Wanna know more?" → `about.html` + secondary · medium "See my work" → `#works`

### Footer (shared across pages)

- "Say hi 👋" → `https://www.linkedin.com/in/gabriela-lissarassa-weber/` (new tab)
- "Get in touch ✉️" → toggles email dropdown (above trigger, right-aligned to trigger)
  - "Copy email" → copies `gabrielaweber008@gmail.com`, toast "Email copied ✓"
  - "Send email" → `mailto:gabrielaweber008@gmail.com`
  - Closes on outside click or Escape
  - Toast: fixed bottom-center, `opacity: 0 → 1` 200ms, hold 1800ms, fade out
- Copyright: "Created by Gabi and powered by iced coffee ☕"

---

## about.html — Component Map

### Nav

Same as index.html. "About me" link gets `.nav-active` class (teal + underline always on, no hover needed).

### Page Hero

- `padding-top: calc(var(--nav-h) + 80px)`, `padding-bottom: 64px`
- Eyebrow: "Get to know me"
- `<h1>`: "I fell in love with design when I realized it could actually help people."
  - Poppins 300, `clamp(28px, 3.2vw, 46px)`, `--color-muted`, `letter-spacing: -0.5px`

### Bio Section

- Grid: `320px | 1fr`, `gap: 72px`, `align-items: start`
- Photo: `aspect-ratio: 3/4`, `--color-accent` bg, `border-radius: 16px`, diagonal stripe overlay, no label text
- Bio text: 3 paragraphs (lead 18px `--color-text`, body 16px `--color-muted`, both `max-width: 65ch`)
- CTA row after third paragraph: primary · medium "See my work" → `index.html#works` + secondary · medium "Get in touch" → `index.html#contact`

### Skills & Interests section

Eyebrow "Skills & interests" above the grid (`.skills-header`, `padding-bottom: 40px`).

Three-column grid `1fr 1fr 1fr`, `gap: 56px`. All columns use the same `.skill-list / .skill-item / .skill-name / .skill-sub` pattern.

Column label style: 11px Poppins 500 uppercase `--color-muted`, `border-bottom: 1px solid --color-border`, `padding-bottom: 16px`.

| Column | Items |
|---|---|
| Competencies | UX Design / Communication / UI Design / Illustration / AI-Augmented Workflow |
| Tools | Figma / Adobe Creative Cloud / Claude |
| Interests | Gaming / Reading / Ceramics / Hiking / Pets / Series |

Each item: `.skill-name` (600, 16px, `--color-text`) + `.skill-sub` (400, 12px, `--color-muted`). Interests have emoji at start of `.skill-sub`, not in the name.

### Reveal animations

- `.reveal` on page hero div, photo wrapper, bio text div, `.skills-header`
- `.reveal-stagger` on `.skills-inner` (3 children stagger at 80ms each)

---

## ghost-hunt.html — Component Map

Case 01, and the reference implementation for every case page that follows. Section order top to bottom:

### Nav

Same as index.html, over the dark hero. The hero paints a `--color-bg` band exactly `--nav-h` tall behind the translucent nav, so at scroll-top the blush strip shows through and the dark banner starts right below it.

### Case hero

Dark `--case-dark` banner, `nav-h + 600px` tall, `overflow: hidden`. The content is one absolutely positioned `.cs-hero-group` (`left: 60px`, `top: nav-h + 52px`, 1405×419px) so the whole composition rescales from one place.

- Copy block 662px wide, vertically centred: eyebrow "Case study · 01" → `<h1>` → tags
- Laptop still starts at x=762 and runs 703px wide, bleeding past the 1440 frame on purpose
- Two decorative ghosts rotated per the Figma frame, hidden at ≤768px

### Metric cards

Three cards in a 1200px grid, 24px gap, pulled up over the hero with `margin-top: -64px` and `z-index: 2`. Each is `--color-white`, 1px border, 12px radius, 32px padding, `box-shadow: 0 12px 32px rgba(37,0,53,.18)`.

| Number | Label |
|---|---|
| 164% | average increase in feature adoption |
| 550% | peak boost in specific profile interactions |
| 64% | average email interaction rate |

### Overview

1320px row: 668px lead paragraph + 71px gap + 544px meta stack (Role and Timeline side by side, then Deliverables full width).

### Problem & Solution / Process

Both use the 846px `.cs-ps` frame, alternating sides: Problem & Solution puts the phone mock left (a looping muted `.mp4`), Process puts it right (a `.cs-crossfade` pair, light over dark). Copy column is `--copy-w`, 52px between title/body blocks, 4px between a title and its body.

### Screens carousel

1200px frame, no heading. Five screens from `assets/ghost-hunt/Screens/`, the active one at full scale and the flankers dimmed to 0.42 and scaled 0.82. Dots below, live-region status for screen readers. Autoplay 4s, resumes 9s after the last interaction.

### KPI trio

1098px row: the campaign email figure + caption on the left, three results on the right in a `--copy-w` column. The email figure shrinks to take up whatever the copy column does not need (634px at full width). Results are `justify-content: center` with a hard **48px** gap — not `space-between`, which stretched it to 74px and broke the three into unrelated items. The list's 36px bottom padding is the figure's 12px gap + 24px caption, so the copy box lines up with the image box rather than the caption.

| Result | |
|---|---|
| Adoption Spike | all five features up, "Edit Profile" +550% |
| Behavioral Attribution | 66% of early Dark Mode adoption traced to the hunt |
| Email-to-App Conversion | higher open rates → stronger component performance |

### Conclusion

692px row, ghosts left and copy right. Title/body reuse `.cs-ps-block` so the 4px step is the section standard. The ghost stage is a fixed 200×200 with a 186×186 art box inside it; the five ghosts cycle on the sequential dissolve described in the Motion System. Copy is one paragraph at `--copy-w`.

### Next-case banner

Full-bleed `--color-primary` strip, `56px 48px`, "Wanna see more of my work?" left and a `.btn-banner` ("See all cases" → `index.html#works`) right. `.btn-banner` is a case-page-only variant: `--color-white` background, `--color-primary` text, 8px radius, `12px 20px`.

### Footer

Identical to index.html, duplicated in full.

---

## Build Order for Case Pages

Each case page is a self-contained `.html` file using the same tokens, fonts, nav, and footer as `index.html`. **`ghost-hunt.html` is the built reference — copy its structure rather than working from the sketch below.**

Suggested structure:
1. **Nav** — copy exactly from index.html, plus the hero's `--nav-h` blush band
2. **Case hero** — eyebrow, title, tags, hero asset
3. **Metric cards** — the outcome numbers, pulled up over the hero
4. **Overview** — lead paragraph + role / timeline / deliverables
5. **Process sections** — alternating copy and asset on the 846px frame
6. **Results** — the numbers in context
7. **Conclusion** — closing copy plus a signature asset
8. **Next case** — link to next page + back to Works
9. **Footer** — copy exactly from index.html

Priority: ~~`ghost-hunt.html`~~ (built) → `reports.html` → `tokens.html` → `themes.html` → `portfolio.html`
