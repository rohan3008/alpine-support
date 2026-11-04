---
title: "Independent science on ski-app GPS: the app barely matters. The phone and terrain do."
description: "A peer-reviewed study ran four ski apps against survey-grade GNSS: differences between apps were negligible. Accuracy came from the phone and terrain."
---

# Independent science on ski-app GPS

Every ski tracker shows you numbers; rarely does anyone get to
check how accurate they are. In winter 2022/23, researchers did (the
study was published in 2025): two skiers ran **four ski apps
simultaneously** (Strava, iSki, Slopes, Skitude) on four phone models,
against a 50 Hz differential-GNSS reference rig carried on the back,
across three days at Davos and Zermatt. It's the only study of its kind we know
of, and it's
[openly published](https://pmc.ncbi.nlm.nih.gov/articles/PMC12349078/)
(Petrella, Ellenberger and Gilgien, *PLOS One*, 2025).

## How accurate is ski-app GPS?

At the median, about 4.5 m of horizontal position error and about
0.5 m/s (~2 km/h) of speed error (speed the researchers computed from
each app's recorded positions) — and the differences between the
four apps were negligible. What moved the numbers was the phone
(high-end beat low-end) and the terrain (Zermatt's more obstructed
sky versus Davos).

The findings, condensed:

- **Median horizontal error ~4.5 m.** High-end phones ~3.6–4.1 m,
  low-end ~6.4–6.8 m.
- **The differences between apps were negligible.** Read that twice:
  running side by side on the same phones, the four apps were
  effectively indistinguishable — the authors note the apps read the
  same position data the phone records. The phone and the terrain
  decide.
- **Median speed error ~0.5 m/s** (~2 km/h), worse at high speed and
  at Zermatt, where terrain blocked more of the sky; there the
  median position error was about 1.7 times that at Davos.
- **Altitude couldn't even be assessed** — raw GNSS altitude error
  runs 2–3× horizontal, and the apps' altitude handling was opaque.

So when ski apps compete on "GPS quality," they're competing on a
layer where, for the four apps tested, the science says they're
tied. The honest competition is in
what happens *after* the fix arrives. Here's Alpy's processing
pipeline — all of it, because an instrument that hides its method is
asking for faith, not trust.

## 1. The gate: implausible fixes never get in

Before a fix touches anything, it has to pass two tests of our own,
set conservatively: a fix reporting horizontal
accuracy worse than 50 m is discarded as noise, and a jump implying
more than 150 km/h between fixes is discarded as a receiver glitch.
A rejected glitch is also never used as the comparison baseline for
the next fix — one teleport can't poison an honest point behind it.

## 2. The speed cross-check: speed must agree with the map

iOS reports a speed with every fix, and a single speed can be badly
wrong: in the study (which computed speed from each app's recorded
positions) the worst speed error was 21.5 m/s, over 75 km/h. Above about 29 km/h, Alpy only lets a speed reading contend
for your day's maximum if the actual displacement between fixes
roughly supports it (with a generous allowance, because the straight
line between two fixes always under-measures a carved path). A spike
with no movement behind it is dropped — not averaged in, not
error-barred, dropped. And the top speed is printed with the phone's
own accuracy estimate for the fastest reading of the day:
**54 ±3 km/h**.

## 3. Altitude: the barometer carries it

The study couldn't assess altitude at all, but it notes that
altitude typically carries two to three times the horizontal error,
and that barometers can only improve relative altitude, not absolute
position. Alpy takes that literally: it fuses the barometer's
relative altitude with GPS as a slow absolute anchor. Run detection
and vertical totals ride the fused curve; airtime comes from the
accelerometer instead. The method is written up in detail in
[our vertical-measurement post](/blog/how-ski-apps-measure-vertical/).

## 4. The battery guard: data you keep beats data you had

A tracker's worst failure isn't a noisy point — it's a phone dying
at 15:40 with the whole day unsaved. (Ski Tracks'
[release notes](https://apps.apple.com/au/app/ski-tracks/id365724094)
say its Watch app saves automatically on low battery too; credit
where due.) If your battery reaches 10% while tracking and you're not on
a charger, Alpy stops, saves the day, and tells you — the record
survives even if the phone doesn't.

## 5. Honesty about acquisition

The study warns that "at the beginning of a tracking period or in
difficult GNSS conditions, position errors can be very large." While
the phone reports a fix accuracy worse than 35 m — first minutes,
deep lodge, canyon walls — Alpy says "Acquiring GPS — numbers firm
up with open sky" instead of rendering confident garbage. The study
found median position error about 1.7 times larger in Zermatt's
obstructed terrain; the least an app can do is admit when it's in
that regime.

## Which ski app has the most accurate GPS?

Among the four apps the study tested, none measurably: on the same
phone they were effectively tied. Buy whichever ski app you like — the satellites don't care. But ask
what it does between the antenna and the screen, because that's
where the real differences live: gating, cross-checking, fusing,
saving early, and admitting uncertainty. Our pipeline is written
down above, our numbers carry their error bars, and the study that keeps
everyone honest is
[right here](https://pmc.ncbi.nlm.nih.gov/articles/PMC12349078/).

*Alpy is a free, private ski app for iPhone. Every number labeled by
how it was measured. [The app](/) · [More from the blog](/blog/).*
