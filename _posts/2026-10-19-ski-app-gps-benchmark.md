---
title: "Independent science on ski-app GPS: the app barely matters. The processing does."
description: "A peer-reviewed benchmark ran four ski apps against survey-grade GNSS at Davos and Zermatt. The apps were indistinguishable — accuracy came down to phone, terrain and processing. Here is Alpy's processing, in the open."
---

# Independent science on ski-app GPS

Ski trackers love accuracy language — "professional grade GPS,"
"precision tracking." Rarely does anyone get to check. In 2023,
researchers did: they ran **four ski apps simultaneously** (Strava,
iSki, Slopes, Skitude) on four phones, against a 50 Hz
differential-GNSS reference rig carried on the skier's back, across
days at Davos and Zermatt. It's the only study of its kind we know
of, and it's
[openly published](https://pmc.ncbi.nlm.nih.gov/articles/PMC12349078/).

The findings, condensed:

- **Median horizontal error ~4.5 m.** High-end phones ~3.6–4.1 m,
  low-end ~6.4–6.8 m.
- **The differences between apps were negligible.** Read that twice:
  with the same phone on the same run, the four apps were effectively
  indistinguishable. The phone and the terrain decide.
- **Median speed error ~0.5 m/s** (~2 km/h), worse at high speed and
  in obstructed terrain — Zermatt's steep walls nearly doubled the
  position error relative to Davos.
- **Altitude couldn't even be assessed** — raw GNSS altitude error
  runs 2–3× horizontal, and the apps' altitude handling was opaque.

So when ski apps compete on "GPS quality," they're competing on a
layer where science says they're tied. The honest competition is in
what happens *after* the fix arrives. Here's Alpy's processing
pipeline — all of it, because an instrument that hides its method is
asking for faith, not trust.

## 1. The gate: implausible fixes never get in

Before a fix touches anything, two tests from the benchmark
literature's own recommendations: a fix reporting horizontal
accuracy worse than 50 m is discarded as noise, and a jump implying
more than 150 km/h between fixes is discarded as a receiver glitch.
A rejected glitch is also never used as the comparison baseline for
the next fix — one teleport can't poison an honest point behind it.

## 2. The speed cross-check: Doppler must agree with the map

Phone speed comes from satellite Doppler, which is good — and
occasionally produces a single spectacular spike. The infamous
"300 km/h top speed" screenshots come from exactly this. Alpy only
lets a speed reading contend for your day's maximum if the actual
displacement between fixes roughly supports it (with a generous
allowance, because the straight line between two fixes always
under-measures a carved path). A spike with no movement behind it
is dropped — not averaged in, not error-barred, dropped. And the
top speed that survives is still printed with its measurement
uncertainty: **54 ±3 km/h**.

## 3. Altitude: the barometer carries it

The study's bluntest finding is that raw GNSS altitude is the worst
channel. Alpy agrees, and fuses the phone's barometric altimeter —
sub-metre relative precision — with GPS as a slow absolute anchor.
Runs, vertical totals and airtime detection all ride the fused
curve. The method is written up in detail in
[our vertical-measurement post](/blog/how-ski-apps-measure-vertical/).

## 4. The battery guard: data you keep beats data you had

A tracker's worst failure isn't a noisy point — it's a phone dying
at 15:40 with the whole day unsaved. (Ski Tracks, the elder
statesman of the category, got this right years ago; credit where
due.) If your battery reaches 10% while tracking and you're not on
a charger, Alpy stops, saves the day, and tells you — the record
survives even if the phone doesn't.

## 5. Honesty about acquisition

GPS needs open sky and a minute to settle. While fix quality is
still poor — first minutes, deep lodge, canyon walls — Alpy says
"acquiring GPS, numbers firm up with open sky" instead of rendering
confident garbage. The study found position error roughly doubled
in obstructed terrain; the least an app can do is admit when it's
in that regime.

## The takeaway

Buy whichever ski app you like — the satellites don't care. But ask
what it does between the antenna and the screen, because that's
where the real differences live: gating, cross-checking, fusing,
saving early, and admitting uncertainty. Our pipeline is public,
our numbers carry their error bars, and the study that keeps
everyone honest is
[right here](https://pmc.ncbi.nlm.nih.gov/articles/PMC12349078/).

*Alpy is a free, private ski app for iPhone. Every number labeled by
how it was measured. [The app](/) · [More from the blog](/blog/).*
