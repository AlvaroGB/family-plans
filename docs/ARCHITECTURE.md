Architecture overview

Purpose
- A tiny, static, local‑first planner for parents in Asturias. Single `index.html` served by GitHub Pages. No backend or build step.

Key concepts
- Data arrays (content you own)
  - EVENTS (required): dated items displayed on the board.
  - window.EVERGREEN (optional): undated “Siempre disponibles” ideas.
- UI chrome (generic scaffolding)
  - Mobile‑first, sticky header, preset chips (Importante, Este finde, 7 días, meses).
  - Cards with badges, urgency tag, and verb CTAs (e.g., “Comprar entradas”).
  - Optional Google Calendar add when pinning.
- State (local‑first)
  - `localStorage` keys: `family-plans-profile-v1` and `family-plans-pinned-v1`.
  - Profile holds board title, base city, adults, radius minutes, and kids (name + birth year).

Data model
- EVENTS example (excerpt from `index.html`):

```js
const EVENTS = [
  {
    id: "muja",
    title: "MUJA — Pequeños chefs",
    start: "2026-09-13", end: "2026-09-13",
    times: "13:00–13:45 · reservado",
    why: "Taller 4–11 para {{kid0}}. {{kid1}} puede acompañar si aguanta.",
    place: "Colunga",
    locKey: "colunga",      // resolved to lat/lng for distance filter
    priority: 95,           // sorts within a day
    type: "booked",         // drives badge color
    tags: ["booked"],       // extra flags: urgent, soon, ticket, festejo, beach, watch, aldea
    link: "https://...",    // optional CTA
    linkLabel: "MUJA"
  }
];
```

- EVERGREEN pattern (optional):

```js
window.EVERGREEN = [
  {
    id: "parque-invierno",
    title: "Parque de Invierno",
    why: "Paseo amplio con juego; perfecto para sobremesa sin reloj.",
    place: "Oviedo",
    type: "aldea" // or a new lightweight type
  }
];
```

Rendering & sorting
- Presets:
  - Importante (default): next 21 days, urgency + booked + ticket bias.
  - Este finde: Saturday–Sunday window, priority‑first.
  - 7 días and month chips: quick horizon filters.
  - Custom date range: free selection (desktop inline; mobile toggled).
- Grouped by day; cards sorted by date, then `priority` descending.
- Pinned items float to their own section.

Distance filter
- Base city is resolved to coordinates (`HOME_CITIES`/`PLACES` table).
- Optional “Use my location” sets the nearest known base.
- Filter keeps events within `radiusMin` minutes (≈ km heuristic).

Pins and calendar
- Pins persist in `localStorage`.
- When “Calendar on pin” is enabled in the profile, pinning opens a prefilled Google Calendar event (all‑day or ~90‑minute slot from first parsed time).

Extension points
- “Pin heatmap”: summarize daily/weekly pin counts as a tiny contribution‑style matrix (pure client‑side; uses the same localStorage pins set).
- Evergreen pool display: add a “Siempre disponibles” panel that lists `window.EVERGREEN` ideas beneath dated items.
- Types: extend the small `type → badge` map for new categories.

Ownership note
- You own the content arrays (`EVENTS`, optional `window.EVERGREEN`).
- The app’s chrome and logic are generic and intentionally minimal so families can fork and maintain their own inventory. 
