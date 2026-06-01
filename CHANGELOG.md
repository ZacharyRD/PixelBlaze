# Changelog

All notable changes to the **PixelBlaze-Patterns** repo. Format follows
[Keep a Changelog](https://keepachangelog.com/). Entries note what changed and
*what was learned* — for fixes, the root cause and the guardrail.

## [1.0.0] - 2026-06-01

### Added
- `patterns/general/` — standalone patterns: Honeycomb (2D/3D with palette
  crossfade), KITT RGB, Xorcery, Oasis Drift, Real World Lights, Spiral Twirls.
- `patterns/infinite-mirror-table/` — patterns for a 326-pixel WS2815 rectangle
  perimeter (the infinite-mirror-table build, sides 106/57/106/57):
  - `mirror-table-2D-map.js` — perimeter pixel map (long side first, clockwise).
  - `mirror-table-warm-wash.js` — calm ambient warm wash that crossfades four
    distinct warm palettes.
  - `mirror-table-ember-flicker.js` — glowing-coals look (layered Perlin noise,
    heat→color mapping).
  - `mirror-table-teleport.js` — a slow → accelerate → fast-peak → calm envelope
    with a multi-palette crossfade.

### Lessons (infinite-mirror-table)
- **12V WS2815 at 144/m** draws ~2.4× less current than 5V for the same brightness;
  no visible voltage drop on this short perimeter run (single feed was fine).
- **Perlin motion drifts its coordinate slowly** via bounded accumulation
  (`z = (z + delta/1000*rate) % 256`) — never `time()*256`, which strobes.
- **Scrolling a non-cyclic palette seams** at the wrap; sweep with `triangle()`.
- **Closed loops** (perimeter) need integer spatial frequencies and one shared
  coefficient-1 phase, or the wiring joint and scroll-wrap jump.
- **Input controls need an exported, name-matched backing var** (`inputNumberPalette`
  ↔ `export var palette`) or the widget displays uninitialized-memory garbage.
- **Palette-blending patterns** ship with `Auto Cycle` + `Random Palette` toggles and
  a `Palette #` input; a one-shot startup makes a random start win over the restore.
