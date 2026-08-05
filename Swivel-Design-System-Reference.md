# Swivel Design System Reference

**Ground-truth extraction of swivelteam.com** — how the site is actually built today, as a baseline to extend.

| | |
|---|---|
| **Method** | Computed styles (`getComputedStyle`) read from the live published site in a real browser, at three real viewport widths, plus real mouse-driven hover/click state capture. Cross-referenced read-only against the Framer project "Swivel". |
| **Coverage** | **75 pages × 3 breakpoints = 225 extractions, 0 errors.** 62 URLs from `sitemap.xml` + 13 live pages found only in Framer's Pages panel. |
| **Excluded** | `/dashboard`, `/old-dashboard` (per brief). `/case-studies` and `/for` are folder roots only (404, no live page). |
| **Measured at** | Desktop 1440px · Tablet 1024px · Mobile 390px |
| **Date** | 3 August 2026 |

> **How to read this.** Everything in fixed-width type is a measured value, not a recommendation. Section 13 (Compositional Grammar) is the part to use when designing something that doesn't exist yet. Section 16 lists everything that is inconsistent or unresolved.

---

## 0. Breakpoints

Confirmed from the live stylesheet **and** the Framer canvas (labelled "Desktop 1200", "Tablet 1199−").

| Name | Range | Media query |
|---|---|---|
| Desktop | ≥ 1200px | `@media (min-width: 1200px)` |
| Tablet | 810 – 1199.98px | `@media (min-width: 810px) and (max-width: 1199.98px)` |
| Mobile | ≤ 809.98px | `@media (max-width: 809.98px)` |

Framer emits one variant per range, so any width inside a range renders the same variant with fluid widths.

---

## 1. Typography Scale

### Typefaces

**Museo Sans** is the entire brand voice. It is loaded as **four separate font families**, not four weights of one family — `Museo Sans 300`, `Museo Sans 500`, `Museo Sans 700`, `Museo Sans 900`, plus `Museo Sans 300 Italic`. The CSS `font-weight` value is therefore near-meaningless on its own: a `font-weight: 600` on `Museo Sans 700` is the 700 face. **Always specify the family name, not the weight.**

Non-brand faces present (all unintentional or system-scoped):

| Face | Where | Verdict |
|---|---|---|
| `Inter` 16px/28.8 bold | `/blog/calculate-cpql-google-meta` only | Stray — should be Museo Sans 500 |
| `Fragment Mono` | `<code>` in one blog post | Stray |
| `Montserrat` 11px | Footer legal links (desktop/tablet only) | Stray |
| `ui-sans-serif`, `ui-monospace`, `sans-serif` | `/login`, `/pathforward-dashboard` | Expected — React code components, outside the Framer system |

### The named scale (Framer Text Styles → measured values)

These are the styles that **exist by name** in the Framer project. Reference them by name in future briefs.

| Framer style | Tag | Desktop | Tablet | Mobile | Measured tracking | Typical use |
|---|---|---|---|---|---|---|
| **Heading 1** | h1 | `90px / 90px` | `72px / 72px` | `40px / 40px` | `-3.5px` → `-2px` → `-1px` | Homepage hero only |
| **Heading 1b** | h1 | `72px / 72px` | `46px / 46px` | `28px / 28px` | `-2.5px` | Page heroes |
| **Heading 2** | h2 | `54px / 59.4px` | `46px / 50.6px` | `36px / 39.6px` | `-2.5px` | **Standard section heading** |
| **Heading 2b** | h2 | `54px / 48.6px` | `54px / 48.6px` | `54px / 48.6px` | `-2.5px` | Big stat numerals ("11.7x") — *does not scale down* |
| **Heading 3** | h3 | `36px / 39.6px` | `28px / 30.8px` | `28px / 30.8px` | `-1.5px` | Sub-section / card heading |
| **Heading 6** | h6 | `32px / 35.2px` | `24px / 26.4px` | `21px / 23.1px` | `-1.5px` | Comparison "faded" headings |
| **Heading Long** | h4 | `28px / 33.6px` | `21px / 25.2px` | `21px / 25.2px` | `normal` | Pull-quotes, long headings |
| **Heading 4** | h4 | `26px / 31.2px` | `20px / 24px` | `20px / 24px` | `-0.6px` | Card titles, feature titles |
| **Heading 6b** | h6 | `22px / 26.4px` | `22px / 26.4px` | `22px / 26.4px` | `-0.6px` | FAQ questions — *does not scale* |
| **Body Large** | p | `20px / 26px` | `18px / 23.4px` | `16px / 20.8px` | `normal` | Hero subhead, lead paragraphs |
| **Body Medium** | p | `16px / 24px` | `14px / 21px` | `14px / 18.2px` | `normal` | Standard body |
| **Strong Medium** | p | `16px / 19.2px` | `16px / 19.2px` | `16px / 19.2px` | `normal` | **Most-used style on the site** (n≈2,091) — UI labels, nav |
| **Body** | p | `16px / 16px` | `16px / 16px` | `16px / 16px` | `normal` | Attribution, tight meta (n≈2,334) |
| **Body Small** | p | `14px / 18.2px` | `14px / 18.2px` | `14px / 18.2px` | `-0.2px` | Footer, timestamps, meta |
| **Heading 5** | h5 | `16px / 24px` | `16px / 24px` | `16px / 24px` | **`+8px`, `UPPERCASE`** | **The eyebrow.** Never scales. |
| **Navigation** | p | `18px / 18px` | — | — | `normal` | Declared; rarely matched in the wild |
| **Nav Small** | p | `13px / 14.3px` declared | — | — | `-0.2px` | Declared 13/1.1 but rendered 13/16.9 — overridden in practice |

### Measured styles with **no** named Framer style

These are consistent, repeated patterns that are **not** bound to a Text Style — prime candidates to formalise.

| Measured | Desktop → Tablet → Mobile | Use | Frequency |
|---|---|---|---|
| `46px / 50.6px` `-1.5px` MS700 | `46 → 38 → 30` | **Blog post H1** | n≈40 |
| `30px / 37.5px` `-0.5px` MS700 | `30 → 26 → 22` | **Blog body H2** | n≈307 |
| `22px / 28.6px` `-0.3px` MS700 | `22 → 20 → 18` | **Blog body H3** | n≈272 |
| `18px / 28.8px` MS300 | `18 → 17 → 16` | **Blog body copy** (1.6 line-height) | n≈1,126 |
| `18px / 28.8px` MS500 | as above | Bold run inside blog body | n≈393 |
| `20px / 24px` `-0.6px` MS500 | constant | **Large button label** | n≈603 |
| `14px / 16.8px` `-0.3px` MS500 | constant | **Small button label** | n≈292 |
| `15px / 30px` `-0.15px` MS300 | constant | Nav dropdown description (2.0 line-height) | n≈756 |
| `27px / 27px` MS700 | constant | The literal "vs" divider on compare pages | n≈60 |
| `13px / 16.9px` `-0.2px` UPPERCASE | desktop/tablet only | Breadcrumb | n≈291 |
| `14px / 18.2px` `+3px` UPPERCASE MS700 | constant | "DOWNSIDES" label, `#f53434` | n≈6 |

