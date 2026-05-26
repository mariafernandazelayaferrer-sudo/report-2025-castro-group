# Castro Group — Sustainability Report 2025

Single-page sustainability report. Vanilla HTML/CSS/JS, no build step.

## Architecture
- `index.html` — entire site in one file (~360KB, ~6400 lines)
  - 2 inline `<style>` blocks (head + body — keep them in sync if both edited)
  - 6 inline `<script>` blocks; the Firebase ESM module is at the top
- `pausa.html`, `projects.html` — secondary pages
- `assets/`, `uploads/` — images, brand, favicons

## Design tokens (CSS vars in `:root`)
- Brand: `--cg-navy #2E4791`, `--cg-orange #FB7622`, `--cg-cyan #0E99D8`, `--cg-green #33B67A`, `--cg-rust #CC512C`
- Neutrals: `--cg-putty` (bg) / `--cg-bone` (cards) / `--cg-ink` (text) / `--cg-mid` (muted) / `--cg-border`
- Fonts: `Inter` body, `Instrument Serif` display (both loaded from Google Fonts with italic axes)

## Scroll/animation stack (loaded via CDN at bottom of body)
- Lenis 1.1.13 — smooth scroll synced with GSAP ticker
- GSAP 3.12.5 + ScrollTrigger
- All inside a single self-contained IIFE; degrades gracefully if CDN fails

## Firebase / Firestore
- Project: `report-2025-7f49a` (default database)
- Collections: `meta/visitor-counter` (atomic counter, transaction-based) and `comments-public`
- Rules require `body.size() <= 500` for comments and increment-only writes on counter
- `window.fbApi` exposes `{ db, collection, addDoc, query, orderBy, limit, onSnapshot, serverTimestamp, doc, runTransaction }` after the `firebase-ready` event

## Storage namespaces (versioned with `-public` suffix for resets)
- `localStorage cg-opiniao-2025-public` — visitor state (id, votes)
- `localStorage cg-opiniao-comments-2025-public` — local fallback for comments
- Counter URL fallback: `api.counterapi.dev/v1/castro-group/rs2025-public/up`

## Conventions
- User input always lands in `textContent`, never `innerHTML`
- New scroll/marquee features should respect `prefers-reduced-motion`
- For full-bleed elements use negative margins `calc(50% - 50vw)` — body already has `overflow-x: hidden`
- Use existing `animateCount`, `.fade-up`, `.stagger` patterns; the page has an IntersectionObserver that auto-applies them

## Deploy
- GitHub Pages from `main` branch root
- After push, force a fresh build with `POST /repos/{owner}/{repo}/pages/builds` (HTTP 201) — bypasses any stuck workflow queue
- Builds with `status: errored, duration: 0` mean the Pages queue is stuck; the direct POST clears it
- `Cache-Control: max-age=600` on Pages assets → users need a hard refresh after deploy
