# TServe Labs — Marketing Style Guide

A reference for visual identity across the website, printed documents, and any future marketing materials.

---

## Color Palette

| Name | Hex | Usage |
|---|---|---|
| Court | `#180a04` | Page / document background |
| Panel | `#200e06` | Card and panel backgrounds |
| Accent | `#c9e52a` | Primary brand color — headings, links, badges, CTAs, bullet arrows, step circles |
| Glow | `#f97316` | Secondary accent — gradient highlights |
| Sky | `#38bdf8` | CourtIQ product color only |
| Green | `#34C759` | Status / success indicators |
| Foreground | `#faf5ee` | Body text, primary headings |
| Mid | `rgba(250,245,238,0.72)` | Secondary body text |
| Dim | `rgba(250,245,238,0.50)` | Footer and metadata text |
| Border | `rgba(194,98,45,0.3)` | Card borders, section dividers |

---

## Typography

### Typeface

System font stack — no external font loaded:

```
-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif
```

Renders as **SF Pro** on macOS/iOS, **Segoe UI** on Windows.

### Type Scale

| Element | Size | Weight | Letter-spacing | Color | Notes |
|---|---|---|---|---|---|
| Document title (`.doc-title`) | `2em` | 700 | `-0.02em` | Accent | Includes logo; see Document Headers |
| Document type (`.doc-type`) | `1.1em` | 700 | `+0.14em` | Foreground | Uppercase |
| Section heading (h2) | `0.72em` | 700 | `+0.08em` | Accent | Uppercase; pill background; see below |
| Sub-heading (h3) | `1em` | 600 | — | Accent | Prefixed with step counter circle; counter resets on each h2 |
| Body text | `11pt` | 400 | — | Foreground | Line-height 1.6 |
| Secondary text | `1em` | 400 | — | Mid | — |
| Labels / meta | `0.85em` | 400 | — | Dim | — |

### Section Headings (h2)

Styled to match the `.project-tag` elements on the website — pill with subtle accent background spanning the full content width.

```css
h2 {
  display: block;
  font-size: 0.72em;
  font-weight: 700;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--accent);
  background: rgba(201,229,42,0.1);
  border-radius: 6px;
  padding: 3px 10px;
}
```

When an h3 immediately follows an h2, reduce its top margin to avoid excess space: `h2 + h3 { margin-top: 8px; }`.

### Sub-headings (h3)

Used for numbered steps within a section. Auto-numbered via CSS counter (resets on each h2) with a filled accent-color circle prefix.

```css
h2 { counter-reset: step; }
h3 { counter-increment: step; }
h3::before {
  content: counter(step);
  background: var(--accent);
  color: var(--court);
  border-radius: 50%;
  font-size: 0.78em;
  font-weight: 700;
}
```

---

## Links

- Color: Accent (`#c9e52a`)
- Text decoration: none (no underline)
- Hover (web only): opacity transition, `0.15s`
- Footer links: Dim color → Foreground on hover

---

## Lists

### Unordered lists

Use `→` as the bullet, in accent color, matching the website's `li::before` treatment.

```css
ul { list-style: none; }
ul li::before { content: "→"; color: var(--accent); }
```

### Ordered lists

Numbers in filled accent-color circles with dark court-color text.

```css
ol { list-style: none; counter-reset: step; }
ol li::before {
  content: counter(step);
  background: var(--accent);
  color: var(--court);
  border-radius: 50%;
  font-size: 0.78em;
  font-weight: 700;
}
```

---

## Icons

No icon library is loaded. Use inline SVG for functional icons (e.g. email, globe). Stroke icons — `stroke="currentColor"`, `fill="none"`, `stroke-width="2"`, `stroke-linecap="round"`, `stroke-linejoin="round"`. Size: `15×15` or `16×16` for inline use.

The company logo (`logo.svg`) is an inline SVG — embed directly in HTML rather than referencing as an external file.

Decorative icons in web content use emoji (e.g. 🎾, 📱).

---

## Layout

### Spacing

- Document / page body padding: `48px` top/bottom, `56px` left/right
- Section margin-top: `32px`
- Paragraph margin-bottom: `10px`
- List item margin-bottom: `5px`
- All body content (p, ul, ol, h3, .contact-block) uses `padding-left: 10px` to align with the start of h2 heading text

### Dividers

- Standard rule: `1px solid rgba(194,98,45,0.3)` — used between major document sections where needed
- h2 headings use a pill background instead of a border-bottom; avoid adding `---` between sections

### Cards / Panels

- Background: Panel (`rgba(32,14,6,0.85)`)
- Border: `1px solid rgba(194,98,45,0.3)`
- Hover glow: `rgba(201,229,42,0.06)`

---

## Document Headers

Client-facing documents use a single-line header: company name + logo left-aligned, document type right-aligned, vertically centered.

```html
<div class="doc-header">
  <span class="doc-title">
    <!-- inline logo SVG -->
    TServe Labs
  </span>
  <span class="doc-type">Engagement Proposal</span>
</div>
```

```css
.doc-header { display: flex; align-items: center; justify-content: space-between; }
.doc-title   { display: flex; align-items: center; gap: 8px; font-size: 2em; font-weight: 700; letter-spacing: -0.02em; color: var(--accent); }
.doc-type    { font-size: 1.1em; font-weight: 700; letter-spacing: 0.14em; text-transform: uppercase; color: var(--fg); }
```

- No title rule or separator after the header — the first h2 provides enough visual break
- Avoid descriptive titles like "How We Work Together" — the document type label is sufficient

---

## Voice & Tone

- Direct and factual — no marketing superlatives
- No self-congratulatory statements about quality or standards
- Client-facing copy should inform, not impress
- Avoid phrases like "we believe we can do the work well" or "good projects require a good client"
- Avoid referring to "a TServe Labs project" — just say "the project"
- Framing should be mutual, not one-sided — e.g. "whether it makes sense to work together" not "whether TServe Labs is the right fit"
- Discovery calls ask clients about **the end result they're trying to achieve** and **what they've already tried** — not vague goal-setting language like "what success looks like"
- Keep copy concise — if a clause can be cut without losing meaning, cut it

---

## Document Production

PDF documents are generated from Markdown using `md-to-pdf` with Puppeteer.

- Source: `.md` files with YAML front matter specifying PDF options
- Theme: `pdf-theme.css` (lives in the same directory)
- Command: `npx md-to-pdf <filename>.md`
- Output: `.pdf` alongside the source `.md`

Front matter template:

```yaml
---
pdf_options:
  format: Letter
  margin: 0
  printBackground: true
stylesheet: pdf-theme.css
---
```
