# Natural Time — spec

What the watch takes into account, how it works it out, and why. Started 2026-11-16. Every rule here matches the live code in `index.html`, except the section **Under discussion**, which records ideas and evidence that aren't agreed or built yet.

Models used to work the ideas out: [Visualizations](Visualizations/README.md).

**Approach.** Engine first, then UX, then UI. The face in `index.html` is a working view of the engine, not the design. The obvious product stops at NT, AT, the day bars and the work-block swap. This project goes further: an evidence-based sleep layer that places sleep on the sun's clock for any latitude, even if few people will live by it. Every value is based on something real and agreed before it ships; the reasoning, evidence and rejected options are recorded here as they happen.

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

### Latitude model: a baseline, then the change with latitude

Z has to be a calculation based on something real. Plan: find the planet's baseline (A), then how sleep changes moving away from it, fitted through real reference places: Lisbon (B, the first user), Austin (Huberman's reference), then Sweden (C) and a place with almost no winter sun (D). Where the sun barely rises, people will have to wake before sunrise; the model must allow for that.

**Baseline: the equator.** Day length is 12h07 every day of the year (refraction included), so neither the light nor Z needs to flex. Nearest population with natural-light sleep data: the Hadza, Tanzania, 3.5° S.

| Place | Latitude | Shortest day | Longest day | Day-length flex | Full dark (sun below −12°) at midsummer |
|---|---|---|---|---|---|
| Equator (A) | 0° | 12h07 | 12h07 | 0 | 10h15 |
| Hadza, Tanzania | 3.5° S | 11h55 | 12h19 | 0h24 | 10h02 |
| Austin (Huberman) | 30.3° N | 10h11 | 14h06 | 3h55 | 7h52 |
| Lisbon (B) | 38.7° N | 9h27 | 14h53 | 5h26 | 6h43 |
| Boulder, Colorado (studies) | 40.0° N | 9h19 | 15h01 | 5h41 | 6h30 |
| Stockholm (C) | 59.3° N | 6h05 | 18h37 | 12h32 | none |
| Tromsø (D) | 69.7° N | none (polar night) | 24 h (midnight sun) | 24 h | none |

**Agreed (2026-11-16): one rule for both hemispheres.** Whatever is set north of the equator holds south of it too, mirrored: same latitude, same rule, seasons flipped. So southern data (Hadza, Tsimané, San) counts for the matching northern latitude.

**Agreed (2026-11-16): the 5 planes are groups of big cities the user knows.** A familiar city beats an exact latitude match; a few degrees off is fine, because a known place makes the data easier to judge. The big metropolises are also where sleep data is most likely to be found. A plane with one city is a line; a plane with several is a band from its nearest to its farthest city (distance from the equator). Southern cities count at their mirrored latitude, written in brackets, so only the northern half of the globe is needed.

| Plane | Cities | Band | Natural-light sleep data near it |
|---|---|---|---|
| 1 | Singapore 1.3° N · (Nairobi 1.3° S) · (Jakarta 6.2° S) | 1–6° | Hadza 3.7° S (Nairobi is the nearest big city) |
| 2 | Bangkok 13.8° N · Hong Kong 22.3° N · (Rio de Janeiro 22.9° S) | 14–23° | Tsimané 14.9° S, San 19.8° S |
| 3 | Austin 30.3° N (Huberman) | line | none yet |
| 4 | Milan 45.5° N | line | Colorado 40° N, between Austin and Milan |
| 5 | Copenhagen 55.7° N · Stockholm 59.3° N · Oslo 59.9° N | 56–60° | none yet |

**Reference lines, not planes:** Lisbon 38.7° N (where the user lives) and London 51.5° N (where he lived), to read the planes against.

Rejected the same day: Equator, Austin, Lisbon, Stockholm, Tromsø (Austin and Lisbon only 8.4° apart, Stockholm and Tromsø 10.3°, nothing in 0–30°, Tromsø too small); then Quito, Manila, Austin, Milan, St Petersburg (exact latitudes, but less familiar cities).

Population check: city population by latitude, north and south folded together (Natural Earth populated places, 7,342 places, 2.37 billion people). Each plane takes the people up to the midpoint with its neighbours, a band counting from its middle (a drawing choice, not agreed): plane 1 13%, plane 2 23%, Austin 36%, Milan 22%, plane 5 6%. Cities only: rural people aren't counted, which under-weights the tropics.

