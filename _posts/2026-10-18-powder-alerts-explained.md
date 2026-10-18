---
title: "Powder alerts: how to hear about fresh snow before the lifts open"
description: "What a powder alert is, where the snow data comes from, and how Alpy's background alerts work without a server or an account."
---

# Powder alerts: how to hear about fresh snow before the lifts open

A powder day is mostly a logistics problem: the snow falls overnight,
the best of it is skied out by 11, and the difference between first
chair and a lazy start is whether anything told you to set an alarm.

## Where fresh-snow numbers come from

There's no sensor at the top of most mountains reporting "powder."
What exists is weather models: Alpy uses
[Open-Meteo](https://open-meteo.com), which assimilates station and
satellite data into hourly snowfall estimates for any coordinates —
including your resort's summit. Model snowfall is a forecast-grade
number, not a snow stake measurement; resorts' own morning reports
(hand-measured, occasionally optimistic) and model estimates
disagree routinely. Alpy shows the model number and names the
source, so you know what kind of number you're reading.

## How the alert works without a server

Most alert features mean an account and a push-notification server
that knows your resorts. Alpy does it on the phone instead: iOS
background refresh wakes the app a few times a day, it checks the
forecast for the resorts you follow, and if fresh snow crosses the
threshold you set — say 15 cm in 24 hours — you get a local
notification. A repeat guard keeps one storm from pinging you every
few hours.

The trade-off is honest: iOS decides when background refresh runs, so
an alert can land at 06:40 instead of 06:00. The benefit is just as
honest: nobody — including us — knows which resorts you follow,
because there is no server to tell.

*Powder alerts are free in Alpy, with the threshold under your
control in Settings. [More about the app](/).*
