---
title: "How fast were you really going? Ski app top speed, honestly"
description: "Every ski app shows a top speed. Almost none show the measurement error. Why GPS speed has error bars and why Alpy prints them."
---

# How fast were you really going? Ski app top speed, honestly

Every ski tracker ends the day with a top speed, and every group chat
has someone claiming 70 km/h off it. Here's the uncomfortable bit:
GPS speed is an estimate with a known error, and at the moment your
app recorded that peak, the error might have been ±2 km/h — or
±10 km/h, if you were between trees or mid-turn with a poor satellite
view.

## Where the number comes from

Phones don't compute speed by dividing distance by time between two
fixes (that would be noisy beyond use). They use the Doppler shift of
the satellite signals themselves, which is far better — and still
imperfect. iOS actually reports its own confidence alongside every
speed reading: a `speedAccuracy` value in metres per second. Most
apps throw it away.

## What an honest tracker does with it

Alpy keeps the accuracy value from the exact moment your day's top
speed was set, and prints the headline number with it: **54 ±3 km/h**.
Two things follow:

- A top speed with a small ± was a clean measurement on an open
  piste. Trust it.
- A top speed with a big ± happened during bad GPS geometry. Maybe
  you hit 61, maybe 49. The app refuses to pretend it knows.

No other ski app we've found publishes its measurement error. We
think that's backwards: the error bar is what makes the number mean
something. It's the same reason Alpy labels turn counts and airtime
as estimates — measured numbers and estimated numbers both have a
place, as long as you can tell which is which.

*Alpy is a free ski app for iPhone that labels every number by how it
was measured. [More](/).*
