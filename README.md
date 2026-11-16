# Natural Time

A clock locked to the sun at your location.

- **NT (natural time):** peak sun is always 12:00 and the sun's lowest point is always 00:00. Minutes stretch or shrink with the season, so NT never reads the same against AT two days running.
- **AT (agreed time):** the clock everyone shares, for meetings.

During the work block (weekdays 08:00–18:00 AT) AT is the big clock and NT the small one. The rest of the time NT is big. The NT icon is the sun while there's light (hollow during nautical twilight) and the real moon phase in the dark; AT is a spinning globe.

Sun maths: NOAA solar calculator formulas, worked out on the device. Only the place name needs the network: coordinates rounded to about 1 km go to BigDataCloud's reverse geocoder.

Testing: `?t=2026-07-25T15:20:00Z&lat=53.48&lon=-2.24&tz=Europe/London&speed=60` (tz sets AT; without it AT is the device time zone)

Live: https://cesarxdesign.github.io/NaturalTime/

Full spec (what it takes into account, how and why, and what's still under discussion): [SPEC.md](SPEC.md)

Story tally for a future folio page: [STORY.md](STORY.md)

Models used to work the ideas out: [Visualizations](Visualizations/README.md), live at https://cesarxdesign.github.io/NaturalTime/Visualizations/globe.html
