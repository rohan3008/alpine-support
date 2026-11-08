---
title: "How fast were you really going? Ski app top speed, honestly"
description: "Every ski app shows a top speed, but GPS speed is an estimate with a known error. Where the number comes from, and why Alpy prints the ±."
---

# How fast were you really going? Ski app top speed, honestly

GPS speed is an estimate with an error. In a
[peer-reviewed test of four ski apps](https://pmc.ncbi.nlm.nih.gov/articles/PMC12349078/),
speed computed from the apps' recorded positions had a median error
of about 0.5 m/s (~2 km/h), but the error grew at
higher speeds and in more obstructed terrain, and the worst single
reading was off by 21.5 m/s (over 75 km/h). So the honest answer is
the number on screen, plus or minus whatever the phone's own accuracy
estimate said at that instant. That's awkward news for every group
chat with someone claiming 70 km/h off their tracker.

## How do ski apps measure top speed?

On iPhone, the phone itself reports a speed with every GPS fix
(Apple doesn't document exactly how it's computed). iOS also reports
its own confidence alongside every speed reading: a
[`speedAccuracy`](https://developer.apple.com/documentation/corelocation/cllocation/speedaccuracy)
value in metres per second, meaning the speed is plus or minus that
much.

## How should a ski tracker report top speed?

With its error bar attached. Alpy keeps the accuracy value iOS
attached to the fastest speed reading of the day (the phone's own
estimate of how far off the reading could be) and prints the
headline number with it: 54 ±3 km/h.

A small ± means the phone itself was confident about that top speed,
so you can trust it more. A big ± means the phone flagged the
reading as shaky. At 54 ±6 you might have hit 60 or you might have
hit 48, and the app doesn't pretend to know which.

We think a top speed without its error bar is backwards, because the
error bar is what makes the number mean something. It's the same
reason Alpy labels turn counts and airtime as estimates. Measured
numbers and estimated numbers both have a place, as long as you can
tell which is which.

*Alpy is a free ski app for iPhone that labels every number by how it
was measured. [More](/).*
