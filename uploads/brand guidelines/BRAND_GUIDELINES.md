# Castro Group — Brand Guidelines (RS26)

> Handoff brief for Claude Code (and any engineer/designer building production
> surfaces). Companion to `colors_and_type.css`. This document captures the
> **RS26 (2025/2026)** palette refresh introduced on the cover of `RS26_identidade_capa_11maio.pdf` and the visual system from `Palette.pdf`.

---

## 1. What changed from RS25

The 2024 / RS25 system used a **mint + green + lavender + purple** ESG palette on a warm off-white (`#f9f7f4`) background.

The 2025 / **RS26** system is a **four-color flag system** on a **warm putty** background.

| Role | RS25 | **RS26** |
|---|---|---|
| Page background | `#f9f7f4` warm off-white | **`#D8D5CC` warm putty** |
| Primary anchor | `#1a1a1a` near-black | **`#2E4791` navy** |
| Pillar 1 | `#00b86e` green (Environmental) | **`#FB7622` orange** (Castro Group) |
| Pillar 2 | `#7c4ddb` purple (Social) | **`#0E99D8` cyan** (Situação Atual) |
| Pillar 3 | `#9e8fd4` lavender (Governance) | **`#33B67A` green** (Creating Tomorrow) |
| Accent | `#00909a` teal | **`#CC512C` rust** |

**Mental model:** RS25 was a pastel + jewel-tone editorial. RS26 is a **bolder, flag-like, four-block identity** — like a tricolore stacked over a putty page, anchored in navy.

The legacy ESG colors (purple, lavender, teal) are **preserved** as `--cg-esg-*` tokens for back-compat with ESG materiality / pillar widgets only. **Do not introduce them into new RS26 chrome.**

---

## 2. The RS26 palette

### Brand flag (use saturated, full-bleed)

| Token | Hex | Role |
|---|---|---|
| `--cg-navy`   | `#2E4791` | Anchor. Cover top band, headings, primary CTAs, dark surfaces |
| `--cg-orange` | `#FB7622` | "Castro Group" pillar — org, structure, history |
| `--cg-cyan`   | `#0E99D8` | "Situação Atual" pillar — current state, data, KPIs |
| `--cg-green`  | `#33B67A` | "Creating Tomorrow" pillar — future, impact, targets |
| `--cg-rust`   | `#CC512C` | Secondary accent — map dots, landbank, density marks |

### Neutrals

| Token | Hex | Role |
|---|---|---|
| `--cg-putty`   | `#D8D5CC` | **Page background. Never use pure `#fff`.** |
| `--cg-putty-2` | `#CECDC9` | Slightly cooler putty — alternating bands, card bg |
| `--cg-bone`    | `#EFEDE6` | Light cream — inverse cards, table stripes |
| `--cg-ink`     | `#1A1F2E` | Primary text — near-navy black. **Never use `#000`.** |
| `--cg-mid`     | `#6B7280` | Secondary text / mute |
| `--cg-border`  | `#C7C4BA` | Hairline on putty |

### Dark surfaces

| Token | Hex | Role |
|---|---|---|
| `--cg-dark`      | `#2E4791` | Default dark surface = navy |
| `--cg-dark-deep` | `#1F3170` | Deeper navy for hover / pressed |
| `--cg-dark-ink`  | `#14182A` | Hero overlays |

### Tag tints (light pills on putty)

```
.cg-pill.orange  → bg #FBE3D2  / fg #B0451A
.cg-pill.cyan    → bg #CFE9F6  / fg #0C6C9B
.cg-pill.green   → bg #CDEBD8  / fg #1D7E4F
.cg-pill.navy    → bg #D6DCEC  / fg #2E4791
.cg-pill.rust    → bg #F0D2C5  / fg #8E3A1F
```

---

## 3. Usage rules

### Backgrounds
- **`--cg-putty` is the page.** Sections alternate `putty ↔ putty-2 ↔ bone ↔ navy`.
- **Saturated bands** (orange / cyan / green / navy) are reserved for:
  - the cover identity strip,
  - chapter dividers,
  - "wins" callouts and full-bleed quote panels.
  They are **full-bleed and never rounded** (`--cg-r-band: 0px`).
- **One gradient is allowed**, only inside data viz: `linear-gradient(--cg-cyan → --cg-green)` to express "current → future". No chrome gradients.

### Text on color
- **White (`--cg-on-color`)** on `navy`, `orange`, `cyan`, `green`, `rust`. Always.
- **Ink (`--cg-ink`)** only on `putty`, `putty-2`, `bone`.
- Never put `cg-ink` on `cyan` or `orange` — contrast fails.

### Pillar identity
RS26 pillars are carried by **colored bands** + **8px dots** + **typographic labels** — never by emoji or icons.

| Section | Band color | Dot color |
|---|---|---|
| Castro Group | `--cg-orange` | `--cg-orange` |
| Situação Atual | `--cg-cyan` | `--cg-cyan` |
| Creating Tomorrow | `--cg-green` | `--cg-green` |

If a section needs **all three at once** (e.g. table of contents), stack the bands left-to-right in the order Castro → Situação → Tomorrow — the exact cover order.

### Headings
Unchanged from RS25:
- Helvetica Neue **light 300**.
- One phrase wrapped in `<strong>` (weight 700) per heading.
- The italic Instrument Serif numeral (`01`, `02`, `03`) is the **only** typographic contrast in the system. In RS26 it is **navy**, not green.