### Line-height convention

Line-height is a **ratio applied per style**, and it is remarkably regular:

- Display (54px+): **0.9 – 1.1** — tight, deliberately cramped
- Headings (22 – 46px): **1.1 – 1.3**
- UI / labels: **1.0 – 1.2**
- Body: **1.5**
- **Long-form blog body: 1.6** — the only place the site breathes this much
- Nav dropdown descriptions: **2.0** — an outlier

### Gradient text

Headings frequently use `background-clip: text` with the brand gradient. **Always** on a `<span>` inside the heading, never the whole heading — so a headline reads "plain words + *gradient words*". Full stop lists in §2.

---

## 2. Colour & Gradient Tokens

### Named Framer Colour Styles (24 styles → 26 published `--token-*` variables)

`Border Day` · `Border Night` · `Surface Night` · `Surface Day` · `Neutral 800` · `Neutral 500` · `Blue Light` · `White` · `GrayDark2` · `Green` · `4-Colors Green` · `4 Colors - Blue` · `3-Colors Green` · `Blue` · `Gray` · `Neutral 04` · `Neutral 01` · `Neutral 03` · `White` · `Green` · `Dark Blue` · `White` · `Medium Grey` · `White`

> **`White` appears four times and `Green` twice.** There are also three parallel neutral namings (`Neutral 800/500` vs `Neutral 01/03/04` vs `Gray` / `GrayDark2` / `Medium Grey`). Naming is the weakest part of the system.

### The palette that is actually rendered

| Hex | Role | Token? |
|---|---|---|
| `#82c88a` | **Brand green** | ✅ |
| `#0196cd` | **Brand blue** | ✅ |
| `#eba343` | **Primary CTA orange** | ❌ **no token — raw hex, n≈195** |
| `#38aeb2` | Teal (secondary CTA) | ✅ |
| `#2ca7b7` | Teal-blue | ✅ |
| `#57b7a0` | Green-teal | ✅ |
| `#3d4443` | **Primary text** | ✅ |
| `#23252c` | Blog body text | ✅ |
| `#2e3238` | Dark text / dark surface | ✅ |
| `#666873` | Muted / eyebrow text | ✅ |
| `#fefffe` | Off-white on dark | ✅ |
| `#0a0a0a` | Near-black section | ✅ |
| `#5b5b5b`, `#646464`, `#0d0d0d` | Greys | ✅ |
| `#f53434` | **Error / negative red** | ❌ **no token** |
| `#373b40` | Split-background charcoal | ❌ no token |
| `#071330`, `#122e76`, `#b3bcff`, `#f7cb2d`, `#1f514c` | Declared but barely/never used on the public site | ✅ (orphan tokens) |
| `#f3f5f8`, `#0d9488`, `#e4e8ec`, `#0a0f1e` | `/login` + `/pathforward-dashboard` only | ❌ outside the system |

### Full-span vs contained

Recorded per instance. Rule that holds site-wide:

- **Solid colours** are almost always *contained* (inside a card/pill). The exceptions are `#0a0a0a` (n=201) and `#2e3238` — used as **full-bleed dark section beds**.
- **Soft tint washes** are almost always *full-span* — they are the section-rhythm device (below).
- `#ffffff` runs both ways: n≈1,228 contained (cards), n≈400 full-span (default page bed).

### The brand gradient

One gradient — `#82c88a → #0196cd` — rendered at **~15 different angles**:

```
0deg   82deg  111deg 135deg 270deg 275deg 277deg 283deg
284deg 288deg(reversed) 289deg 291deg 294deg(3-stop) 315deg  vertical(no angle)
```

Two stop patterns are also in play: plain `0% → 100%`, and `16% → 88%`. One 3-stop variant adds `#45a6bd` at `71.9888%`.

> This is the single biggest inconsistency in the system. See §16.

**Most-used instances**

| Gradient | Count | Span |
|---|---|---|
| `linear-gradient(#82c88a 0%, #0196cd 100%)` | 246 | full |
| `linear-gradient(315deg, #82c88a 0%, #0196cd 100%)` | 220 | contained |
| `linear-gradient(82deg, #0196cd 0%, #82c88a 100%)` | 216 | contained |
| `linear-gradient(275deg, #82c88a 0%, #0196cd 100%)` | 192 | contained |
| `linear-gradient(270deg, #82c88a 0%, #0196cd 100%)` | 186 | contained |

Text gradients cluster at **270 – 294deg** (right-to-left, green → blue).

### Soft tint section washes — *the rhythm device*

Full-span, and this is how the site separates sections without hard rules or solid blocks. Brand colours at **15–20% alpha** bleed in at the top and/or bottom edge; the middle stays pure white.

```css
linear-gradient(rgba(0,152,205,.15) -5%, #fff 10%, #fff 90%, rgba(112,196,151,.15) 100%)  /* n=30 */
linear-gradient(rgba(0,152,205,.15) -5%, #fff 10%, #fff 90%, rgba(112,196,151,0)   100%)  /* n=27 */
linear-gradient(#fff 43.2133%, rgba(112,196,151,.15) 100%)                                /* n=27 */
linear-gradient(rgba(0,152,205,.15) 0%, #fff 10%, #fff 90%)                               /* n=18 */
linear-gradient(rgba(0,152,205,.16) 0%, rgba(112,196,151,0) 100%)                          /* n=19 */
linear-gradient(rgba(112,196,151,.2) 0%, #fff 50%, rgba(1,150,205,.2) 101.629%)            /* n=9  */
linear-gradient(#e6f6fc -5%, #fff 10%, #fff 90%, #fff 100%)                                /* n=3  */
```

### Radial accent glows (contained, decorative)

