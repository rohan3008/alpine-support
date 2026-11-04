---
title: "The freeze curve: reading the freezing level for your ski day"
description: "What the freezing level is, how it moves through a day and a storm, how to time soft snow and dodge ice — and how Alpy draws the curve."
---

# The freeze curve: the one chart that explains your ski day

Snow quality matters as much as snow quantity, and one number does a
lot of the explaining: the
[**freezing level**](https://avalanche.org/avalanche-encyclopedia/weather/freezing-level/) —
the elevation where the air temperature crosses 0 °C. Where that line
sits against your mountain, and how it moves, shapes much of a ski
day.

Alpy draws this as the *freeze curve*: freezing-level altitude, hour
by hour, from six hours ago to 24 hours ahead, with your resort's
base and summit marked and a rule at "now." Here's how to read it.

## How do you read a freeze curve?

Find where the freeze line sits against your resort's base and
summit. Below the base, the model has the whole mountain in
sub-freezing air; between base and summit, it's split — freezing
above the line, above freezing below it; above the summit, the whole
hill is in above-freezing air. Then watch which way the line moves,
overnight and through any storm.

**Freeze line below the base.** The whole mountain is in
sub-freezing air, so precipitation should fall as snow top to
bottom. On a storm day this is the jackpot reading.

**Freeze line between base and summit** — the interesting case. The
mountain is split: above the line, winter; below it, spring. Rain at
the bottom can be snow up top (the saddest lift queue in skiing is
the one standing in drizzle below a snowline you can *see*). This
reading decides where to ski: snow above the line stays wintry,
snow below it softens.

**Freeze line above the summit.** The whole hill is in
above-freezing air and surfaces soften through the day — which is
not automatically bad news, and that's where timing comes in.

## When is spring corn snow at its best?

After a decent overnight refreeze, in the window when only the top
few inches have softened. That's avalanche.org's description of
[corn snow](https://avalanche.org/avalanche-encyclopedia/corn-snow/):
snow matured through repeated melt-freeze cycles, most often in
spring, and good corn skiing "hinges on a decent overnight
refreeze."

In settled spring weather the snowpack melts by day and refreezes by
night. The sequence on a clear spring day: dawn surfaces are frozen
*boilerplate*. As the day warms, the top few inches soften into
*corn*: hero snow, edge-friendly and forgiving. As melting goes
deeper it turns to wet slush — and, per the same page, the chance of
wet snow avalanches can quickly increase. Aspect shifts the
schedule:
[snow temperature changes by aspect on sunny days](https://avalanche.org/avalanche-encyclopedia/terrain/slope-characteristics/aspect/).

The freeze curve helps you time it. Overnight dip below the slopes
you'll ski → the air there went below freezing, the setup for a
refreeze → expect firm snow early and softening as the day warms.
No overnight dip at all → the air stayed above freezing all night,
so don't count on a refreeze. One glance at whether the overnight
curve dipped under your resort's base tells you which movie you're
in.

## Storms: the rain–snow line is a freeze line

During a storm, the rain–snow line sits a little below the freeze
curve: precipitation
[falls as snow a few hundred feet below the freezing level](https://avalanche.org/avalanche-encyclopedia/weather/freezing-level/)
before turning to rain. A storm that gets colder as it goes — curve
stepping down through the hours — tends to build a
[right-side-up](https://avalanche.org/avalanche-encyclopedia/right-side-up-storm/)
storm snowpack, denser below and lighter on top — usually the more
stable arrangement, if storm snow is the only concern. A storm that warms as it passes can build the
inverse: an
[upside-down storm](https://avalanche.org/avalanche-encyclopedia/upside-down-storm/),
denser snow over lighter snow — the ingredients for storm-slab
avalanches. Wind can do the same, so the curve's *direction during
the storm hours* tells you the temperature half of that story, not
all of it.

## Where does the freezing-level forecast come from?

Alpy's curve is built from [Open-Meteo](https://open-meteo.com)
forecast data — model output for your resort's coordinates (most
global models update every 6 hours, regional ones every 1–3 hours,
per Open-Meteo), using its
[`freezing_level_height`](https://open-meteo.com/en/docs) variable:
the altitude above sea level of the 0 °C level. It is a forecast,
not a measurement on your slope.

The app does not pretend otherwise — the curve is labeled with its
source, and it's a planning instrument, not a promise. The summit
temperature shown beside it comes from the same forecast, with
Alpy passing your summit's height as Open-Meteo's elevation
setting (used for statistical downscaling). Expect it to read much
colder than a forecast for the village: the
[International Standard Atmosphere](https://en.wikipedia.org/wiki/International_Standard_Atmosphere)
cools 6.5 °C per 1,000 m, and between the 1,620 m base and
3,883 m summit Alpy uses for Zermatt (2,263 m apart) that model
gives about 15 °C. That's the model's gradient, not a measurement
for any given day.

## Using it in practice

The night before: check whether the curve dips below base
overnight (refreeze?) and where it sits at 09:00 (which half of the
mountain gets winter?). Storm inbound: watch the curve's trend
through the storm hours (right-side-up or upside-down?). Spring
day: ski the corn window while only the top few inches are soft,
and be on the deck before the slush wins.

One line on a chart, and most of a ski day's decisions fall out of
it. That's the best kind of instrument.

*The freeze curve is free in Alpy for every resort, next to summit
weather and official avalanche bulletins. [The app](/) ·
[More from the blog](/blog/).*