### Numbers
Numbers stay the hero. `38–52px` Helvetica light, `--cg-ink` color, `--cg-mid` unit suffix. KPI cards now use **navy hairlines** instead of green.

### Quotes
- Guillemets (`«…»`), never curly quotes.
- Left rule **3px solid `--cg-navy`** (was green in RS25).
- Italic body.
- On a color band, use `.cg-quote.on-color` — rule becomes `rgba(255,255,255,0.6)`.

### Borders & corners
- Corners stay **2px** (`--cg-r-xs`). Bands are `0px`. Pills are `24px`.
- Hairlines do all the work. **No card shadows** except modals.
- The right-edge vertical accent bar (RS25 teal) is now **navy** at 28px width.

### Iconography
**Still zero icon files.** Pillar identity = colored dot. Trends = unicode arrows (`↓ ↑ ↗`). Frameworks = typographic chips. No emoji ever.

If a downstream surface needs additional icons, substitute **Lucide at 1.5px stroke, 16–20px, recoloured to `--cg-ink` or `--cg-mid`** — and flag the substitution.

### Motion
Unchanged. Easing `cubic-bezier(0.4, 0, 0.2, 1)`. Fade-up entrances, 1.4s bar fills, counter increments on KPIs. No springs, no rotation.

---

## 4. Component recipes

### Cover-strip header
```html
<header class="cg-cover">
  <div class="cg-band navy">
    <p class="cg-quote on-color">«The best way to predict the future is to create it.»</p>
    <span class="cg-caption" style="color:rgba(255,255,255,.7)">Peter Drucker</span>
  </div>
  <div class="cg-cover-body">
    <h1 class="cg-cover-title">Relatório de <strong>Sustentabilidade</strong> 2025</h1>
  </div>
</header>
```

### Three-pillar nav (TOC / chapter index)
```html
<nav class="cg-pillar-nav">
  <a class="cg-band orange">Castro Group</a>
  <a class="cg-band cyan">Situação Atual</a>
  <a class="cg-band green">Creating Tomorrow</a>
</nav>
```
The three blocks are equal-width, full-bleed, no gap.

### KPI card (RS26)
- Putty background, `1px solid --cg-border-soft` hairline.
- Eyebrow in navy at 70%, 9px, 0.22em tracking.
- 52px light number in `--cg-ink`.
- Unit suffix in `--cg-mid`.
- Trend arrow in pillar color (`--cg-green` for ↓ emissions, `--cg-cyan` for ↑ neutral, `--cg-rust` for ↑ warning).

---

## 5. Accessibility

- **Body text contrast:** `--cg-ink #1A1F2E` on `--cg-putty #D8D5CC` → ratio ≈ 9.8:1 ✅
- **Mid text:** `--cg-mid #6B7280` on putty → ≈ 3.5:1 — use only for ≥14px / non-essential.
- **White on saturated bands:**
  - on navy → ≈ 9.2:1 ✅
  - on orange → ≈ 3.2:1 — use ≥18px / 600 weight only
  - on cyan → ≈ 2.9:1 — **use ≥24px / 700 weight only, or fall back to navy text**
  - on green → ≈ 2.7:1 — **use ≥24px / 700 weight only, or fall back to navy text**
  - on rust → ≈ 4.6:1 ✅ for ≥14px
- **Never** combine orange / cyan / green text *with each other* — they vibrate.

For any UI control text < 18px sitting on cyan or green, **switch the band to navy** or move the text off the band.

---

## 6. PT / EN, copy, casing

Unchanged from RS25. Sentence case for body and headings. ALL CAPS w/ wide tracking for eyebrows and pills. PT primary, EN peer translation (`data-pt` / `data-en`). Decimals with commas. Currency suffix `€`. No emoji.

The three pillar names are **proper nouns** and stay capitalised in both languages:

| PT | EN |
|---|---|
| Castro Group | Castro Group |
| Situação Atual | Current Situation |
| Creating Tomorrow | Creating Tomorrow |

---

## 7. Asset inventory

- `colors_and_type.css` — RS26 tokens (current).
- `colors_and_type.RS25.css` — previous tokens, archived.
- `assets/photos/` — unchanged portfolio photography (BUZ, SPARK, The Breeze, Valpark, Fuse Valley, Palacete 31, Villa Bloom, Villa Chloe) + portraits (Paulo Castro, Fernanda Zelaya).
- `assets/brand/` — Castro Group wordmark (logo).
- `preview/` — RS25 spec cards — **flag**: these still show the old palette and will need to be regenerated against the RS26 tokens.
- `ui_kits/report/` — RS25 demo composition — **flag**: will need a RS26 pass.
- `uploads/RS26_identidade_capa_11maio.pdf` — source cover identity.
- `uploads/Palette.pdf` — source palette document.

---

## 8. Open questions for the brand team

1. **Logo lockup on putty** — confirm the existing Castro Group wordmark holds on `#D8D5CC`, or supply a navy version.
2. **Photography grade** — RS25 photos are warm golden-hour. Against the cooler navy/cyan palette, do we re-grade slightly cooler, or keep warm for contrast?
3. **ESG widget retirement** — should we phase out the purple/lavender ESG identity entirely and remap Environmental/Social/Governance onto green/cyan/orange? Currently kept side-by-side; a decision should land before RS26 publish.
4. **Rust (`#CC512C`)** — used sparingly on landbank maps in the source. OK to extend to other "real-estate" data marks (sqm, units), or keep as map-only?
5. **Cover wordmark size** — `--cg-display-cover` is set to `clamp(56px, 6.5vw, 96px)`. Confirm with print spec from the print partner.
