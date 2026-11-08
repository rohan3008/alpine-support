---
title: "The freeze curve: reading the freezing level for your ski day"
description: "What the freezing level is, how it moves through a day and a storm, how to time soft snow and dodge ice, and how Alpy draws the curve."
---

# The freeze curve: reading the freezing level for your ski day

Snow quality matters as much as snow quantity, and one number does a
lot of the explaining: the
[freezing level](https://avalanche.org/avalanche-encyclopedia/weather/freezing-level/),
the elevation where the air temperature crosses 0 °C. Where that line
sits against your mountain, and how it moves, shapes much of a ski
day.

Alpy draws this as the *freeze curve*: freezing-level altitude, hour
by hour, from six hours ago to 24 hours ahead, with your resort's
base and summit marked and a rule at "now." Here's how to read it.

## How do you read a freeze curve?

Find where the freeze line sits against your resort's base and
summit. Below the base, the model has the whole mountain in
sub-freezing air; between base and summit, it's split, freezing
above the line and above freezing below it; above the summit, the
whole hill is in above-freezing air. Then watch which way the line
moves, overnight and through any storm.

With the freeze line below the base, the whole mountain is in
sub-freezing air, so precipitation should fall as snow top to
bottom. On a storm day this is the jackpot reading.

With the line between base and summit, things get interesting. The
mountain is split: above the line, winter; below it, spring. Rain at
the bottom can be snow up top (the saddest lift queue in skiing is
the one standing in drizzle below a snowline you can *see*). This
reading decides where to ski, since snow above the line stays wintry
and snow below it softens.

With the line above the summit, the whole hill is in above-freezing
air and surfaces soften through the day. That isn't automatically bad
news, and it's where timing comes in.

## When is spring corn snow at its best?

After a decent overnight refreeze, in the window when only the top
few inches have softened. That's avalanche.org's description of
[corn snow](https://avalanche.org/avalanche-encyclopedia/corn-snow/):
snow matured through repeated melt-freeze cycles, most often in
spring, and good corn skiing "hinges on a decent overnight
refreeze."

In settled spring weather the snowpack melts by day and refreezes by
night. On a clear spring day, dawn surfaces are frozen *boilerplate*.
As the day warms, the top few inches soften into *corn*: hero snow,
edge-friendly and forgiving. As melting goes deeper it turns to wet
slush, and per the same page the chance of wet snow avalanches can
quickly increase. Aspect shifts the schedule:
[snow temperature changes by aspect on sunny days](https://avalanche.org/avalanche-encyclopedia/terrain/slope-characteristics/aspect/).

The freeze curve helps you time it. If the curve dipped overnight
below the slopes you'll ski, the air there went below freezing, which
sets up a refreeze: expect firm snow early and softening as the day
warms. If there was no overnight dip at all, the air stayed above
freezing all night, so don't count on a refreeze. One glance at
whether the overnight curve dipped under your resort's base tells you
which movie you're in.

## Storms: the rain-snow line is a freeze line

During a storm, the rain-snow line sits a little below the freeze
curve: precipitation
[falls as snow a few hundred feet below the freezing level](https://avalanche.org/avalanche-encyclopedia/weather/freezing-level/)
before turning to rain. A storm that gets colder as it goes, with the
curve stepping down through the hours, tends to build a
[right-side-up](https://avalanche.org/avalanche-encyclopedia/right-side-up-storm/)
storm snowpack, denser below and lighter on top. That's usually the
more stable arrangement, if storm snow is the only concern. A storm
that warms as it passes can build the inverse, an
[upside-down storm](https://avalanche.org/avalanche-encyclopedia/upside-down-storm/)
with denser snow over lighter snow, which has the ingredients for
storm-slab avalanches. Wind can do the same, so the curve's
*direction during the storm hours* tells you only the temperature half
of that story.

## Where does the freezing-level forecast come from?

Alpy's curve is built from [Open-Meteo](https://open-meteo.com)
forecast data, which is model output for your resort's coordinates
(most global models update every 6 hours, regional ones every 1 to 3
hours, per Open-Meteo). It uses the
[`freezing_level_height`](https://open-meteo.com/en/docs) variable,
the altitude above sea level of the 0 °C level. It is a forecast and
not a measurement on your slope.

The app labels the curve with its source, and it's meant for
planning. The summit temperature shown beside it comes from the same
forecast, with Alpy passing your summit's height as Open-Meteo's
elevation setting (used for statistical downscaling). Expect it to
read much colder than a forecast for the village: the
[International Standard Atmosphere](https://en.wikipedia.org/wiki/International_Standard_Atmosphere)
cools 6.5 °C per 1,000 m, and between the 1,620 m base and 3,883 m
summit Alpy uses for Zermatt (2,263 m apart) that model gives about
15 °C. That figure comes from the model's gradient and isn't a
measurement for any given day.

## Using it in practice

The night before, check whether the curve dips below base overnight
(refreeze?) and where it sits at 09:00 (which half of the mountain
gets winter?). With a storm inbound, watch the curve's trend through
the storm hours (right-side-up or upside-down?). On a spring day, ski
the corn window while only the top few inches are soft, and be on the
deck before the slush wins.

*The freeze curve is free in Alpy for every resort, next to summit
weather and official avalanche bulletins. [The app](/) ·
[More from the blog](/blog/).*
