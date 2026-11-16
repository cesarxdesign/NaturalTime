# Visualizations

Models used to work out the ideas behind Natural Time. They aren't part of the watch.

Run locally from the repo root (`python3 -m http.server 4191`), or open on GitHub Pages. Test links: `#lisbon` (view), `?time=imprint` (mode), `?t=2026-06-21T12:36Z` (moment).

## globe.html: where the sun is overhead

A 3D Earth (three.js r128) lit by a sun on the right. Sun maths: the same NOAA formulas as the watch.

Live: https://cesarxdesign.github.io/NaturalTime/Visualizations/globe.html

### 5 views (top right, or `#axis` / `#spin` / `#around` / `#lisbon` / `#orbit` in the URL)

| View | Earth | Sun | Light |
|---|---|---|---|
| **Spin · axis still** | turns once a day, axis upright on screen | moves up and down with the season | always on: half the globe is lit |
| **Spin · axis moves** | turns once a day under a still sun | fixed on the right; the axis leans toward it in June, away in December, sideways at the equinoxes | always on |
| **Lisbon · sun around** | held still, Lisbon's meridian (blue line) facing you | goes round Earth once a day, at that day's height | real: Lisbon goes dark when the sun goes behind |
| **Lisbon · sun up/down** | held still, Lisbon's meridian facing you | sits on Lisbon's meridian at that day's point of the figure-8: high in June, low in December, nudged sideways by the equation of time | follows Lisbon's light as the eye sees it (below) |

**Light in "sun up/down", as the eye sees it.**

