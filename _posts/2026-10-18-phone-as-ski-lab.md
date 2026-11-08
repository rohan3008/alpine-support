---
title: "The phone in your pocket is a ski lab: GPS, barometer, accelerometer"
description: "The three instruments inside an iPhone, what each can and can't measure on a mountain, and how fusing them gives honest ski telemetry with error bars."
---

# The phone in your pocket is a ski lab

A modern iPhone carries three instruments that matter on a mountain:
a GPS receiver, a barometric altimeter, and an inertial unit
(accelerometer plus gyroscope). None of them was designed for
skiing, and each one is wrong in its own characteristic way. The
useful part is that they're wrong in *different* ways, so if you
cross-check them you get telemetry none of them could produce alone.

This is the long version of how Alpy turns those sensors into the
numbers on your debrief, and why some of those numbers come with a
tilde or a ± attached.

## How accurate is phone GPS on a ski slope?

Good for position, worse for altitude and speed. Horizontally, with
open sky, a phone is
[typically within about 5 m](https://www.gps.gov/gps-accuracy) of
the truth, and worse near trees and buildings; altitude and speed are
where it degrades on a mountain.

Vertical error typically runs
[two to three times horizontal error](https://pmc.ncbi.nlm.nih.gov/articles/PMC12349078/),
and that study measured larger errors where the terrain blocked more
of the sky. For a ski app this is poison: altitude drives run
detection and vertical totals, and raw GPS altitude makes a
stationary phone "climb" and "descend" all afternoon.

Speed is harder to judge. iOS reports a speed with every fix (Apple
doesn't document exactly how it's computed). In
[a peer-reviewed test of four ski apps](https://pmc.ncbi.nlm.nih.gov/articles/PMC12349078/),
speed derived from phone positions had a median error of about
0.5 m/s (~2 km/h), worse at Zermatt than at Davos. iOS also reports a
[per-reading accuracy](https://developer.apple.com/documentation/corelocation/cllocation/speedaccuracy)
alongside every speed: the reading is plus or minus that many metres
per second. Alpy keeps the accuracy attached to the fastest speed
reading of the day and prints your top speed with it, as
54 ±3 km/h, because a headline number without its error bar is a
guess.

## The barometer: precise but unanchored

The pressure sensor measures altitude *changes*: Apple's Core
Motion reports it as a
[relative altitude](https://developer.apple.com/documentation/coremotion/cmaltitudedata/relativealtitude),
the change in metres since the first reading. Since iOS 15, iPhone 12
and later can also report an
[absolute altitude](https://developer.apple.com/documentation/coremotion/cmabsolutealtitudedata)
with its own accuracy estimate, but Alpy uses only the relative
stream and anchors it to GPS itself. The relative reading's weakness
is that a pressure sensor can't tell height from weather: by the
FAA's rule of thumb
[an inch of mercury reads as 1,000 feet](https://www.faa.gov/air_traffic/publications/atpubs/aim_html/chap7_section_2.html)
(about 9 m per hectopascal), and the Met Office classes a change of
[more than 6 hPa in three hours](https://www.metoffice.gov.uk/weather/guides/coast-and-sea/glossary)
as "very rapid". A fast-moving weather system during your ski day can
shift the pressure-derived altitude by tens of metres.

So the fusion is natural. Take the barometer's beautiful short-term
*shape* and anchor it to GPS's absolute *level* with an offset learned
slowly, over minutes rather than seconds. Learned fast, the offset
would re-import GPS wobble; learned slowly, it absorbs weather drift
while ignoring satellite noise. In a simulated unit test (synthetic
GPS wobble, an ideal barometer) the fused altitude's error is under
35% of raw GPS's; it hasn't yet been measured against surveyed truth
on real ski days. Every point Alpy records while tracking rides the
fused value, so run detection and vertical totals use it.

## What can a phone's accelerometer measure while skiing?

Two things nothing else on the phone can: airtime and turn load. Raw
accelerometer data picks up every chatter of the piste and every
pocket bounce, so both measurements look for signatures that noise
can't fake. Turn load has a trap, too.

In freefall,
[all three accelerometer axes converge to 0 g](https://www.nxp.com/docs/en/application-note/AN3151.pdf),
so the total acceleration reads zero whichever way the phone is
turned. That means it doesn't matter which pocket the phone is in:
total measured acceleration near 0 g (Alpy's threshold is 0.35 g)
*is* flight. Alpy calls it air when that signature holds for at
least a quarter second (we treat shorter dips as your knees
absorbing terrain), and discards "airs" longer than three seconds as
sensor glitches, on the grounds that three seconds of freefall is a
drop of about 44 m and you did not, in fact, huck that cliff. An air
that's still open when tracking stops is thrown away too, since
nothing confirms it ever landed.

For turn load, subtract gravity's direction and the acceleration
left over, perpendicular to gravity, is the sideways push of your
turns. The trap is spikes. A single landing rattle can spike for one
sample, and a "max G" feature that reports it is measuring how your
phone got bounced around. Alpy smooths the lateral signal over
roughly half a second and reports the peak of the *smoothed* curve,
which only a sustained carve can set. The number still wears a
tilde. It's an estimate until we've validated it against
instrumented skiing, and the app says so in the same breath it shows
the number.

## How does a phone count ski turns?

From GPS heading swings. Linked turns sweep your course
left-right-left, and each sustained swing past 30° (with hysteresis,
so jitter can't double-count) is a turn. The method's blind spot is
sampling: phone apps
[usually record about one position per second](https://pmc.ncbi.nlm.nih.gov/articles/PMC12349078/),
which limits how well they resolve turns (and Alpy only takes a new
fix every 10 m of movement), so tight turns blur together and the
count reads low. That's why the debrief says "~14 turns," never
"14", and why the *trend* matters more than the level. Cadence per
run, plotted across the day, shows whether your rhythm changes even
if every individual count is a little short. Terrain moves it as
well as tired legs, so the app shows it as a pattern and doesn't
offer a diagnosis. With four or more comparable runs (each at least
a minute long) the app will put a number on the change. With three
it refuses, because three points are too few to call a trend.

## The design rule under all of it

Every number in Alpy is classified as measured (GPS distance, fused
vertical, speed with its ±), estimated (turns, airtime, turn load,
always marked with ~), or sourced (weather, avalanche danger, always
naming the provider). Nothing is invented, and when a sensor can't
support a claim, the claim doesn't appear.

A phone will never match a lab, but a lab doesn't fit in your
jacket. We'd take a phone that's honest about its error bars over a
gadget that's confident about numbers it can't actually measure.

*All of this telemetry is free in Alpy, with nothing leaving your
phone. [The app](/) · [More from the blog](/blog/).*