```css
radial-gradient(50% 50%, #fff 0%, rgba(130,200,138,.16) 100%)                 /* n=21, all bp */
radial-gradient(50% 50%, rgba(255,255,255,.16) 0%, rgba(56,174,178,.16) 100%) /* n=21 */
radial-gradient(50% 50%, #fff 0%, rgba(1,150,205,.16) 100%)                   /* n=21 */
radial-gradient(86% 124% at 19% 57.1%, #4e4e4e 0%, #000 57.5838%)             /* dark section, desktop */
radial-gradient(86% 67%  at 50% 43.9%, #4e4e4e 0%, #000 57.5838%)             /* same, mobile re-aimed */
```

### Conic gradients (3D orb / icon fills, identical at all breakpoints)

```css
conic-gradient(from 66deg  at 38.5% 37.4%, #82c88a 93.6deg, #209e5b 219.6deg)
conic-gradient(from 66deg  at 38.5% 37.4%, #0196cd 93.6deg, #00678c 219.6deg)
conic-gradient(from 225deg at 83%   63.6%, #1a777a  3.6deg, #38aeb2 151.2deg)
```

### Hard-stop / split backgrounds

Used to put a card half on a dark bed and half on a light one.

```css
linear-gradient(#373b40 50%, #82c88a 50%)                          /* n=60, desktop+tablet */
linear-gradient(#2e3238 49.9701%, #82c88a 50%, #0196cd 100%)       /* desktop only  */
linear-gradient(#2e3238 49.9701%, #2e3238 50%, #2e3238 100%)       /* mobile flattens to flat charcoal */
linear-gradient(#000 0%, #545454 100%)                              /* n=21 */
```

---

## 3. Spacing Scale

### Section padding — the actual rules

| Context | Desktop | Tablet | Mobile |
|---|---|---|---|
| **Horizontal gutter** | `40px` (on the 1360 rail) or `64px` (on the 1200 rail) | **`64px` uniformly** | **`30px` uniformly** |
| **Hero top** | `160px` | `120px` | `120px` |
| **Standard section** | `120px` top / `120px` bottom | `120 / 80` or `80 / 80` | `120 / 40` |
| **Compact section** | `80 / 80`, `64 / 64` | `64 / 64`, `90 / 90` | `64 / 64`, `64 / 40` |

Most frequent full padding shorthands measured (`top,right,bottom,left`):

```
Desktop  180,64,0,64 (n=33) · 120,40,120,40 (n=14) · 160,40,120,40 (n=12)
         160,40,80,40 (n=10) · 120,40,80,40 (n=9) · 160,64,120,64 (n=7) · 80,40,80,40 (n=6)
Tablet   120,64,0,64 (n=36) · 120,64,80,64 (n=23) · 80,64,80,64 (n=13)
         64,64,64,64 (n=10) · 80,64,64,64 (n=9) · 90,64,90,64 (n=8) · 120,64,120,64 (n=7)
Mobile   120,30,40,30 (n=45) · 64,30,64,30 (n=27) · 120,0,40,0 (n=15) · 64,30,40,30 (n=13)
```

### Vertical spacing between typographic elements

Derived from repeated card/section instances rather than one-offs:

- **Eyebrow → H2:** ~16–24px
- **H1/H2 → subhead:** ~24px consistently
- **Subhead → CTA:** ~40px in heroes, ~32px in sections
- **Card padding:** `40px` all round is the default; `32px` on smaller cards; `64,30,40,30` on the tall testimonial card
- **Section → section:** always via the two paddings above; there are **no** margins between sections and **no** horizontal rules

### The spacing vocabulary

Values actually in use: `8 · 12 · 16 · 18 · 24 · 26 · 30 · 32 · 40 · 48 · 64 · 80 · 90 · 120 · 128 · 160 · 164 · 180`.
This is close to an 8px grid, with `18`, `26`, `30`, `90` and `164` as the deviations.

---

## 4. Shadows & Effects

Only **five** distinct shadows exist site-wide. This part of the system is tight.

| # | Value | Use |
|---|---|---|
| **1. Button / ambient** | `rgba(0,0,0,.07) 0 0.602187px 1.80656px -1.25px,`<br>`rgba(0,0,0,.06) 0 2.28853px 6.8656px -2.5px,`<br>`rgba(0,0,0,.03) 0 10px 30px -3.75px` | **Every pill button.** Framer's 3-layer preset. Unchanged on hover. |
| **2. Card lift** | `rgba(0,0,0,.08) 0 10px 15px 0` | Standard raised card |
| **3. Deep soft** | 5 layers, `rgba(20,15,15,.06)` at `0.59 / 1.61 / 3.54 / 7.87 / 20px` offsets (diagonal, x = y) | Feature cards — a diagonal shadow, unusual for this system |
| **4. Hard drop** | `rgba(0,0,0,.25) 10px 10px 2px 0` | One card only. Off-system. |
| **5. Brand glow** | `rgb(1,150,205) 0 0 60px 0` | The dark `#0a0a0a` chart panel — a blue bloom |
| *(login only)* | `rgba(13,27,42,.08) 0 4px 24px 0` | `/login` card, outside the system |

### Borders — only three exist

| Value | Count | Use |
|---|---|---|
| `1px solid rgba(34,34,34,0.1)` | 138 | **The hairline.** Dividers, card outlines, FAQ separators. Token `#2222221a` exists. |
| `1px solid rgba(255,255,255,0.16)` | 9 | Hairline on dark beds |
| `1px solid #e4e8ec` | 6 | `/login` only — off-system |

### Radii

| Value | Use |
|---|---|
| `999px` | **All buttons/pills, avatars.** Universal. |
| `40px` | Large feature cards; `40px 40px 0 0` for top-rounded panels |
| `24px` | **Default card radius** (most common) |
| `20px` | Secondary card, dropdown panel |
| `12px` | `/login` inputs & card |
| `8px` | `/login` submit button |
| `50%` | Carousel control dots |

`24px 24px 0 0` and `40px 40px 0 0` (top-only) are a recurring device for panels that sit flush on a coloured bed.

**Backdrop-filter is not used anywhere.** Glass effects are achieved with `rgba(255,255,255,0.12)` / `0.3` fills over dark beds.

---

## 5. Buttons & Components

### The button system (Framer components: `⬛️ L Button Fill`, `⬛️ M Button Fill`, `⬛️ S Button Fill`)

| Size | Component | Padding | Height | Label style | Radius | Where |
|---|---|---|---|---|---|---|
| **L** | `⬛️ L Button Fill` | `18 / 40` | `60px` | MS500 `20px/24` `-0.6px` | `999px` | Hero + section CTAs (n=218 across 10 pages) |
| **M** | `⬛️ M Button Fill` | `12 / 24` | `43px` | MS500 `16px` | `999px` | Card CTAs (n=16, 7 pages) |
| **S** | `⬛️ S Button Fill` | `8 / 24` | `40px` | MS500 `14px/16.8` `-0.3px` | `999px` | Nav "Book Call" / "Login" (n=128) |
| **XS** | *(unnamed)* | `8 / 24` | `33px` | MS500 `14px` | `999px` | "Read Now" on blog cards |

