---
title: "Lift lines: a queue tracker built from your own GPS"
description: "Alpy estimates your wait in each lift line from your own GPS, per lift and per day, and explains why an app with no server can't show live crowds."
---

# Lift lines: a queue tracker built from your own GPS

<p align="center"><img src="/assets/screens/alpy-ski-debrief.png" alt="The Ski Debrief: day totals above the per-run registers" width="280" style="border-radius:22px; border:1px solid #d0d7de; box-shadow:0 8px 24px rgba(10,17,31,.15);" loading="lazy"></p>


Most skiers have had a day that felt great while somewhere an hour
went missing in lift queues. Alpy now measures that hour and tells you
which lifts took it.

## How can a ski app measure lift line wait times?

From your own GPS. Working from your saved day's track, the app looks at
the gap between each run's end and the following lift ride. It scans
**backwards** from the moment the climb starts and adds up the time
you were essentially stationary (under about 0.6 m/s, which means
standing, with shuffle-forward moments tolerated).

Scanning backwards is what keeps your lunch out of the number, because
the walk from the restaurant to the lift breaks the standing streak.
The result is labeled an estimate, since GPS genuinely cannot tell a
lift line from you finishing a sandwich at the base.

Each wait is then matched to a **named lift** by comparing the ascent
that follows with the resort's OpenStreetMap
[lift lines](https://wiki.openstreetmap.org/wiki/Key:aerialway). Your
track hugs the lift you actually rode.

## What you see

The day's debrief has a Lift Lines card showing total minutes waiting,
then a bar per lift: "Gondola · ×3 … ~11 min". Once a lift has four
rides in your history, a season line appears underneath with average
wait and ride count. From six rides it adds a morning/afternoon split
(before and after noon). I find that split the most useful number on
the card. If a lift queues in the morning and walks on after lunch,
*your own data* shows it after a few tracked days.

Walk-on rides count as zero-minute waits on purpose. Otherwise
"average wait" would secretly mean "average wait when there was a
line", which is a worst case dressed up as a typical one.

## Can Alpy show live lift queues?

No. Live crowd numbers would need many skiers' positions pooled on a
server. Alpy has no server and no accounts, and it sends nothing off
your phone. We designed it that way from the start. So the card says
what it is: *"Your own days only — nothing is shared, so this can't
see today's crowds, only your history with them."* For planning your
own week at your own resort, we think that history is most of what you
want anyway.

*Lift Lines appears automatically in the [Ski Debrief](/blog/first-day-with-alpy/)
of any tracked day with at least two minutes of queueing. Free, like
the rest of [Alpy](/).*
