---
title: "Powder alerts: how to hear about fresh snow before the lifts open"
description: "What a powder alert is, where the snow data comes from, and how Alpy's background alerts work without a server or an account."
---

# Powder alerts: how to hear about fresh snow before the lifts open

A powder day is mostly a logistics problem. Whether you get first
chair or a lazy start comes down to whether anything told you to set
an alarm.

## Where do powder forecasts come from?

In Alpy's case, from weather models, not snow stakes. Alpy reads
model snowfall for your resort's summit, which is a forecast-grade
number, so the app shows the model number and names the source and
you know what kind of number you're reading.

The source is [Open-Meteo](https://open-meteo.com), which draws on
weather models from over 15 national weather services and serves
[hourly snowfall](https://open-meteo.com/en/docs) for any
coordinates, including your resort's summit. A resort's own
morning report is a different kind of number, so don't expect the
two to match.

## How does a powder alert work without a server?

Alpy has no account and no push-notification server, so the alert
runs on the phone. iOS background refresh wakes the app (Alpy asks
for no sooner than six hours after the last check), it checks the
48-hour snowfall forecast for your selected resort, and if that
crosses the threshold you set (15 cm by default, adjustable from 5
to 50 cm) you get a local notification.

A repeat guard allows at most one alert every 20 hours, so one storm
doesn't ping you all day.

There's a cost to doing it this way. iOS
[decides when background refresh runs](https://developer.apple.com/documentation/backgroundtasks/bgtaskrequest/earliestbegindate)
and guarantees only that the task won't start earlier than asked,
so an alert can land later than you'd like. In exchange, we don't
know which resort you follow, because there is no Alpy server to
tell. The only request is the forecast fetch itself, which goes to
Open-Meteo with the resort's coordinates.

*Powder alerts are free in Alpy, with the threshold under your
control in Settings. [More about the app](/).*