Natural-light sleep by latitude (Yetish et al. 2015, Table S2; Wright et al. 2013; Stothard et al. 2017). "Night" is sunset to sunrise. "Sleep" is time actually asleep (actigraphy), not time in bed: the 3 traditional groups were asleep about 83% of the time between falling asleep and waking.

| Group | Latitude | Season | Night | Sleep |
|---|---|---|---|---|
| Hadza | 3.7° S | one week, May (no seasons at the equator) | 12.1 h | 6.3 h; fell asleep 3.4 h after sunset, woke 1 h before sunrise |
| Tsimané | 14.9° S | winter / summer | 12.4 h / 11.1 h | 6.6 h / 5.7 h (56 min more in winter) |
| San | 19.8° S | winter / summer | 12.9 h / 11.0 h | 7.1 h / 6.2 h (53 min more in winter); in summer woke 1 h after sunrise, with the day's coldest point |
| Colorado campers | 40° N | summer / winter | about 9.3 h / about 14.7 h | 6.8 h / 9.9 h |

- In all 3 traditional groups sleep began while the air was cooling and ended near the day's coldest point.
- Ratio of sleep change to night change: Tsimané about 0.7, San about 0.45, Colorado about 0.56.
- Doesn't line up on one straight line from the equator: Colorado's summer sleep (6.8 h, 9.3 h night) is about the Hadza's (6.3 h, 12.1 h night), and Colorado's winter sleep is far longer. Possible reasons: modern sleepers catching up, different sleep scoring, or sleep shrinking less in short nights than it grows in long ones. Not settled.
- **Agreed: Z is time in bed.** Zs is going to bed. Then a short delay before falling asleep (sleep latency). Then the sleep period: falling asleep to final waking, including brief wakings during the night. Ze is waking, and getting up follows almost at once. So **Z = latency + sleep period**, and the studies' "sleep" figures have to be converted up: sleep period = time asleep ÷ sleep efficiency (about 83% in the traditional groups, so Hadza 6.3 h asleep ≈ 7.6 h sleep period). **Agreed: latency = 15 min** (2026-11-16, from the sources below):
  - **Boulos et al. 2019** (Lancet Respiratory Medicine, 169 sleep-lab studies of healthy adults, Table 3): 15.4 min overall (95% CI 14.2–16.7). By age: 18–34 14.3, 35–49 14.4, 50–64 15.7, 65–79 19.5 min; about +1.1 min per decade. Men 14.7, women 13.5. Same paper, sleep efficiency 85.7% overall (18–34 89.0%, 35–49 85.4%), close to the 83% used above.
  - **Huberman:** no target figure. His rule: go to bed only when truly sleepy, and if still awake after about 20–25 min, get up and do something calm elsewhere. No conflict: the 15 min norm sits inside his 20–25 min limit.
  - Caveat: lab latency is counted from lights-out in a sleep lab, not under natural light. No latency figure found yet for the natural-light groups (Hadza, San, Tsimané).
  - With 15 min, Hadza Z ≈ 7.6 h + 0.25 h ≈ 7.9 h in bed.

Real natural-light sleep data exists near A (Hadza, San, Tsimané) and at B's latitude (Colorado). Not yet for Austin, C or D under natural light; Tromsø data is under electric light.

### Proposed Z model (2026-11-16, not agreed)

One rule for the whole planet, driven by the night length N (sunset to sunrise, hours) at the GPS position for that day:

```
asleep  S = 6.4 h + 0.56 × (N − 11.9 h), kept between a floor and a ceiling
Z (bed) = 15 min + S ÷ 0.83
```

