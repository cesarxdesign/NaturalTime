# Visualizations

Models used to work out the ideas behind Natural Time. They aren't part of the watch.

Run locally from the repo root (`python3 -m http.server 4191`), or open on GitHub Pages.

## globe.html: where the sun is overhead

A 3D Earth (three.js r128) lit by a sun on the right. Sun maths: the same NOAA formulas as the watch.

Live: https://cesarxdesign.github.io/NaturalTime/Visualizations/globe.html

### 2 views (top right, or `#spin` / `#lisbon` in the URL)

| View | Earth | Sun | Light |
|---|---|---|---|
| **Spinning Earth** | turns once a day under a still sun | fixed on the right | always on: half the globe is lit |
| **Lisbon, still** | held still, Lisbon's meridian (blue line) facing you | sits on Lisbon's meridian at that day's point of the figure-8: high in June, low in December, nudged sideways by the equation of time | follows Lisbon's sun height: dark below −12° (nautical night), full by +6° |

The Lisbon view also shows a **sky panel** (bottom left): the sun's height over Lisbon from 00:00 to 24:00 sun time, the horizon, the −12° line, and where the sun is now (filled by day, hollow otherwise). The sky colour follows the sun's height.

### What's drawn

- **Overhead band (amber):** where the sun is straight overhead today. On any one day it's a straight parallel at the sun's declination.
- **Equator** (dashed) and **tropics** at 23.4° N and S: the band never leaves the tropics.
- **Year path (thin amber, toggle "Year path"):** where the sun is overhead at the same clock time every day of the year. It's a figure-8 (the analemma): up and down from the tilt, sideways from the equation of time. Drawn at 12:00 UTC on the spinning globe and at Lisbon mean noon on the still view, so there it sits on Lisbon's meridian.
- **Lisbon** (blue dot).

### Controls

- **Tilt 23.4°:** off puts the axis upright. The band stays on the equator all year, the 8 collapses to a short sideways line (only the orbit's eccentricity left), and every place gets about 12 hours of day.
- **Play day:** 1 day every 8 s.
- **Play year:** 30 days a second.
- **Timeline:** drag to any day of 2026. Marks show the equinoxes and solstices, the months, and Earth's closest (3 Jan) and farthest (6 Jul) points from the sun. Click a mark to jump to it.
- **Drag** the globe to turn the camera; double-click to reset.

### Readouts

The date, the latitude where the sun is overhead (declination), Earth–sun distance, and Lisbon's daylight for that day (sunrise to sunset, refraction included): 9h28 in December to 14h50 in June.

### What it shows for NT

- No place on Earth keeps the same day length, sun height or temperature all year. The equator comes closest: about 12h07 of daylight every day. Geometry fixes it near 12h; the extra minutes come from refraction, which adds about 7 minutes everywhere.
- Peak sun and lowest sun (the sun crossing your meridian) are the only markers that happen every day everywhere. That's why NT anchors 12:00 and 00:00 on them.
- The hottest belt (the thermal equator) is not the overhead band: it bends with land and sea. Not drawn.