**Fill colours in use, all on the same geometry:**
`#eba343` (orange, primary) · `#82c88a` (green) · `#38aeb2` (teal) · `#0196cd` (blue) · `#57b7a0` · `#2ca7b7` · `#ffffff` (outline/inverse) · transparent (ghost, e.g. persona tabs).

> There is **no** single "primary button colour". The same L component appears in orange, green, teal and blue on different pages with no evident rule. See §16.

**Every button carries shadow #1 and every button has `border: 0`.** The white "Login" button's visible outline is a `1px rgba(34,34,34,0.1)` border on a child, not a button border.

### Other named components

- `Easy Button` — the recurring closing CTA block on all five compare pages (n=6, 6 pages)
- `DSecondary` — secondary link treatment (n=3)
- Carousel: `Carousel Controls` → `Slide Dots` (`Dot 1`, `Dot 2`), `Arrow Controls` (`Previous Slide`, `Next Slide`). Dots are `rgba(0,0,0,0.3)`, `border-radius: 50%`, `40px`, `transition: opacity 0.2s`.
- Theme variants exist as `⚪️ Day` / night pairs, and `Variant 1`–`Variant 5`, `Default`, `Selected` / `Unselected`.

### Cards

| Pattern | Radius | Background | Shadow | Padding | Width |
|---|---|---|---|---|---|
| Top-rounded stat panel | `40px 40px 0 0` | `#fff` | none | `40,24,40,24` | ~313px (n=220) |
| Dark chart panel | `24px` | `#0a0a0a` | brand glow | `40` all | ~1000px |
| Standard content card | `24px` | `#fff` | none | `0` (inner padding on child) | ~373px |
| Lifted feature card | `20px` | `#fff` | card lift | `40` all | ~397px |
| Testimonial card | `24px` | `#fff` | card lift | `64,30,40,30` | ~536px |
| Split-bed card | `24px 24px 0 0` | `#373b40` | none | `0,0,32,0` | ~896px (tablet/mobile) |

---

## 6. Icon System

Identified by `viewBox` signature — different viewBox conventions mean different icon sets.

| viewBox | Family | Count of distinct icons | Sizes | Fill/stroke |
|---|---|---|---|---|
| **`0 0 256 256`** | **Phosphor Icons** — this is the house set | 11 variants | `16 · 30 · 35 · 39 · 47px` | single `<path>`, filled |
| `0 0 24 24` | Lucide/Feather-style | 3 variants | `16 · 20 · 24px` | shape primitives, filled |
| `0 0 512 512` | Font Awesome-style | 1 | `20px` | LinkedIn social icon, `#ffffff` |
| *(no viewBox)* | Inline decorative marks | 1 | `14px` | n≈339 — the small check/bullet glyph |

### Context rules — which icon appears next to what

| Context | Icon treatment |
|---|---|
| **Nav dropdown items** | Phosphor duotone, ~24px, brand blue/green — one per menu entry |
| **FAQ / list rows** | Phosphor 30px, colour-stepped across the gradient: `#82c88a → #62bc9b → #42afac → #21a3bc → #0196cd` — a 5-stop ramp used to sequence sibling rows |
| **Nav trigger (`Closed`/`Open`)** | Phosphor `35px` / `39px`, `#3d4443`; `16px` `#000` on the desktop compact variant |
| **Feature blocks** | Phosphor `47px`, `#82c88a` |
| **On dark beds** | Phosphor `30px`, `#fefffe` |
| **Carousel arrows** | 24×24 set, `20px`, `#000` |
| **Footer social** | 512-viewBox, `20px`, `#ffffff` |
| **Hero proof points** | Large outlined check circles (~60px), white on the gradient bed |

> The colour-stepped Phosphor ramp is the most distinctive icon behaviour in the system: sibling items don't share an icon colour, they walk the brand gradient.

---

## 7. Imagery Treatment

162 distinct rendered image treatments were recorded. The **style rules**, not the assets:

### Aspect ratios & crops

| Ratio | Fit | Radius | Meaning |
|---|---|---|---|
| `1.00` | `cover` | `999px` | **Testimonial avatar**, `42×42` (n=99) — the single most repeated image treatment |
| `1.00` | `cover` | `100%` | Team headshot, `90×90` / `92×92` |
| `1.00` | `cover` | `999px` | Large round portrait, `330×330` / `352×352` |
| `1.00` | `contain` | `0` | Icon-like SVG, `50×50` / `65×65` |
| `0.97` | `cover` | `0` | Client logo, `58×60` (n=24) — near-square, uncropped |
| `0.5 – 1.16` | `contain` | `0` | **Illustration SVGs**, 330–816px wide — the dominant hero/feature image type |
| `1.15` | `cover` | `0` | Photography, `667×579` / `768×667` |
| `0.68` | `cover` | `0` | Portrait-crop photography, `270×400` |

### Rules that hold

1. **Illustrations are SVG and `object-fit: contain`** — they are never cropped. Their natural aspect ratio is preserved and the container flexes around them. Widths cluster at **330px** (mobile/card), **436px**, **533px**, **816px**.
2. **Photography is raster and `object-fit: cover`** — always cropped to the container.
3. **People are always round.** Every human image is `border-radius: 999px` or `100%`. There is no square headshot anywhere.
4. **Logos are never cropped and never rounded** — `contain`/`cover` at near-1:1, `border-radius: 0`, presented in a monochrome-ish row with white edge-fade scrims (`linear-gradient(90deg, #fff, transparent)`) at the ends of the marquee.
5. **Photography is candid and human** — the homepage hero is a real person mid-laugh, held at very low contrast behind the headline (the image is effectively a texture, not a subject). Where photography appears behind type, it is **washed out to near-white** so the type carries all contrast.
6. **No image ever carries a drop shadow.** Depth comes from the container, not the picture.
7. **Overlays** are the soft tint washes from §2, applied over the image, not a flat scrim.

---

## 8. Interactive States

*All captured by driving a real mouse and re-reading computed styles — not inferred from CSS.*

### Nav link (`How It Works`, `Pricing`, `Results`)

```
rest    Museo Sans 300 · 16px/16px · #3d4443
hover   font-family → Museo Sans 700   (light → bold)
        no colour change · no underline · no background
```

**Side effect:** the bold face is wider, so sibling nav items translate horizontally (measured up to `translateX(2.41px)`). **The nav visibly reflows on hover.** This is a real layout shift, not a design intent — see §16.

