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
17. **Sleep counted as time in bed.** Studies report time asleep; the watch needs time in bed. Z = time to fall asleep (about 15 min, 169 lab studies) + sleep period (time asleep ÷ efficiency, 83% in the traditional groups and 86% in the labs). Huberman sets no target, only a limit: up after 20–25 min awake.

## Rejected or replaced

- Sunrise as the anchor: doesn't exist every day far north.
- Day and night as two fixed halves: ignores the season.
- Split (two-phase) sleep: left out.
- Deepest sleep as the anchor: follows bedtime, not the clock.
- 30% stretch, 22:00–06:00 sleep arc: picked without evidence; placeholders until agreed.
- On/off light on the globe: replaced by measured lux on an eye scale.

## Numbers bank

- Lisbon peak sun: about 12:20–13:43 AT over a year; 37 min from its place in the time zone, −16 to +14 min from the equation of time, +60 min daylight saving.
- Lisbon day length: 9h27 (December) to 14h53 (June). Equator: 12h07 every day.
- Lisbon's year: sun 51%, twilight 9%, dark 40%.
- Earth–sun distance: 147.1 million km (3 Jan) to 152.1 million km (6 Jul); about 7% more light in January.
- Sleep without electric light: Hadza, San, Tsimané 5.7–7.1 h (average 6.4 h), start about 3.3 h after sunset, wake before sunrise. Colorado: 6.8 h summer, 9.9 h winter.
- Time to fall asleep: 15.4 min (adults, 169 lab studies, Boulos 2019); 14.3 min at 18–34, 19.5 min at 65–79. Sleep efficiency 85.7%. Huberman: get up after 20–25 min awake.

## Visuals available

- The watch face (index.html): NT/AT, day bars, seconds dots, icons.
- Globe (Visualizations/globe.html): the 4 views, the year-in-2-s trail, the imprint figure-8 over Lisbon, the "Lisbon, the year" chart of sun, twilight and dark.

## Open

Z swing, Z baseline, temperature, where Z sits, the seasonal stretch, the latitude relation. See SPEC.md, Under discussion.
