---
title: "Lift lines: the only honest queue tracker has your name on it"
description: "Alpy estimates how long you stood in each lift line from your own GPS — per lift, per day, with season averages. Why a no-server app can't show live crowds, and why your own history is the useful number anyway."
---

# Lift lines: the only honest queue tracker has your name on it

<p align="center"><img src="/assets/screens/alpy-ski-debrief.png" alt="The Ski Debrief, where the Lift Lines card lives alongside the per-run registers" width="280" style="border-radius:22px; border:1px solid #d0d7de; box-shadow:0 8px 24px rgba(10,17,31,.15);" loading="lazy"></p>


Every skier knows the feeling: the day felt great, but somewhere an
hour evaporated into lift queues. Alpy now measures that hour — and
tells you which lifts ate it.

## How it measures a queue

When your tracked day is saved, the app looks at the gap between each
run's end and the following lift ride, scanning **backwards** from the
moment the climb starts and adding up the time you were essentially
stationary (under about 0.6 m/s — standing, with shuffle-forward
moments tolerated). Scanning backwards matters: it's what keeps your
lunch out of the number, because the walk from the restaurant to the
lift breaks the standing streak. The result is labeled an estimate,
because GPS genuinely cannot tell a lift line from you finishing a
sandwich at the base — but the backwards scan makes the honest cases
land right.

Each wait is then matched to a **named lift** by comparing the ascent
that follows with the resort's OpenStreetMap lift lines — your track
hugs the lift you actually rode.

## What you see

In the day's debrief, a Lift Lines card: total minutes waiting, then
a bar per lift — "Gondola ×3 · ~11 min". Once a lift has enough rides
in your history, a season line appears underneath: average wait, ride
count, and a morning/afternoon split. That last one is the quietly
useful number: many lifts queue hard at 9:30 and walk on at 13:30,
and after a few tracked days *your own data* shows exactly which.

Walk-on rides count as zero-minute waits on purpose. If they didn't,
"average wait" would secretly mean "average wait when there was a
line" — a worst case dressed up as a typical one.

## Why not live crowds?

Apps with servers can show live lift waits by aggregating thousands
of users. Alpy has no server, no accounts, and sends nothing off your
phone — that's a founding constraint, not a missing feature. So the
card says what it is: *your own days only; this can't see today's
crowds, only your history with them.* For planning your own week at
your own resort, that history turns out to be most of what you
wanted anyway.

*Lift Lines appears automatically in the [Ski Debrief](../blog/first-day-with-alpy/)
of any tracked day with a couple of minutes of queueing. Free, like
the rest of [Alpy](../).*