### Nav dropdown (`Why Swivel`, `Compare`, `Company`)

```
trigger  hover (no click needed)
label    same 300 → 700 swap; chevron rotates ~180°
panel    #fff · radius ~20px · ambient shadow · ~268px wide · offset ~44px below nav
rows     ~80px tall · duotone Phosphor icon (~24px) + label
divider  1px rgba(34,34,34,.1) BETWEEN rows only — none at top or bottom
label    two-tone: leading words #0196cd, trailing word green/dark
         e.g. "For Sales" (blue) + "Leaders" (green)
close    latches open; closes on pointer leaving trigger+panel
```

### `⬛️ L Button Fill` — primary CTA

```
rest    212 × 60px · radius 999px · #eba343 · padding 18/40 · no icon
hover   width 212 → 240px  (+28px)
        arrow glyph slides in from the right; label shifts left
        NO colour change · NO shadow change · NO scale
        settles within ~1s (framer-motion driven)
```

This width-expand-and-reveal-arrow is **the** signature interaction of the site.

### `⬛️ S Button Fill` — nav "Book Call" / "Login"

```
rest    40px tall · radius 999px · #eba343 / #fff
hover   NO CHANGE AT ALL
```

Verified by full-subtree computed-style diff while `:hover` was confirmed on the element. **The site's most prominent conversion CTA is completely inert on hover.**

### FAQ block

Not an accordion on `/` or `/audit` — questions and answers are **always expanded**, stacked, separated by the `1px rgba(34,34,34,.1)` hairline. Question is `22px/28.6` MS700 in the brand gradient; answer is `16–18px` MS300. (The `Closed`/`Open` named variants belong to the nav and menu components, not this block.)

### Focus states

No custom `:focus-visible` styling was found on buttons or nav links; the browser default outline is what remains. Form inputs on `/login` are the only elements with a designed focus treatment.

---

## 9. Motion & Scroll Behaviour

