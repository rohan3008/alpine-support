---
title: "How fast were you really going? Ski app top speed, honestly"
description: "Every ski app shows a top speed. Almost none show the measurement error. Why GPS speed has error bars and why Alpy prints them."
---

# How fast were you really going? Ski app top speed, honestly

GPS speed is an estimate with a known error. At the moment your app
recorded your top speed, that error might have been ±2 km/h — or
±10 km/h, if you were between trees or mid-turn with a poor satellite
view. So the honest answer is the number on screen, plus or minus
whatever the phone's own accuracy estimate said at that instant.

That's the uncomfortable bit for every group chat with someone
claiming 70 km/h off their tracker.

## How do ski apps measure top speed?

Phones don't compute speed by dividing distance by time between two
fixes (that would be noisy beyond use). They use the Doppler shift of
the satellite signals themselves, which is far better — and still
imperfect. iOS reports its own confidence alongside every speed
reading: a
[`speedAccuracy`](https://developer.apple.com/documentation/corelocation/cllocation/speedaccuracy)
value in metres per second. Most apps throw it away.

## How should a ski tracker report top speed?

With its error bar attached. Alpy keeps the accuracy value from the
exact moment your day's top speed was set — the phone's own estimate
of how far off the reading could be — and prints the headline number
with it: **54 ±3 km/h**.

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
