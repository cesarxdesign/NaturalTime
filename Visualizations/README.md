# Visualizations

Models used to work out the ideas behind Natural Time. They aren't part of the watch.

Run locally from the repo root (`python3 -m http.server 4191`), or open on GitHub Pages. Test links: `#lisbon` (view), `?time=imprint` (mode), `?t=2026-06-21T12:36Z` (moment).

## globe.html: where the sun is overhead

A 3D Earth (three.js r128) lit by a sun on the right. Sun maths: the same NOAA formulas as the watch.

Live: https://cesarxdesign.github.io/NaturalTime/Visualizations/globe.html

### 4 views (top right, or `#axis` / `#spin` / `#around` / `#lisbon` in the URL)

| View | Earth | Sun | Light |
|---|---|---|---|
| **Spin · axis still** | turns once a day, axis upright on screen | moves up and down with the season | always on: half the globe is lit |
| **Spin · axis moves** | turns once a day under a still sun | fixed on the right; the axis leans toward it in June, away in December, sideways at the equinoxes | always on |
| **Lisbon · sun around** | held still, Lisbon's meridian (blue line) facing you | goes round Earth once a day, at that day's height | real: Lisbon goes dark when the sun goes behind |
| **Lisbon · sun up/down** | held still, Lisbon's meridian facing you | sits on Lisbon's meridian at that day's point of the figure-8: high in June, low in December, nudged sideways by the equation of time | follows Lisbon's sun height: brightness grows with sin(sun height), as sunlight on flat ground does, so it peaks at peak sun and is weaker on winter noons. Scaled to Lisbon's highest sun of the year (74.7°). Below the horizon a dim glow (12%, a display choice) fades out by −12° |

The 2 Lisbon views also show 2 panels (bottom left):

- **Lisbon, the year:** every day of the year across, sun time 00–24 down, painted sun (amber), twilight to −12° (blue) and dark. The top line gives the year's shares (sun 51%, twilight 9%, dark 40%). A line and dot mark now.
- **Lisbon sky:** the sun's height over Lisbon from 00:00 to 24:00 sun time, the horizon, the −12° line, and where the sun is now (filled by day, hollow otherwise). The sky colour follows the sun's height.

To watch Lisbon's sun and dark over the year with the globe still: **Lisbon · sun up/down**, **Day**, and push **Speed** up. The sun climbs and drops along the 8 with the season while the light goes on and off each day.

### 5 time modes (panel, or `?time=` in the URL)

| Mode | Speed | What it shows |
|---|---|---|
| **Pause** | stopped | the chosen moment; drag the timeline |
| **Day** | 1 day every 8 s up to 3 days a second (Speed slider; a year in 49 min down to 2 min) | day and night, and at the top speeds the season too |
| **Year** | 30 days a second, about 12 s a year | the season |
| **Year in 2 s** | 182.5 days a second | the season, with a fading light trail behind the sun, the ground point under it and the axis tip |
| **Imprint** | still | a timelapse photo: 1 dot a day for the whole year, for the sun, the ground point and the axis tip |

Day stops at 3 days a second because faster each frame skips too much of the day: the light would strobe instead of showing dawn and dusk.

Year, Year in 2 s and Imprint step a day at a time at the same clock time as the year path (12:00 UTC in the spin views, Lisbon mean noon in the Lisbon views), so Earth doesn't blur through day and night. That's what draws the figure-8: in the Lisbon views the sun's imprint is the 8 in Lisbon's sky; in "axis moves" the axis tip draws a ring, because seen from the sun the axis turns once a year.

### What's drawn

- **Overhead band (amber):** where the sun is straight overhead today. On any one day it's a straight parallel at the sun's declination.
- **Equator** (dashed) and **tropics** at 23.4° N and S: the band never leaves the tropics.
- **Year path (thin amber, toggle "Year path"):** where the sun is overhead at the same clock time every day of the year. It's a figure-8 (the analemma): up and down from the tilt, sideways from the equation of time. Drawn at 12:00 UTC in the spin views and at Lisbon mean noon in the Lisbon views, so there it sits on Lisbon's meridian.
- **Lisbon** (blue dot).

### Controls

- **Tilt 23.4°:** off puts the axis upright. The band stays on the equator all year, the 8 collapses to a short sideways line (only the orbit's eccentricity left), and every place gets about 12 hours of day.
- **Timeline:** drag to any day of 2026. Marks show the equinoxes and solstices, the months, and Earth's closest (3 Jan) and farthest (6 Jul) points from the sun. Click a mark to jump to it.
- **Drag** the globe to turn the camera. **Reset view** (or double-click) puts the camera back.

### Readouts

The date, the latitude where the sun is overhead (declination), Earth–sun distance, and Lisbon's daylight for that day (sunrise to sunset, refraction included): 9h28 in December to 14h50 in June.

### What it shows for NT

- No place on Earth keeps the same day length, sun height or temperature all year. The equator comes closest: about 12h07 of daylight every day. Geometry fixes it near 12h; the extra minutes come from refraction, which adds about 7 minutes everywhere.
- Peak sun and lowest sun (the sun crossing your meridian) are the only markers that happen every day everywhere. That's why NT anchors 12:00 and 00:00 on them.
- The hottest belt (the thermal equator) is not the overhead band: it bends with land and sea. Not drawn.