| Mechanism | Detail |
|---|---|
| **Entrance ("Appear")** | 5 elements per page carry `data-framer-appear-id`; 79 instances site-wide. They render at `opacity: 0.001` with `will-change: transform` until triggered, then fade/translate to `opacity: 1`. |
| **Scroll-linked fades** | Additional sections (e.g. the homepage FAQ) fade in progressively as they enter the viewport, using a different mechanism than appear-ids — the opacity tracks scroll position rather than firing once. |
| **Transitions** | `transition: all` is set on ~32,700 elements — Framer's default. Real durations and easings are **JS-driven by framer-motion and are not readable from CSS.** The only explicit CSS transition is `opacity 0.2s` on carousel controls. |
| **Keyframes** | Exactly one `@keyframes` exists site-wide: `__framer-loading-spin` (Framer's internal loader). No custom keyframe animation. |
| **Stagger** | Multi-item grids do not show a measurable per-item stagger delay in the DOM; items share one appear group. |
| **Video** | The homepage carries a full-bleed autoplaying background video section (`Video Background`, 781px tall) directly beneath the hero. |

> **Caveat:** appear animations do not fire inside a same-origin iframe (they require top-level viewport events). All *values* here were verified on the top-level page; only the screenshot capture needed an override.

---

## 10. Forms & Inputs

**The site has almost no native forms.** Across 75 pages, native `<input>` elements exist on exactly **two** pages.

| Page | Fields | Styling |
|---|---|---|
| `/login` | `email`, `password` | `40px` tall · bg `rgba(10,15,30,0.5)` · border `1px solid rgba(255,255,255,0.16)` · radius `12px` · padding `12/14` · `12px` text · `#82c88a` caret/label · label `13px/15.6` MS700 `#fff` · submit `#82c88a`, radius `12px`, `38px` |
| `/pathforward-dashboard` | `password` | `38px` · bg `#fff` · border `1px solid #e4e8ec` · radius `8px` · padding `10/12` · `14px` · submit `#0d9488`, radius `8px`, `36px` |

Both are **React code components** (`PasswordGateLogin.tsx`, `Client_Dashboard.tsx`), not Framer forms — which is why they use `ui-sans-serif`, `#0d9488` and `#e4e8ec`, none of which exist in the design system.

**Every real conversion form** — `/audit`, `/contact`, `/newsletter`, `/schedule-meeting-calendar`, `/gtm-audit-start`, `/gtm-audit` — is a **third-party embed** (HubSpot / scheduling iframe). It renders inside a Framer section but its fields, validation, and error states are **not controlled by this design system at all**.

> **Consequence:** there is no design-system answer to "what does a text input look like?", "what does a validation error look like?", or "what does a multi-step form look like?" If a new page needs a native form, that pattern has to be designed — it does not exist. See §16.

---

## 11. Section & Block Taxonomy

Shared vocabulary. Names in **bold** are the actual Framer layer names; names in *italics* are proposed for recurring blocks that are currently unnamed.

| Block | Framer name | Appears on | Notes |
|---|---|---|---|
| **Hero** | `Hero`, `Section - Hero` | `/`, `/results`, `/about`, `/resources` | `160px` top padding, `1200`/`1272` rail |
| **Video Background** | `Video Background` | `/` | Full-bleed autoplay video, 781px |
| *Trusted-By Logo Bar* | `Logos` (on `/results`) | `/`, `/newsletter`, `/results` | 313px tall, `1400` rail, edge-fade scrims, ~20 client logo components |
| *Objection Banner* | — | `/` | "Does this actually work?" — 678px |
| *Problem/Solution Split* | `Challenge/Solution` (`Challenge`, `Solution`) | `/`, `/how-it-works` | "Stop managing chaos, start running a system" |
| **Stat Banner** | — | `/`, `/how-it-works` | `Heading 2b` numerals (54/48.6) + gradient; `#82c88a`/`#38aeb2`/`#0196cd` variants |
| **Why Swivel** | `Why Swivel` | `/`, `/how-it-works`, `/why-swivel/for-ceos` | Soft-tint full-span wash, `1200` rail, `120/64` padding |
| **Chart** | `Chart` | `/` | Dark `#0a0a0a` panel, radius 24, brand glow shadow, `1400` rail |
| **Just Exploring 2-Across** | `Just Exploring 2-Across` | `/` | Two-up card grid |
| **FAQs** | `FAQs`, `FAQ` | `/`, `/audit`, all 5 compare pages, all 3 persona pages | Always-open Q&A, hairline dividers, `1360` rail |
| **Testimonials** | `Testimonials` | `/how-it-works`, `/pricing`, all compare + persona pages | Also (mis)used as the generic section wrapper on compare pages |
| **Quote** | `Quote` | `/how-it-works` | Single large pull-quote, `1072` rail |
| **Case Studies** | `Case Studies` | `/newsletter`, persona pages | Card row |
| *Case Study Spotlight* | client name (`AGI`, `Buckhorn`, `Transportant`, `Leasecake`, `Abre`, `Conger`, `Dysinger`) | `/results` | 7 near-identical 1700–1830px sections, `1200` rail, `160/64/120/64` |
| **Features** | `Features` | 25+ pages | The generic content-section wrapper; also used as page hero on `/pricing`, `/audit`, `/blog`, `/contact`, all thank-you pages |
| **Easy Button** | `Easy Button` | all 5 compare pages + `/resources/hire-a-bdr…` | Closing CTA block, 561px, `739` rail |
| **Downsides** | `Downsides` | compare pages | Red `#f53434` uppercase label |
| *Versus Divider* | — | compare pages | The literal "vs" glyph, `27px/27` MS700, `59px` rail |
| **Guides** | `Guides` | `/resources` | 2294px card grid |
| **Blog — Home / Blog Articles** | `Blog - Home`, `Blog Articles`, `Blog` | `/`, `/resources`, `/blog` | CMS-driven |
| **Meet the Team** | `Meet the Team`, `Team About` | `/about` | Used twice — team grid (2684px) *and* core values (676px) |
| **Swivel Promise** | `Swivel Promise` | `/about` | "Our story" |
| **3 Values** | `3 Values` | `/about` | |
| **Our experts** | `Our experts` | `/resources` | |
| **Getting Started with Swivel** | `Getting Started with Swivel` | `/resources` | |
| **Positioned to Win** | `Positioned to Win` | `/audit` | |
| **Timeline** | `Timeline` | `/how-it-works` | |
| **Outcomes** | `Outcomes` | | |
| **Carousel** | `Carousel Controls`, `Slide Dots`, `Arrow Controls` | testimonial/case-study rows | |
| *Footer* | `Logo/Address`, `Nav Links`, `Links`, `Company`, `Compare`, partner/cert badges | every page | Dark gradient bed; `Montserrat 11px` legal row |
| *Utility Strip* | — | every page, last child | 64px tall, `1043` rail |

### Static vs CMS-driven

| Content | Source |
|---|---|
| **Blog posts** (33) | **Framer CMS** — one template; add a post as a CMS entry, never a hand-built page |
| **Blog cards** on `/`, `/resources`, `/blog` | CMS collection lists |
| **Guides** on `/resources` | Appears CMS-driven (uniform card grid) |
| **Testimonials** | **Hard-coded per section** — avatars, names and quotes are literal layers, not a collection. A new testimonial is a manual build. |
| **Case studies** on `/results` | **Hard-coded**, one named section per client (`AGI`, `Buckhorn`, …). A new case study means duplicating a ~1,750px section, not adding a CMS row. |
| **Client logos** | Hard-coded components, one per client (~20) |
| **Professional-services pages** (6) | Hand-built from one shared structure, not CMS |

> This is the most important operational finding in the taxonomy: **adding a blog post is a CMS action; adding a testimonial or case study is a design action.**

---

## 12. Content Flow & Page Narrative Patterns

### Where each block type sits

| Position | Block types |
|---|---|
| **Opening (always)** | Hero — `160px` top padding, H1 with a gradient span, 1–3 line subhead, one L button |
| **Immediately after hero** | Trust signal — logo bar or stat banner. Credibility comes *before* explanation. |
| **Early-middle** | Problem framing — "Stop managing chaos", "The major drawbacks of…", "What you're juggling…". Named negatively. |
| **Middle** | Solution / system explanation — `Why Swivel`, `Features`, `Chart`, `Timeline` |
| **Late-middle** | Proof, again — `Testimonials`, `Case Studies`, `Quote`. Trust appears **twice**: once early for credibility, once late to close objections. |
| **Penultimate** | Objection handling — `FAQs`, "We know what you're thinking", `Downsides` |
| **Closing (always)** | CTA block — `Easy Button` on compare pages, "Ready to begin?" on funnel pages, `Just Exploring 2-Across` on the homepage |
| **Always last** | Footer + 64px utility strip |

### What each page type ends with

| Page type | Ends with |
|---|---|
| Homepage | FAQs → footer |
| Compare (`/vs-*`) | FAQs → footer (after `Easy Button` mid-page) |
| Persona (`/why-swivel/*`) | FAQs → footer |
| Blog post | Related/CTA blocks → footer |
| Funnel (`/audit`, `/newsletter`, `/gtm-audit-start`) | "Ready to begin?" CTA → footer |
| Thank-you | Single content section → footer (nothing else) |
| Case-study index (`/results`) | Last client spotlight → footer, **no closing CTA** |

### The narrative arc

```
credibility → problem (named as their pain) → system (named as Swivel's) →
proof (named clients, real numbers) → objections → single next action
```

Proof is deployed **twice** and objections are handled **explicitly and by name** ("Does this actually work?", "We know what you're thinking", "The major drawbacks of BDRs"). The site argues rather than asserts.

---

## 13. Compositional Grammar — how to build something new

*The rules a never-before-seen block must follow to feel native. This is the section to use when designing new work.*

### R1 — Section skeleton

```
EYEBROW (Heading 5, 16px, +8px tracking, UPPERCASE, #666873 or a brand colour)
    ↓ ~16–24px
H2 (Heading 2, 54px desktop) — with ONE gradient <span> on the emphatic phrase
    ↓ ~24px
1–2 sentences of support copy (Body Large 20px, max ~75 characters per line)
    ↓ ~32–40px
ONE L button, OR a proof point — never both
```

Not every element is required, but **the order never changes**, and nothing else may be inserted between them.

### R2 — Background rhythm

Alternate `white` → `soft-tint wash` → `white`. Never place two tinted sections adjacent. Use a solid dark bed (`#0a0a0a` / `#2e3238`) at most **once per page**, for the single highest-impact block. Tints are always **full-span**; solid colours are always **contained**.

### R3 — The rails

Pick one and stay on it for the whole section:

- **1360** with `40px` gutters — wide content: FAQs, testimonials, card grids
- **1200** with `64px` gutters — standard content: heroes, features, case studies
- **≤1072** — measure-constrained: long-form prose, quotes, single-column CTAs

Tablet collapses everything to **896** (`64px` gutters). Mobile collapses everything to **330** (`30px` gutters).

### R4 — Emphasis hierarchy

Emphasis is created by **size first, then colour, then weight** — in that order.

- Size carries the hierarchy (90 → 54 → 36 → 26 → 20 → 16)
- Colour marks the *one* important phrase (the gradient span), not whole headings
- Weight is used sparingly, mostly to separate a lead-in from body copy
- **Never** use all three at once on the same element

### R5 — The gradient is a highlighter, not a fill

The brand gradient goes on **one phrase per heading**, never the full heading, never body copy. On backgrounds it appears only as a **15–20% alpha wash**, never at full saturation behind text.

### R6 — One CTA per section

Exactly one L button per section. The nav's S button is the only always-present second CTA. Ghost/transparent buttons are for **selection** (tabs, personas), never for a primary action.

### R7 — Cards

`radius 24px` · `background #fff` · `padding 40px` · **no border**. Add shadow #2 only when the card sits on a white bed and needs separation. On a tinted bed, use no shadow. Top-only radius (`24px 24px 0 0`) when the card is flush to a coloured bed.

### R8 — Icons

Phosphor (`viewBox 0 0 256 256`), filled, `30px` in content and `47px` in feature blocks. When a set of sibling items each take an icon, **walk them across the gradient ramp** (`#82c88a → #62bc9b → #42afac → #21a3bc → #0196cd`) rather than giving them all one colour.

### R9 — Imagery

Illustrations: SVG, `contain`, uncropped, 330–816px. Photography: raster, `cover`, desaturated/washed toward white if type sits over it. People: always `border-radius: 999px`. Logos: never cropped, never rounded. **No image gets a shadow.**

### R10 — Copy length constraints

Measured against where components actually break:

| Element | Desktop | Mobile |
|---|---|---|
| H1 hero | **3–5 words**, 2 lines at 90px | 3 lines at 40px — 5 words is the ceiling |
| H2 section | **4–8 words**, ideally 2 lines | wraps to 3 lines at 36px |
| Eyebrow | **2–5 words** — `+8px` tracking eats width fast |
| Support copy | **15–30 words** (~2 lines at 1360, 3 at 1200) | 4–5 lines |
| Card title | **3–6 words** at 26px | |
| Button label | **2–4 words** — the L button starts at 212px and grows 28px on hover; a long label makes the arrow reveal look broken |
| FAQ question | **5–10 words** at 22px |

### R11 — CTA copy

Verb-led and first-person-plural-free: *"See the System"*, *"See Pricing"*, *"Request Audit"*, *"Ask a Question"*, *"Explore guides"*, *"Read Now"*, *"Book Call"*. Benefit-led only when the offer needs qualifying: *"Get a Free Growth Audit"*. Never *"Learn more"*, never *"Submit"*.

### R12 — Interaction

New interactive elements should adopt the **width-expand + arrow-reveal** pattern for primary buttons and the **weight-swap** for text links. Do **not** invent hover colour shifts — the system has none.

---

## 14. Page Anatomy Patterns

### Template families (all 75 pages)

| Family | Count | Structure |
|---|---|---|
| **Blog post** | 33 | `[60px bar] → [article 3,400–5,400px] → [720px] → [490px]` |
| **Professional services** | 6 | `[main 2,590–4,570px] → [720] → [490] → [60]` |
| **Compare (`/vs-*`)** | 6 | `Testimonials → Testimonials → "vs" → Testimonials → Easy Button → ? → ? → FAQs → [64]` |
| **Persona (`/why-swivel/*`)** | 3 | `Features(hero) → Why Swivel → Features → ? → Features → Testimonials → FAQs` |
| **Guide thank-you** | 6 | `Features(1360 rail, 160/40/120/40, H1 "Your guide is here!") → [64]` — six are byte-identical |
| **Simple thank-you** | 4 | Same shape, shorter (H≈2,692) |
| **Unique** | 17 | `/`, `/how-it-works`, `/pricing`, `/results`, `/about`, `/resources`, `/blog`, `/audit`, `/contact`, `/newsletter`, `/schedule-meeting-calendar`, `/gtm-audit-start`, `/gtm-audit`, `/privacy`, `/login`, `/pathforward-dashboard`, `/404` |

### Reference anatomies (desktop)

**`/` (12,641px)**
`Hero` 900 · `Video Background` 781 · Logo bar 313 · Objection 678 · Problem/Solution 973 · Stat 510 · `Why Swivel` 1099 · `Chart` 876 · `Just Exploring 2-Across` 893 · `FAQs` 1826 · strip 64

**`/how-it-works` (9,420px)**
Hero 625 · `Why Swivel` 370 · "Relief." 758 · `Testimonials` 892 · `Features` 309 · Why Swivel 769 · "One partner. One hour a week." 709 · `Quote` 962 · strip 64

**`/results` (15,623px)**
`Hero` 354 · `Logos` 246 · seven client spotlights (1,691–1,831px each, all `1200` rail, `160/64/120/64`) · strip 64

**`/vs-bdrs` (6,469px)**
Drawbacks 1038 · "See how systems win" 219 · "vs" 712 · "We know what you're thinking" 758 · `Easy Button` 561 · 487 · 592 · `FAQs` 899 · strip 64

**`/privacy` (7,598px)** — single `Features` section, 6,396px, `1120` rail.

---

## 15. Responsive Behaviour

### The rails

| | Desktop 1440 | Tablet 1024 | Mobile 390 |
|---|---|---|---|
| **Content width** | `1360` / `1200` / `1072` / `1000` | **`896` (uniform)** | **`330` (uniform)** |
| **Gutter** | `40px` or `64px` | **`64px`** | **`30px`** |
| **Formula** | rail is fixed, viewport-independent | `viewport − 128` | `viewport − 60` |

Tablet and mobile abandon fixed rails entirely and become fully fluid. Only desktop has a max-width system.

### Type scaling

| Style | 1440 → 1024 → 390 |
|---|---|
| Heading 1 | `90 → 72 → 40` |
| Heading 1b | `72 → 46 → 28` |
| Heading 2 | `54 → 46 → 36` |
| Heading 3 | `36 → 28 → 28` *(tablet and mobile identical)* |
| Heading 6 | `32 → 24 → 21` |
| Body Large | `20 → 18 → 16` |
| Blog H1 | `46 → 38 → 30` |
| Blog H2 | `30 → 26 → 22` |
| Blog body | `18 → 17 → 16` (line-height `28.8 → 27.2 → 24.8`) |

**Does not scale at all:** the eyebrow (`Heading 5`, 16px/+8px), `Heading 6b` (22px, FAQ questions), `Heading 2b` (54px stat numerals), `Heading 4` at 24px, the 26px/26 heading, and all button label sizes.

Letter-spacing loosens as size drops: hero tracking goes `-3.5px → -2px → -1px`.

### Structural changes

- **Nav:** full horizontal nav + `Book Call` + `Login` on desktop → **hamburger only** on mobile. Both nav CTAs disappear.
- **Hero proof points:** 3-across with vertical dividers on desktop → **stacked vertically** on mobile.
- **Split backgrounds flatten:** `linear-gradient(#2e3238 50%, #82c88a 50%, #0196cd 100%)` becomes flat `#2e3238` on mobile.
- **Radial glows re-aim:** `radial-gradient(86% 124% at 19% 57.1%, …)` → `radial-gradient(86% 67% at 50% 43.9%, …)` — off-centre on desktop, centred on mobile.
- **Mobile-only scrim:** `linear-gradient(to top, #fefffe, transparent)` appears only at 390px.
- **72px stat numerals vanish** on mobile — the stat banner reflows to a different treatment.
- **Breadcrumb (13px) and the Montserrat 11px footer legal row are absent** on mobile.
- **New uppercase style at tablet/mobile:** `16px/24 +8px MS900 uppercase #fefffe` (n=80) has no desktop equivalent.

---

## 16. Open Questions

*Every inconsistency found, plus anything that could not be fully inspected. Nothing here has been resolved automatically — these need a human decision.*

### Inconsistent — needs a decision

1. **The brand gradient has ~15 different angles.** Same two hex values (`#82c88a` → `#0196cd`), rendered at `0 · 82 · 111 · 135 · 270 · 275 · 277 · 283 · 284 · 288(reversed) · 289 · 291 · 294 · 315` degrees, plus a no-angle vertical, plus two stop patterns (`0→100%` and `16→88%`), plus a 3-stop variant. **Should there be one canonical text gradient and one canonical fill gradient?**

2. **The primary CTA orange `#eba343` is not a Colour Style.** It is a raw hex used ~195 times — the single most important conversion colour in the system is untokenised. So is the error red `#f53434`.

3. **There is no single primary button colour.** The same `⬛️ L Button Fill` appears in orange, green, teal and blue across pages with no discernible rule ("See Pricing" green, "Request Audit" teal, "Ask a Question" blue, "See the System" orange — all n=183 on the same page). Is the colour semantic, decorative, or accidental?

4. **Four Colour Styles are named `White`; two are named `Green`.** Three parallel neutral naming schemes coexist: `Neutral 800/500`, `Neutral 01/03/04`, and `Gray`/`GrayDark2`/`Medium Grey`. Two Text Styles in the `Audit` folder are both named `Body`.

5. **`⬛️ S Button Fill` — the nav "Book Call" CTA — has no hover state whatsoever.** Verified by real hover. Intentional or an oversight?

6. **Nav links reflow the nav on hover.** The `Museo Sans 300 → 700` swap changes text width, pushing siblings sideways by up to 2.4px. Fix by reserving the bold width, or accept it?

7. **Blog post template is not uniform.** 7 of 33 posts are missing the two trailing sections (720px + 490px) that the other 26 have: `what-is-a-revenue-operating-system`, `hire-a-bdr-vs-build-a-bd-system`, `improve-warm-lead-connect-rate`, `more-meetings-from-inbound`, `calculate-cpql-google-meta`, `best-b2b-sales-agencies`, `best-hubspot-revops-agencies`.

8. **`/vs-sales-coaches` has a different structure** from the other five compare pages — it uniquely carries trailing 720px + 490px blocks.

9. **Persona pages vary structurally:** `/why-swivel/for-ceos` has 9 sections, `/for-marketers/` has 7, `/for-sales-leaders` has 13. Same page type, three different shapes.

10. **Duplicate content:** `/resources/hire-a-bdr-vs-build-a-bd-system` and `/blog/hire-a-bdr-vs-build-a-bd-system` are the same article at two URLs.

11. **`/why-swivel/for-marketers/` has a trailing slash** in the sitemap; its two siblings do not.

12. **Stray typefaces:** `Inter` (one blog post), `Fragment Mono` (one code block), `Montserrat 11px` (footer legal). None belong to the system.

13. **`Testimonials` is used as a generic section wrapper** on the compare pages — three of the four sections on `/vs-bdrs` are named `Testimonials` but contain drawbacks, comparisons and objections. The name no longer describes the content.

14. **`Meet the Team` is used for two different blocks** on `/about` — the team grid and the core-values block.

15. **Shadow #4** (`rgba(0,0,0,.25) 10px 10px 2px 0`) appears on exactly one card and matches nothing else in the system.

16. **Spacing deviates from an 8px grid** at `18`, `26`, `30`, `90` and `164`.

17. **Orphan Colour Styles:** `#071330`, `#122e76`, `#b3bcff`, `#f7cb2d`, `#1f514c` are defined but effectively unused on the public site.

### Gaps — patterns that do not exist yet

18. **There is no form design pattern.** Every real conversion form is a third-party embed. The system has no input, no label, no validation state, no error state, no multi-step pattern. If a new page needs a native form, it must be designed from scratch.

19. **There is no designed focus state** on buttons or links — keyboard users get the browser default. An accessibility gap.

20. **Semantic heading hierarchy diverges from visual hierarchy in several places** — visual size is chosen before semantic level. Notable: `/why-swivel/for-ceos` uses `<h1>` for "Objections & testimonials" mid-page (a second H1); `/` uses `<h3>` for "Trusted by Service, Tech, & MFG Companies" ahead of any `<h2>`; `/how-it-works` opens with `<h1>` then uses `<h2>` and `<h3>` interchangeably by size. `/results` uses `<h3>` for all seven case-study titles under a single `<h1>`.

### Could not be fully inspected

21. **Motion durations and easings are not measurable from CSS.** `transition: all` is set on ~32,700 elements and the actual timing is driven by framer-motion in JS. Exact durations, easing curves and stagger delays would need either the Framer editor's per-element animation panel or frame-by-frame capture.

22. **The `Blog` Text-Style folder in Framer was not expanded** — blog typography *is* bound to named styles, but those style names were not read. The measured values are in §1.

23. **Appear animations do not fire inside an iframe**, so per-breakpoint screenshots required overriding `opacity` to capture. Measurements are unaffected; only the visual capture needed the override.

24. **`/pathforward-dashboard` and `/login`** are React code components, not Framer designs. They were measured but should be treated as outside this design system.

25. **A security observation, not a design one:** `SwivelDash.tsx` in the Framer project contains a hard-coded API URL, sync secret and dashboard password as client-side constants. Worth a separate review.