- **Baseline (A):** the 3 traditional groups average 6.4 h asleep at nights of about 11.9 h (Hadza 6.3 at 12.1; Tsimané and San, averaged over their seasons, 6.2 and 6.7). Z at the equator: 7.9 h in bed, every day.
- **Swing:** 0.56 h of sleep per hour of night. Tsimané 0.7, San 0.45, Colorado 0.56: all natural-light, within the same people. Huberman's example at his latitude (Austin, nights 9.9–13.8 h): 6 h → 8 h is 0.51. The natural data and Huberman roughly agree on the slope.
- **Floor: 6 h asleep (7.5 h in bed).** Huberman's summer figure. Shortest-night measurements: Tsimané 5.7, San 6.2, Colorado 6.8. Reached at nights under 11.2 h.
- **Ceiling:** 8 h asleep **rejected** (2026-11-16): not natural; in deep winter, people living by the sun sleep longer than 8 h, not just lie in bed. Huberman's 7–8 h winter figure overruled here (flagged). Proposed instead: 9.9 h asleep (12.2 h in bed), the longest sleep measured under natural light (Colorado camping, winter). Not agreed.
- **Temperature:** no separate length term, to avoid double-counting the season. Heat only as a later adjustment: nights above 30 °C cut sleep by just over 14 min (Minor et al. 2022, 47,000 people, 68 countries).
- **Where Z sits: agreed, wake at sunrise** (2026-11-16): humans wake when the light comes. Ze = sunrise; Zs = sunrise − Z, so longer nights bring bedtime forward, never the wake. Replaces my own pick of centring sleep 1.1 h after lowest sun (from the Hadza), which put Lisbon's November wake 1h12 before sunrise. Open: places where sunrise comes very late or not at all (wake has to come before it there); and the far north in summer, where wake at sunrise plus the 6 h floor puts bedtime before sunset (Oslo 22 Jun: bed 20:25, sunset 22:44, wake 03:54).
- **Society adjustment (open, 2026-11-16):** no reason to wake before the sun unless something in the day needs it. When sunrise comes too late for the day's first commitment (London at peak winter: light around 08:00, train at 07:30), wake moves earlier, only as far as needed: wake = the earlier of sunrise and the latest wake that still makes the first commitment. Days without a commitment (weekends) wake at sunrise. To agree: what sets the first commitment (the work block start, per user) and how long the user needs between waking and leaving (per user, not a picked number).

| Place | Summer: asleep / in bed | Winter: asleep / in bed (ceiling 8 / 9.9) |
|---|---|---|
| Equator | 6.4 / 7.9 | 6.4 / 7.9 |
| Austin | 6.0 / 7.5 | 7.5 / 9.3 |
| Lisbon | 6.0 / 7.5 | 7.9 / 9.7 |
| Stockholm | 6.0 / 7.5 | 8.0 / 9.9 · 9.8 / 12.0 |
| Tromsø | 6.0 / 7.5 | 8.0 / 9.9 · 9.9 / 12.2 |

Lisbon check with the first user (2026-11-16), equator baseline, AT:
- 16 Nov: sunrise 07:20, peak sun 12:21, sunset 17:23; bed 20:47 ("almost 21 seems ok as guidance"), wake 06:08, 1h12 before sunrise.
- 22 Jun: sunrise 06:12, peak sun 13:38, sunset 21:05; bed 23:00 ("a wee bit late", but 21:22 NT reads right), wake 06:29 ("in line with regular standards"), 17 min after sunrise.

With wake at sunrise (AT): 16 Nov bed 21:59, wake 07:20; 22 Jun bed 22:44, wake 06:12; 21 Dec bed 22:06, wake 07:51.

Conflict: Colorado measured 9.9 h asleep in winter at 40° N; this rule gives about 8 h there. Huberman favored; Colorado's week-long campers may have been catching up on sleep.

### Observed sleep today, with electric light (for comparison, not a target)

Sleep Cycle app, 941,329 users aged 18–55, June 2014 to March 2015, time in bed, national averages (Daily Mail 2015, read from a reprint): Portugal 00:41 → 08:22, UK 00:28 → 07:33, Italy 00:35 → 07:52, USA 23:54 → 07:20, Denmark 23:47 → 07:19, Sweden 23:50 → 07:21, Norway 00:16 → 07:43, Singapore 23:52 → 07:38, Indonesia 00:10 → 06:55, Thailand 00:22 → 07:24, Hong Kong 00:55 → 07:57, Brazil 00:32 → 07:31. Kenya: not found. No city-level or seasonal figures for these places. Huberman: no fixed clock times; wake at the same time daily, sunlight within 30–60 min of waking, sleep when first sleepy, his own bedtime about 22:00–23:00 ([Toolkit for Sleep](https://www.hubermanlab.com/newsletter/toolkit-for-sleep)).

Lisbon in NT: Portugal's 00:41 → 08:22 is 23:03 → 06:44 NT on 22 June and 00:20 → 08:01 NT on 16 November; centred about 3–4 h after lowest sun, against the Hadza's 1.1 h.

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
