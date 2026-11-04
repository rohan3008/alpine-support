---
title: "How ski apps measure vertical — and why GPS lies about it"
description: "GPS altitude wobbles 10–20 m on a mountain. How barometer fusion gives a ski tracker honest vertical, and what Alpy does differently."
---

# How ski apps measure vertical — and why GPS lies about it

Ask your phone where you are and it's accurate to a few metres. Ask it
how *high* you are and it can miss by 10–20 m — vertical error is
GPS's weakest axis (typically
[two to three times the horizontal error](https://pmc.ncbi.nlm.nih.gov/articles/PMC12349078/)),
and it gets worse in steep terrain, where the satellites you'd need
for a clean fix are hidden behind the mountain itself.

For a ski tracker this matters everywhere: vertical drop is the
number skiers brag about, run detection works by watching altitude
trends, and airtime detection needs a clean altitude signal. If the
raw GPS altitude wobbles ±15 m, a parked phone "descends" and
"climbs" all afternoon.

## What does a phone use to measure altitude?

Two instruments: GPS and a **barometric altimeter**, which modern
iPhones carry alongside it. GPS knows your absolute height but
wobbles; the barometer is smooth but only knows how your height is
*changing*. Neither is good enough alone for honest ski vertical,
which is why the useful answer is to combine them.

The barometer is the opposite of GPS: beautifully smooth — it resolves
altitude changes under a metre — but *relative*. It doesn't know your
elevation, only how it's changing, and its baseline drifts as weather
systems move through (a passing front can shift it tens of metres
over hours).

So you have one instrument that's accurate but noisy, and one that's
precise but unanchored.

## How do ski apps combine the barometer and GPS?

By fusing them: take the barometer's smooth *shape* and pin it to
GPS's absolute *level* with a slowly-learned offset. The offset
has to adapt slowly — over minutes, not seconds — so it absorbs
weather drift without re-importing GPS wobble.

This is what Alpy does while you track. Every recorded fix rides the
fused altitude: in our tests the fusion cuts GPS altitude noise by
more than 65%, which means cleaner run detection, honest vertical
totals, and an airtime detector that isn't fooled by satellite
jitter. On phones without a barometer the app falls back to GPS alone
— and it tells you which it used, because an instrument that doesn't
disclose its method isn't an instrument.

*Alpy is a free ski app for iPhone — no account, no ads, and your GPS
never leaves the phone. [What it does](/).*
