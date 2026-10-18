---
title: "The phone in your pocket is a ski lab: GPS, barometer, accelerometer"
description: "A long look at the three instruments inside an iPhone, what each one can and cannot measure on a mountain, and how fusing them produces honest ski telemetry — vertical, airtime, turn load, and error bars."
---

# The phone in your pocket is a ski lab

A modern iPhone carries three instruments that matter on a mountain:
a GPS receiver, a barometric altimeter, and an inertial unit —
accelerometer plus gyroscope. None of them was designed for skiing.
Each one lies in its own characteristic way. But their lies are
*uncorrelated*, and that's the whole game: cross-check three flawed
instruments and you get telemetry none could produce alone.

This is the long version of how Alpy turns those sensors into the
numbers on your debrief — and why some of those numbers come with a
tilde or a ± attached.

## GPS: great at where, mediocre at how high, sneaky about how fast

Satellite positioning solves your location from timing differences
across visible satellites. Horizontally, with open sky, a phone sits
within a few metres of the truth. Two things degrade on a mountain:

**Altitude.** Vertical error runs two to three times horizontal
error by geometry alone — the satellites that would pin your height
best are below the horizon. Add a valley wall blocking half the sky
and ±15 m of altitude wobble is normal. For a ski app this is
poison: altitude drives everything (run detection, vertical totals),
and raw GPS altitude makes a stationary phone "climb" and "descend"
all afternoon.

**Speed.** Phones don't derive speed from successive positions
(hopeless noise); they use the Doppler shift of the satellite
carriers, which is much better — typically within 1–2 km/h in open
terrain. But iOS reports a per-reading confidence alongside every
speed, and that confidence collapses in trees and tight terrain.
Most apps discard the confidence number. Alpy records the one
attached to the moment your top speed was set, and prints the result
as **54 ±3 km/h** — because a headline number without its error bar
is a guess wearing a suit.

## The barometer: precise, smooth, and unanchored

The pressure sensor resolves altitude *changes* of well under a
metre and reacts instantly — a sensor you could feel a staircase
with. Its weaknesses mirror GPS's strengths: it has no idea of your
absolute altitude, and its baseline drifts as weather moves through.
A front passing during your ski day can shift the pressure-derived
altitude by tens of metres — ironic, since storm days are exactly
when you're skiing.

So the fusion is natural. Take the barometer's beautiful short-term
*shape*; anchor it to GPS's absolute *level* with an offset learned
slowly — over minutes, not seconds. Learned fast, the offset would
re-import GPS wobble; learned slow, it absorbs weather drift while
ignoring satellite noise. In our test harness the fused altitude
tracks truth with less than a third of raw GPS's error. Every point
Alpy records while tracking rides the fused value, which is why run
detection doesn't stutter and vertical totals don't inflate.

## The accelerometer: two honest tricks and a trap

Raw accelerometer data is the noisiest signal on the phone — every
chatter of the piste, every pocket bounce. It still yields two
measurements nothing else can, both built on the same idea: look
for signatures that can't be faked by noise.

**Airtime.** In freefall, an accelerometer reads zero — you, the
phone, and the sensor's test mass all accelerate identically, so
nothing presses on anything. It doesn't matter which pocket the
phone is in or which way it's turned: total measured acceleration
near 0 g *is* flight. Alpy calls it air when that signature holds
for at least a quarter second (shorter dips are the suspension of
your knees absorbing terrain), and discards "airs" longer than
three seconds as sensor glitches, on the grounds that you did not,
in fact, huck a seventy-metre cliff. An air that's still open when
tracking stops is thrown away too: unclosed air is unproven air.

**Turn load.** Subtract gravity's direction and the acceleration
left over, perpendicular to gravity, is the sideways push of your
turns — carve hard and it climbs toward 1 g and beyond. The trap is
spikes: a single landing rattle can read 3 g for one sample, and a
"max G" feature that reports it is measuring your phone's ride, not
your skiing. Alpy smooths the lateral signal over roughly half a
second and reports the peak of the *smoothed* curve — only a
sustained carve can set it. The number still wears a tilde. It's an
estimate until we've validated it against instrumented skiing, and
the app says so in the same breath it shows the number.

## Turns: the estimate that's honest about being one

Turn counting uses GPS heading swings: linked turns sweep your
course left-right-left, and each sustained swing past 30° (with
hysteresis, so jitter can't double-count) is a turn. The method's
blind spot is sampling: at one fix per second, tight slalom turns
blur together and the count reads low. That's why the debrief says
"~14 turns," never "14" — and why the *trend* matters more than the
level. Cadence per run, plotted across the day, shows your rhythm
fading as your legs go even if every individual count is a little
short. With four or more comparable runs the app will put a number
on the fade; with three it refuses, because three points claiming a
trend is how instruments become horoscopes.

## The design rule under all of it

Every number in Alpy is classified: **measured** (GPS distance,
fused vertical, speed with its ±), **estimated** (turns, airtime,
turn load — always marked with ~), or **sourced** (weather,
avalanche danger — always naming the provider). Nothing is invented,
and when a sensor can't support a claim, the claim doesn't appear.

A phone will never match a lab. But a lab doesn't fit in your
jacket, and a phone that's honest about its error bars beats a
gadget that's confident about numbers it can't actually measure.

*All of this telemetry is free in Alpy, with nothing leaving your
phone. [The app](/) · [More from the blog](/blog/).*
