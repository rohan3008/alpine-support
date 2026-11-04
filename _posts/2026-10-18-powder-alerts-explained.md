---
title: "Powder alerts: how to hear about fresh snow before the lifts open"
description: "What a powder alert is, where the snow data comes from, and how Alpy's background alerts work without a server or an account."
---

# Powder alerts: how to hear about fresh snow before the lifts open

A powder day is mostly a logistics problem: the snow falls overnight,
the best of it is skied out by 11, and the difference between first
chair and a lazy start is whether anything told you to set an alarm.

## Where do powder forecasts come from?

From weather models, not snow stakes. There's no sensor at the top
of most mountains reporting "powder." Alpy reads model snowfall for
your resort's summit: a forecast-grade number, not a snow stake
measurement, so the app shows the model number and names the
source — you know what kind of number you're reading.

The source is [Open-Meteo](https://open-meteo.com), which combines forecast models
from national weather services into hourly snowfall estimates for any coordinates —
including your resort's summit. Resorts' own morning reports
(hand-measured, occasionally optimistic) and model estimates
disagree routinely.

## How does a powder alert work without a server?

On the phone. Most alert features mean an account and a
push-notification server that knows your resorts. Alpy's alert runs
on the phone instead: iOS background refresh wakes the app a few
times a day, it checks the forecast for the resorts you follow, and
if fresh snow crosses the threshold you set — say 15 cm in 24 hours
— you get a local notification.

A repeat guard keeps one storm from pinging you every few hours.

The trade-off is honest: iOS
[decides when background refresh runs](https://developer.apple.com/documentation/backgroundtasks/bgtaskrequest/earliestbegindate),
so
an alert can land at 06:40 instead of 06:00. The benefit is just as
honest: nobody — including us — knows which resorts you follow,
because there is no server to tell.

*Powder alerts are free in Alpy, with the threshold under your
control in Settings. [More about the app](/).*
