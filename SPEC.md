# Natural Time — spec

What the watch takes into account, how it works it out, and why. Started 2026-11-16. Every rule here matches the live code in `index.html`, except the section **Under discussion**, which records ideas and evidence that aren't agreed or built yet.

Models used to work the ideas out: [Visualizations](Visualizations/README.md).

---

## The problem: the clock's noon is not the sun's noon

Agreed time (AT) puts noon at 12:00 every day. The sun doesn't. In Lisbon the sun's peak lands anywhere from about 12:20 to 13:43 on AT over a year, because AT ignores 3 things:

| Cause | Lisbon effect | Changes |
|---|---|---|
| Place in the time zone | +37 min (Lisbon is 9.14° west of the zone's centre; 4 min per degree) | never |
| Earth's tilt and orbit (equation of time) | from −16 min (early Nov) to +14 min (mid-Feb) | every day |
| Daylight saving | +60 min | in 2 jumps a year |

On top of that, AT ignores the season: the same 08:00 is dark in December and full daylight in June.

In Lisbon, AT is never in step with the sun, not even for one day: the 37-minute offset is bigger than the 16-minute maximum of the equation of time.

## Two clocks: NT for the body, AT for meetings

- **NT (natural time)** follows the sun at the exact GPS position. Sleep, meals and workouts run on NT.
- **AT (agreed time)** is the device's time zone. Meetings and anything shared with other people run on AT.

Both show the same moment. NT is like a private time zone that moves with the sun, the way a call with New York is 08:00 for one person and 13:00 for another.

## What NT takes into account

| Input | Source | Why |
|---|---|---|
| Exact time | the device clock (synced by the network) | the base of everything |
| Longitude | GPS | sets where the sun peaks: 4 min per degree, about 3 s per km east–west in Lisbon |
| Latitude | GPS | sets the length of the day, which sets the seasonal stretch |
| Date | the device clock | equation of time and day length change every day |

Nothing else counts. Mountains, buildings, clouds and weather don't change NT: it's where Earth is relative to the sun, not how much light reaches you.

GPS is the only source of position. The place name shown on the watch is a label and never feeds the time.

## How NT is worked out

### 1. Sun time: peak sun is always 12:00

Sun time (apparent solar time) puts the sun's lowest point at 00:00 and its highest point at 12:00, every day, everywhere except exactly at the poles.

```
sun time = UTC + 4 min × longitude + equation of time
```

The equation of time and the sun's declination come from the NOAA solar calculator formulas, accurate to a few seconds for peak sun and about a minute for sunrise and sunset.

Peak sun and lowest sun are the only markers that exist every day everywhere. Sunrise and sunset don't: far north there are weeks without one. That's why they anchor NT and sunrise doesn't.

### 2. The seasonal stretch: minutes change length

Inside the day, NT stretches or shrinks its minutes with the season, while keeping 00:00 at lowest sun and 12:00 at peak sun.

1. Work out today's daylight `D` in hours: sunrise to sunset, with the sun's centre 0.833° below the horizon (standard refraction).
2. Blend it toward 12 hours by the stretch `k` (live code: 30%, a placeholder not yet agreed, see Under discussion): `D' = 12 + k × (D − 12)`, kept between 0.5 h and 23.5 h.
3. Map the blended day onto NT 06:00–18:00 and the rest onto the night, in 4 straight pieces:

| Sun time | NT |
|---|---|
| lowest sun (00:00) | 00:00 |
| peak sun − D'/2 | 06:00 |
| peak sun (12:00) | 12:00 |
| peak sun + D'/2 | 18:00 |

- At `k = 0%`, NT is pure sun time: every minute is about 60 s and sunrise moves around the dial.
- At `k = 100%`, sunrise is always 06:00 and sunset always 18:00 (the old "temporal hours"). In Lisbon that gives about 9h20 of real sleep in winter and 6h10 in summer, which is more than people living by the sun actually do.
- At `k = 30%`, a day minute in Lisbon runs from about 56 s in December to about 64 s in June, and night minutes the other way.

Length of 1 NT minute = `5 × D'` seconds by day and `5 × (24 − D')` seconds by night.

NT seconds stretch with the minutes. In Lisbon right now an NT second is 0.95 real seconds by day and 1.05 at night.

### 3. Sleep: 22:00–06:00 NT (placeholder, not agreed)

Live code draws sleep as a fixed arc on the NT dial, 22:00 to 06:00, centred on 02:00 NT. It's a placeholder chosen without agreement; the sleep rule is being worked out under **Under discussion**. The reasoning behind the placeholder:

- Centred about 2 hours after the sun's lowest point because that's where people living without electricity centre their sleep: they fall asleep about 3 hours after sunset and wake near the coldest point of the night, just before dawn. Air temperature trails the sun by about 2 hours.
- With the 30% stretch, the arc gives Lisbon about **8h30 of real sleep in December and 7h30 in June**. That's close to the roughly 1 extra hour in winter seen in those groups.
- Waking exactly at sunrise and sleeping at sunset is not the goal: dawn is a gentle wake-up and dusk still has activity.

### 4. Never the same time twice

NT against AT changes every day: by a few seconds a week near the turning points (mid-Feb, mid-May, late July, early Nov) and up to about 3.5 minutes a week around Christmas, plus the stretch, which changes fastest at the equinoxes.

Two people with NT in the same town read the same minute: across Caparica (about 5 km) NT differs by at most about 14 s. Across London (about 50 km) it differs by about 3 minutes.

## The watch face

### Two clocks, one big

- **Work block, weekdays 08:00–18:00 AT:** AT is the big clock and NT the small one, top right.
- **The rest of the time:** NT is big and AT small.
- **Handover:** the 5 minutes before 08:00 and before 18:00 show both clocks at the same size.
- **Tap the big clock** to swap them by hand. The swap lasts until the next scheduled change.

In Lisbon in 2026, at the 30% stretch, the work block starts between 06:22 and 07:31 NT and ends between 16:01 and 17:56 NT, depending on the season. While daylight saving is on (late March to late October), 08:00 AT arrives only 23–45 minutes after a 06:00 NT wake-up. NT doesn't hide that: it shows the cost so the choice is yours.

### Time, seconds and labels

- Hours and minutes in IBM Plex Mono, colon centred on the face.
- Seconds are a line of 60 dots under the big clock, filling as the minute passes. NT dots fill at NT's speed, AT dots at exactly 1 per second.
- **AT label:** the city the device's time zone is named after (Europe/Lisbon → Lisbon, Europe/London → London).
- **NT label:** the locality from GPS (Caparica, Manchester, Dover), in the place's own language so accents stay (Santo António, Setúbal). Merged Portuguese parishes keep their first name.

### Icons

| Clock | Icon | Rule |
|---|---|---|
| AT | spinning globe | what the planet agrees on |
| NT | filled sun | sun above the horizon |
| NT | hollow sun | sun below the horizon but above −12° (nautical twilight: there's still light) |
| NT | moon, real phase | sun below −12° |

The moon phase is the mean phase, accurate to within about a day. It's mirrored in the southern hemisphere.

### Day bars

2 lines at the bottom of the face. Across is NT, 00:00 to 24:00.

- **Top line, NT:** an amber tick in the middle for peak sun, which never moves, and 2 amber dots for nautical dawn and dusk.
- **Bottom line, AT:** a blue band for the 08:00–18:00 work block and a blue tick for 12:00 AT. These drift against the peak through the year.
- **A thin white line through both** is now.

## Data and privacy

- All sun and moon maths runs on the device. No server.
- The place name is the only network call: coordinates rounded to 2 decimals (about 1 km) go to BigDataCloud's free reverse geocoder. The name is cached until you move about 1 km.
- Position, place name and stretch are remembered in the browser.
- Without GPS permission, the place is Lisbon.

## Under discussion (not agreed, not built)

### Sleep: Z, Zs and Ze

Agreed so far:

- **Time follows the planet; sleep follows the body.** NT minutes flex only to fit the hours to the sun. They never flex to fit sleep. Sleep is markers placed on the NT dial.
- **Z** is how long to sleep, always stated in real hours (AT hours), so the number is never odd-looking. **Zs** (go to sleep) and **Ze** (wake up) are where it sits on the NT dial.
- **Natural conditions:** the rule assumes no artificial light at night. The watch gives the natural guidance; blackout is up to the user.
- **One block of sleep.** No split sleep.
- **Z changes with the season:** longer in winter and when cold, shorter in summer and when hot. It changes a little every day, never in jumps. How much it swings must come from evidence, not a picked number.

Evidence gathered so far:

| Conditions | Winter vs summer sleep |
|---|---|
| Without electric light (Tsimané, Bolivia; San, Namibia) | about 1 hour more in winter |
| Camping without electric light, Colorado (40° N, close to Lisbon's 38.7°) | winter, around the solstice (5 people): 9.9 h vs 7.6 h at home. Summer, 14h40 of daylight (8 people): 6.8 h vs 6.7 h at home |
| With electric light (Germany; 73 million nights of wearable data; Tromsø) | 0–25 minutes more in winter |

- Read as a ratio: under natural light, sleep changes by about 40–60% of the change in night length.
- People living by the sun wake near the coldest point of the night, about 1 hour before sunrise.
- Under natural light only (Colorado, summer), melatonin rises near sunset, peaks in **the middle of the solar night**, and falls just after sunrise, before waking. The body's night lines up with the sun's.
- Deepest sleep (slow-wave) comes early, in the first sleep cycles, and follows bedtime rather than the clock. Mid-sleep tracks melatonin timing closely. Core body temperature bottoms out about 2 hours before habitual waking.
- **Huberman** (Huberman Lab sleep toolkit): needs change, for example "6 hours a night in summer and 7-8 in winter"; wake at the same time every day, go to bed when first sleepy; sunlight within 30–60 minutes of waking; avoid bright overhead light 10 pm–4 am.
- **Conflict:** Huberman's example swing (6 h → 7–8 h) is smaller than Colorado's measured one (6.8 h → 9.9 h). His is an example of changing needs, Colorado's a small measured study. Standing rule: favor Huberman where they disagree.

Lisbon's nights match Colorado's closely: 9h07 at the June solstice (Colorado summer camping had 9h20 of dark) and 14h32 at the December solstice.

Open questions:

1. **Z's swing:** Huberman's example (summer 6 h, winter 7–8 h) or Colorado's measurement (summer 6.8 h, winter 9.9 h, about 56% of the night-length change); and whether a floor and a ceiling apply.
2. **Z's baseline:** the length at the equinox, set per user (8 h for the first user).
3. **Temperature:** heat shortens sleep and cold lengthens it; the size of the effect needs data.
4. **Where Z sits:** the evidence puts the body's night (melatonin midpoint) at the middle of the solar night, i.e. lowest sun, NT 00:00. Options: around a "peak sleep" point, stretched both ways like NT stretches from peak sun, or ending at the coldest point of the night with Z counted backwards. This also settles the 2-hour offset between lowest sun and the middle of sleep that the placeholder uses.

### The seasonal stretch

How far NT pulls sunrise and sunset toward 06:00 and 18:00. Live code runs 30%, a placeholder chosen without agreement. Options on the table: 0% (pure sun time), 100% (sunrise always 06:00, sunset always 18:00, with a fallback where the sun doesn't set or rise), or a value with a reason behind it.

## Open items

- **Temperature offset:** agreed that the 2-hour gap between the sun and the body should follow the place's measured temperature cycle (from forecasts, averaged over 1–2 weeks so weather doesn't jerk it). Not built: sleep is fixed at 22:00–06:00 NT.
- **Stretch 30%:** a placeholder chosen without agreement (see Under discussion). Far north it's extreme: Kiruna at midsummer gets about 5h36.
- **Sleep arc 22:00–06:00 NT:** a placeholder, to be replaced by the Z rule.
- **Work block weekdays only:** an assumption. Weekends are NT all day. The block itself (08:00–18:00) will be set per user.
- **Handover and hollow-sun craft:** to be designed.
- **Apple Watch:** Apple doesn't allow third-party watch faces, so the big clock has to be a large complication (X-Large or Modular Ultra face) with the small one as a second complication. AT can use the system clock. NT's stretched minutes have to be worked out ahead of time and handed to the complication as a timeline.

## Testing

Add to the URL:

- `t=2026-07-25T15:20:00Z` to start at any moment
- `lat=53.48&lon=-2.24` for any place
- `tz=Europe/London` for that place's AT (without it, AT is the device's time zone)
- `speed=60` to run time 60× faster