1. Light on flat ground under a clear sky, in lux. Sun up: 100,000 × sin(sun height) × (1 AU ÷ distance)² for the direct sun, plus 400 for the sky at the horizon. So it peaks at peak sun, is weaker on winter noons, and is about 7% stronger at the closest point (3 Jan) than the farthest (6 Jul). Twilight: published clear-sky values, joined smoothly: 0° about 400 lux, −6° about 3, −12° about 0.03, −18° and below 0.002 (moonless night). Sources: [AMS glossary, civil twilight](https://glossarystaging.ametsoc.net/wiki/Civil_twilight), [NRC, NAP chapter](https://www.nap.edu/read/1037/chapter/3).
2. Shown on a log scale, the way eyes and cameras respond, from moonless night to Lisbon's brightest noon (21 June). Brightness: June noon 100%, December noon 96%, sun 10° up 91%, sunrise 69%, end of civil twilight 41%, end of nautical twilight 15%, −18° 0%. The Lisbon sky panel uses the same scale for its colour.

Simplifications: clear sky, no moon, no clouds, and the atmosphere's dimming of a low sun isn't modelled.

The 2 Lisbon views also show 2 panels (bottom left):

- **Lisbon, the year:** every day of the year across, sun time 00–24 down, painted sun (amber), twilight to −12° (blue) and dark. The top line gives the year's shares (sun 51%, twilight 9%, dark 40%). A line and dot mark now.
- **Lisbon sky:** the sun's height over Lisbon from 00:00 to 24:00 sun time, the horizon, the −12° line, and where the sun is now (filled by day, hollow otherwise). The sky colour follows the sun's height. Click or drag along it to jump to that time of day; the globe's sun and light follow (year modes switch to Pause).

To watch Lisbon's sun and dark over the year with the globe still: **Lisbon · sun up/down**, **Day**, and push **Speed** up. The sun climbs and drops along the 8 with the season while the light goes on and off each day.

- **Orbit · sun in middle:** the sun at the centre and Earth going round it on its true orbit: its true distance each day (147.1 million km on 3 Jan to 152.1 million km on 6 Jul) and its true shape, which is almost a circle. Earth's axis stays fixed in space, leaning 23.44°, so the north leans toward the sun at the June solstice and away at December's. Marks for the equinoxes, solstices, closest and farthest points. Earth and sun are drawn far bigger than real. In the trail modes, the amber trail is Earth's path.

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
- **Equator** (turquoise) and **tropics** at 23.4° N and S: the band never leaves the tropics.
- **Year path (thin amber, toggle "Year path"):** where the sun is overhead at the same clock time every day of the year. It's a figure-8 (the analemma): up and down from the tilt, sideways from the equation of time. Drawn at 12:00 UTC in the spin views and at Lisbon mean noon in the Lisbon views, so there it sits on Lisbon's meridian.
- **Where the 8 crosses (thin amber line, with Year path):** the parallel through the figure-8's crossing point, 8.9° N: on 12 April and 29 August the sun is overhead at the same spot at the same clock time. Found from the sun in the page, not typed in.
- **Lisbon and London** (blue dots, always shown).
- **Reference bands (toggle "Bands", or `?bands=1`):** the bands the model is built on: E0 (8.3° S – 8.3° N), N1 (8.3–23.4°), N2 (23.4–40.2°), N3 (40.2–50.7°), labelled with their share of the world's people (12.8%, 27.1%, 37.1%, 11.3%). The tropics are split by equal day-length change (about 58 min each on the June solstice). The south mirrors the north, so everything south of E0 is one hollow group (S1+, 7.2%), as is N4+ (4.5%). The globe's skin covers only 8.3° S – 50.7° N. A key under the legend (top left, in every view) lists each band's share and biggest cities by metro population (Natural Earth), one per line.
- **Population (toggle "Population", or `?pop=1`):** the same light bands in both halves, N1–N8 + cap and S1–S8 + cap, each labelled with its share of the world and its density (share of people ÷ share of Earth's surface, × world average), and shaded by density: N1 1.7×, N2 3.0×, N3 1.8×, N4+ 0.4×; S1 0.5×, S2+ 0.1×. Bands with 10% or more stand alone; neighbouring bands under 10% are merged and drawn hollow (the globe's skin is cut away there): N1 33.6%, N2 37.1%, N3 11.3%, N4+ 4.5%; S1 10.3%, S2+ 3.2%. Rough: Natural Earth country populations (about 2019, 7.68 billion) spread across bands by where each country's cities are.
- **1 h bands / 2 h bands (buttons, or `?swing=1` / `?swing=2`):** both halves split so each band adds 1 h (or 2 h) to the gap between the longest and shortest day, from the equator out, named N1, N2… and S1, S2…; above 65.7° the 24 h cap. A key (top left) lists every band from the north cap to the south cap with its share of the world's people, its latitudes and its 2 biggest cities of 100,000+ (Natural Earth); the globe labels carry the share too. Edges are worked out from the sun in the page. One set of bands shows at a time (these or the reference Bands). In the 1 h set, S2 and further south and N10 and further north are hollow: no fill and no skin, so the globe is solid only from 8.6° S to 52.0° N, and the hollow bands carry no labels on the globe (they stay in the key).
- **Tropics ribbon (faint amber):** the strip between the tropics, the only part of Earth where the sun is ever straight overhead.
- **Cities (toggle "Cities", or `?planes=1`), the sleep planes:** the 5 agreed reference planes for the sleep rule, northern half only (the rule is the same in both hemispheres). Each plane is a group of big cities: a line for one city (Austin, Milan), a band from nearest to farthest city for a group (Singapore · (Nairobi) · (Jakarta) 1–6°; Bangkok · Hong Kong · (Rio) 14–23°; Copenhagen · Stockholm · Oslo 56–60°). Southern cities are mirrored onto the north and written in brackets. Dots mark the cities and turn with the Earth. A panel, **People by latitude**, shows city population per degree from the equator (north and south folded; Natural Earth populated places, 2.37 billion people) with each plane's share of the people nearest it. Hidden in the Lisbon views, where the Lisbon panels take that space. **Reference lines** (dashed blue, labelled on the right, and on the chart): Lisbon 38.7° N and London 51.5° N.

### Controls

- **Tilt 23.4°:** off puts the axis upright. The band stays on the equator all year, the 8 collapses to a short sideways line (only the orbit's eccentricity left), and every place gets about 12 hours of day.
- **Timeline:** drag to any day of 2026. Marks show the equinoxes and solstices, the months, and Earth's closest (3 Jan) and farthest (6 Jul) points from the sun. Click a mark to jump to it.
- **Drag** the globe to turn the camera. **Reset view** (or double-click) puts the camera back.

### Your setup is remembered

The globe keeps your view, toggles, time mode, speed and camera angle in the browser, so reloading or opening an updated version comes back as you left it; URL parameters still override. The sleep page remembers the chosen city.

### Readouts

The date, the latitude where the sun is overhead (declination), Earth–sun distance, and Lisbon's daylight for that day (sunrise to sunset, refraction included): 9h28 in December to 14h50 in June.

### What it shows for NT

- No place on Earth keeps the same day length, sun height or temperature all year. The equator comes closest: about 12h07 of daylight every day. Geometry fixes it near 12h; the extra minutes come from refraction, which adds about 7 minutes everywhere.
- Peak sun and lowest sun (the sun crossing your meridian) are the only markers that happen every day everywhere. That's why NT anchors 12:00 and 00:00 on them.
- The hottest belt (the thermal equator) is not the overhead band: it bends with land and sea. Not drawn.

## sleep.html: sleep by city

Every night of 2026 for the 13 reference cities (the 5 planes' cities plus Lisbon and London). Pick a city; drag across the chart or the slider to pick a day. `?city=lis&day=319` opens a city and day (city ids: sin, nbo, jkt, bkk, hkg, rio, aus, lis, mil, lon, cph, sto, osl; day 0 = 1 Jan).

- **Year chart:** days across; NT down the side from 12:00 through 00:00 to 12:00, so the night sits in the middle. Painted sun up (amber), twilight to −12° (blue) and dark.
- **Should (green):** the proposed Z rule (SPEC.md, not agreed): asleep = 6.4 h + 0.56 × (night − 11.9 h), floor 6 h, ceiling 8 h or 9.9 h (buttons); in bed = 15 min + asleep ÷ 0.83; wake at sunrise, bed = sunrise − time in bed.
- **Observed (dashed blue):** typical bed and wake times from published data, converted from the local clock to NT for every day, so they wander with daylight saving and the equation of time. "Not found" where no sourced figure exists.
- **Readouts and table:** sunrise and sunset on the local clock and in NT, day and night length, should bed and wake (clock and NT), time in bed and asleep, observed times, for the chosen city and for all 13 on the chosen day.
- **NT** uses the agreed 100% stretch (sunrise 06:00, peak 12:00, sunset 18:00); the chart's side scale stays plain sun time so the seasons show. Wake is at sunrise (agreed), bed = sunrise − Z. Clock times use each city's time zone with daylight saving.
