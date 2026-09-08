Planes familia — weekend-first family board for Asturias
Small, fast, local‑first web app to plan weekends with toddlers — mobile‑first, no login, deploys on GitHub Pages.

ES: Tablero ligero para familias en Asturias. Fin‑de‑semana primero, móvil, sin registro. Prueba la demo abajo.

[![Live Demo](https://img.shields.io/badge/Live_Demo-GitHub_Pages-0f766e?logo=github)](https://alvarogb.github.io/family-plans/) [![Static Site](https://img.shields.io/badge/Static%20Site-index.html-1f2937)](#tech-stack) ![Vanilla JS](https://img.shields.io/badge/Vanilla-JS%20%2F%20CSS-informational) ![No Backend](https://img.shields.io/badge/Backend-None-success) [![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](#license)

### Live demo
- https://alvarogb.github.io/family-plans/

## Problem → solution
- Parents of toddlers in Asturias often decide plans late and need a clear, urgent‑first board.
- Weekend‑first presets (Today → This weekend → 7 days → by month) surface the right items at the right moment.
- Local‑first UX: no login, nothing leaves the browser; profile and pins are stored in `localStorage`.

## Features
- Mobile‑first UI with sticky header and compact chips
- Weekend‑first presets plus quick month filters
- Pinned items surface first; optional contribution‑style “pin heatmap” pattern for history (see Architecture)
- Evergreen pool «Siempre disponibles» pattern for undated ideas (documented below)
- Local profile and pins persisted in `localStorage`
- Optional GPS: “Use my location” to auto‑set base city and filter by distance
- Type badges and subtle emojis (ticket, booked, festejo, beach, watch, aldea)
- Clear, verb CTAs (e.g., “Comprar entradas”), optional Google Calendar add on pin

## Screenshots

Drop screenshots into `docs/` and reference them here, for example:

```markdown
![Board — mobile](docs/screen-mobile.png)
![Board — desktop](docs/screen-desktop.png)
```

If you don’t have screenshots yet, here’s a simple architecture diagram instead:

```mermaid
flowchart TD
  A[User (mobile/desktop)] --> B[index.html (static)]
  B --> C[UI chrome (filters, cards, badges)]
  B --> D[Data: EVENTS (dated)]
  B --> E[Data: window.EVERGREEN (undated pool)]
  B --> F[State: localStorage (profile, pins)]
  C --> G[Filters: weekend-first, 7d, month, custom]
  C --> H[Pinned list + optional heatmap summary]
  C --> I[Optional: open Google Calendar on pin]
  J[(GitHub Pages)] --> B
```

## Tech stack
- Single static `index.html`
- Vanilla JS and CSS (no frameworks)
- GitHub Pages for hosting
- No backend; all state in `localStorage`

## Architecture
- Data:
  - `EVENTS`: dated items rendered on the board.
  - `window.EVERGREEN`: undated “Siempre disponibles” ideas (optional pool you can add; see below).
- Rendering:
  - Filters are weekend‑first by default; month chips and free‑range dates available.
  - Pins float to a dedicated section; you can also summarize pins as a small contribution‑style heatmap across weeks if desired (pure client‑side).
- Ownership:
  - Content (the events/ideas arrays) is yours to edit in the file.
  - Chrome (the UI scaffolding) is generic, static, and free to reuse.

## Getting started
- Fastest path: open the Pages URL — https://alvarogb.github.io/family-plans/
- Run locally:
  1) Fork or clone the repo
  2) Open `index.html` directly in a browser
  3) Optional: enable GitHub Pages (Pages → Deploy from main) to publish your fork

## Project structure
```
.
├─ index.html              # App (UI + data arrays)
├─ README.md               # This document
├─ docs/
│  └─ ARCHITECTURE.md      # Deeper notes and extension points
└─ LICENSE                 # MIT
```

## Contributing / content updates
- Inventory lives in `index.html`:
  - Update the `EVENTS` array for dated items (festival days, ticketed shows, one‑offs).
  - Optionally add a global `window.EVERGREEN = [ ... ]` array for undated ideas (parks, aldeas, museums). The UI can list them in a “Siempre disponibles” section or surface them as suggestions.
- Keep titles action‑oriented, add a short “why” for parents, and use types/tags to drive badges and sorting.

## License
MIT — see `LICENSE`.

## Author
Álvaro García Barbón — [@AlvaroGB](https://github.com/AlvaroGB). Built in/for Asturias, as a small family product.

---

Maintainers note (for repo settings):
- Suggested description: “Weekend‑first family plans board for Asturias — static, local‑first, vanilla JS, GitHub Pages.”
- Suggested topics: `family`, `asturias`, `static-site`, `vanilla-js`, `github-pages`, `local-first`, `parenting`
