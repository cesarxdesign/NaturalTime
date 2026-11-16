# Story tally

Raw material for a future folio page: turning points, decisions, what was rejected and why, numbers, and visuals available. Notes, not copy. Updated as the project moves.

## Turning points (2026-11-16)

1. **The question.** Noon on the clock isn't noon in the sky. In Lisbon the sun peaks anywhere from about 12:20 to 13:43 AT over a year.
2. **The anchor.** Sunrise and sunset don't exist every day everywhere (polar day and night). Peak sun and lowest sun do. So NT puts 12:00 at peak sun and 00:00 at lowest sun, at the exact GPS position.
3. **Two clocks, not one.** NT is for the body (sleep, meals, training); AT is for other people (meetings). Neither replaces the other.
4. **Minutes that change length.** NT stretches day and night minutes with the season, so the clock never reads the same against AT two days running.
5. **Society stays in charge of the work block.** The world won't move, so AT is the strongest anchor: the work block (XY, weekdays 08:00–18:00 AT) is a solid block, AT big inside it, NT big outside, a handover window, tap to swap.
6. **Icons that carry information.** AT: spinning globe. NT: filled sun by day, hollow sun in nautical twilight (sun down but still light), real moon phase in the dark.
7. **Place names: GPS is king.** AT shows the time-zone city (Lisbon, London); NT shows the locality (Caparica), in the place's own language. Names never feed the time. Bug caught: a Manchester test showed "Lisbon" for AT; fixed so AT always follows the place's time zone.
8. **Spec from day one.** Everything the watch takes into account is documented as it's built (SPEC.md).
9. **No arbitrary calls.** A 30% stretch and a 22:00–06:00 sleep arc went in as my own picks. Rejected: every value must be evidence-based and agreed. Both are now marked placeholders.
10. **The extra mile: sleep.** The obvious product stops at NT, AT, the day bars and the swap. Sleep is added on top: Z (how long, in real hours), Zs and Ze (when, on the sun's dial). Principle: time follows the planet, sleep follows the body; minutes never flex to fit sleep.
11. **Where is "peak sleep"?** Research changed the idea: deepest sleep comes early and follows bedtime, so it can't be the anchor. Under natural light only, the body's night (melatonin) centres on the middle of the solar night, which is lowest sun, NT 00:00.
12. **Building a model to think with.** A 3D globe to see where the sun is overhead and how much light one place gets: 4 views (axis still, axis moving, sun around Lisbon, sun up/down on Lisbon), playback up to a year in 2 s with light trails, and an imprint mode that paints the figure-8 (analemma) like a timelapse photo.
13. **Light as the eye sees it.** The globe's light was first an on/off guess, then sin(sun height), then the Earth–sun distance was added, then measured clear-sky lux (sunrise about 400 lux, end of civil twilight about 3, nautical about 0.03) on a log scale, because eyes respond to light that way.
14. **Evidence over intuition.** Colorado camping (40° N, close to Lisbon): 6.8 h of sleep in summer, 9.9 h in winter under natural light only. Huberman's example: 6 h summer, 7–8 h winter. Conflict recorded; Huberman favored.
15. **One model for the whole planet.** Baseline at the equator (12h07 of day all year, nothing to flex), then a relation fitted through real places: Lisbon (first user), Austin (Huberman), Stockholm, Tromsø.
16. **The baseline has data.** The Hadza, 3.7° S, under natural light: 12.1 h nights, 6.3 h of sleep, asleep 3.4 h after sunset, awake 1 h before sunrise, no seasons. Further from the equator sleep grows in winter (Tsimané +56 min, San +53 min), always ending near the day's coldest point.
17. **Sleep counted as time in bed.** Studies report time asleep; the watch needs time in bed. Z = time to fall asleep (about 15 min, 169 lab studies) + sleep period (time asleep ÷ efficiency, 83% in the traditional groups and 86% in the labs). Huberman sets no target, only a limit: up after 20–25 min awake. Agreed: 15 min to fall asleep.

18. **The data and Huberman meet.** Natural-light groups gain about 0.56 h of sleep per extra hour of night. Huberman's 6 h summer, 8 h winter, at Austin's latitude, works out at 0.51. One rule proposed for the planet: 6.4 h at the equator, plus 0.56 × the extra night, never under 6 h.

19. **One rule, both hemispheres; 5 planes of cities he knows.** The rule is mirrored, so only the northern half of the globe is needed and southern cities count at their mirrored latitude. First picks bunched up (Austin and Lisbon 8° apart, nothing in 0–30°, where most people live); exact-latitude picks (Quito, Manila, St Petersburg) were evenly spaced but unfamiliar. Settled on groups of big cities he knows, a few degrees off allowed: Singapore · (Nairobi) · (Jakarta), Bangkok · Hong Kong · (Rio), Austin, Milan, Copenhagen · Stockholm · Oslo. Lisbon and London stay as reference lines. Familiar beats exact: a known place makes the data easier to judge, and big metropolises are where data lives.

20. **Wake when the light comes.** Centring sleep on the night, as the Hadza do, had Lisbon up 1h12 before a November sunrise. Rule set instead: wake at sunrise, and longer nights only move bedtime earlier.

21. **Two equal halves, and a wrong turn.** The Earth turns at a steady rate, so the morning is exactly as long as the afternoon. That looked like it forced sunrise 06:00, peak 12:00, sunset 18:00 (100% stretch), and it went live. Then the question that undid it: is the day 12 + 12 everywhere? Only at the equator. Equal halves only need sunrise and sunset the same distance from 12:00; pinning them to 06:00 and 18:00 is a separate choice.

22. **The light ramp.** Waking at sunrise is fine where the light comes on fast. Where it creeps in (winter, the north), sleeping a little past sunrise beats sitting in dim light, and it lets winter's extra sleep come partly from the morning, not all from the evening.

**The stretch, in his words:** "anyone else would have put 30% and shipped it." The placeholder was 30%. Instead: equal halves, a wrong turn to 100%, 4 cities on their longest and shortest days, equal-light bands, the figure-8, light strength, the morning ramp, the heat lag, and a search of the published models. Still open, on purpose.

23. **Testing the stretch on real places.** Longest and shortest day, sun time and clock, in Singapore, Nairobi, Lisbon and Oslo:
   - Singapore and Nairobi: 12h03–12h12 of day all year, so 06:00–18:00 is almost true. Put Singapore's clock on its natural zone and sunrise is 06:01, peak 12:03–12:07, sunset 18:04–18:12.
   - Lisbon: 14h53 in June (sun time 04:34 → 19:26), 9h27 in December (07:16 → 16:44).
   - Oslo: 18h50 in June (02:35 → 21:25, twilight all night), 5h54 in December (09:03 → 14:57).
   - The deciding image: at 100%, Oslo's June sunset reads 18:00 when it's really 21:25. "We can't call 22h 18h... but they WILL have light." 100% reopened.
   - Nobody gets 06:00 / 12:00 / 18:00 on the clock all year; even the equator has 12h07 of day (refraction), and the clock drifts ±16 min from the sun. Closest: Quito (14 Oct) and Mbandaka (25 Feb), each for about a day.
24. **Bands of equal light.** One band = equator to the Tropic of Cancer (23.44°, the tilt); the polar cap is exactly one more. Equal-width bands: 3.84 to the pole. But light changes faster further north, so bands of equal light change (each adds the tropics' 1h28 to the longest day) shrink: 23.4°, 16.8°, 10.5°, 6.5°, 4.1°, 2.5°, 1.4°, 0.5°: 8 bands before the Arctic Circle. Total yearly daylight is about the same everywhere; what latitude changes is how it's spread across the seasons.
25. **Reading the figure-8.** Its height is the tilt (seasons, ±23.44°, symmetric); its width is the clock drifting from the sun. The bottom loop is fat because Earth is closest and fastest in January; the crossing sits at 8.9° N, not on the equator, as a fingerprint of the oval orbit. NT erases the width: 12:00 is always peak sun, so the 8 collapses to a straight line on your own meridian.
26. **Strength, not just length.** Distance gives January about 7% stronger sun; sun height matters far more (Lisbon noon light about twice as strong in June). At sunrise itself the light is about the same every day; 20 minutes later the season barely matters, but latitude does (the sun creeps sideways in Oslo). The real seasonal difference is later in the morning.
27. **Ease in, ease out.** No animal runs at full speed at sunrise; the productive day trails the light (7–19 or 8–20 instead of 6–18). Nature has the same shift: peak heat trails peak sun by about 2–3 h, and the body's temperature peaks in the late afternoon. Not a fixed 2 h: it moves with season, latitude and coast.
28. **Looking for the heat formula.** The best published rule found: Cesaraccio et al. 2001 (yes, nearly his name), peak heat 4 h before sunset, coldest at sunrise, built on 5 Californian weather stations. It moves with day length (equator 2h03 after peak sun; Lisbon 3h26 in June, 0h44 in December) but breaks on short days (Oslo in December would peak before noon). Other models (Parton & Logan) use a fixed lag tuned site by site. Nobody found adjusts the timing for latitude: a gap the project may have to fill with its own fit to measured data.

29. **The body's day, not the light's (hypothesis).** Earth warms up late, and so do we: light runs 6–18, the lived day closer to 8–20, everywhere. Maybe NT's anchor is peak heat, not peak sun; maybe the halves aren't equal, because we linger in the evening; and the lingering flexes with the season, but less than the light. The aim: the same numbers mean the same thing all year (eat at 12, bed at 21, up at 6–7, as shapes, not values). First evidence: the Hadza's waking day is centred 1h12 after peak sun, with a 6h57 morning and a 9h21 evening.

## Rejected or replaced

- Sunrise as the anchor: doesn't exist every day far north.
- Day and night as two fixed halves: ignores the season.
- Split (two-phase) sleep: left out.
- Deepest sleep as the anchor: follows bedtime, not the clock.
- 30% stretch, 22:00–06:00 sleep arc: picked without evidence.
- 100% stretch (sunrise always 06:00, sunset 18:00): agreed in a hurry, then reopened. It forces a 12 + 12 split that only the equator has; Oslo's 21:25 June sunset would read 18:00.
- An 8 h sleep ceiling (Huberman's winter top): not natural; deep-winter sleep under natural light runs longer. The one place the user overruled Huberman.
- Sleep centred on the night (1.1 h after lowest sun): woke people in the dark in winter. Replaced by wake at sunrise.
- Stretch 30%: a placeholder with no reason. Stretch 0% (pure sun time): honest minutes, but sunrise wanders 04:34–07:16 NT in Lisbon.
- On/off light on the globe: replaced by measured lux on an eye scale.
- Reference planes Equator, Austin, Lisbon, Stockholm, Tromsø: bunched in pairs, a 30° hole where most people live; Tromsø too small.
- Planes Quito, Manila, Austin, Milan, St Petersburg: exact 15° spacing, but cities he doesn't know.

## Numbers bank

- Lisbon peak sun: about 12:20–13:43 AT over a year; 37 min from its place in the time zone, −16 to +14 min from the equation of time, +60 min daylight saving.
- Lisbon day length: 9h27 (December) to 14h53 (June). Equator: 12h07 every day.
- Lisbon's year: sun 51%, twilight 9%, dark 40%.
- Earth–sun distance: 147.1 million km (3 Jan) to 152.1 million km (6 Jul); about 7% more light in January.
- Sleep without electric light: Hadza, San, Tsimané 5.7–7.1 h (average 6.4 h), start about 3.3 h after sunset, wake before sunrise. Colorado: 6.8 h summer, 9.9 h winter.
- People by latitude (cities, N and S folded), nearest each plane: Singapore group 13%, Bangkok group 23%, Austin 36%, Milan 22%, Copenhagen group 6%.
- Time to fall asleep: 15.4 min (adults, 169 lab studies, Boulos 2019); 14.3 min at 18–34, 19.5 min at 65–79. Sleep efficiency 85.7%. Huberman: get up after 20–25 min awake.

## Visuals available

- The watch face (index.html): NT/AT, day bars, seconds dots, icons.
- Globe (Visualizations/globe.html): the 4 views, the year-in-2-s trail, the imprint figure-8 over Lisbon, the "Lisbon, the year" chart of sun, twilight and dark; the 5 sleep planes with the people-by-latitude chart.
- Sleep by city (Visualizations/sleep.html): every night of the year for 13 cities, light, the proposed sleep window and observed bed and wake times, on the clock and in NT.

## Open

Z swing, Z baseline, temperature, where Z sits, the seasonal stretch, the latitude relation. See SPEC.md, Under discussion.
