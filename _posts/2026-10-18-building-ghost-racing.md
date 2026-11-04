---
title: "How we built ghost racing for skiing: a technical deep-dive"
description: "How Alpy turns OpenStreetMap pistes into segments, handles partial descents, computes F1-style deltas and races your ghost live on the mountain."
---

# How we built ghost racing for skiing: a technical deep-dive

Alpy lets you race a ghost of yourself down a ski run — live, on the
mountain, with an F1-style time delta ticking on your screen. This
post is the engineering story: what made it hard, what we got wrong,
and the four or five small decisions that make the feature honest
rather than just flashy. It's written for people who like knowing how
their instruments work; no code required to follow along.

## The problem: ski runs don't have finish lines

Strava's [Live Segments](https://support.strava.com/hc/en-us/articles/207343830-Live-Segments)
race a ride or run against your PR on a segment — a stretch of road
or trail you enter and complete. A ski run is a wide ribbon of
snow, not a line. Two descents of the same piste never trace the
same GPS line, never start at the same point, and often end in different places —
one pulls up at the lift, the other carries on to the restaurant.

So the first decision is what a "segment" even is. Our answer: a
segment is a *named piste in OpenStreetMap*. OSM contributors have
mapped ski runs as coordinate chains, tagged with names and
[difficulties](https://wiki.openstreetmap.org/wiki/Key:piste:difficulty).
If we can tell which named run a descent happened on, each descent
becomes an *attempt* on that run, and a record book follows
naturally.

## How does Alpy know which run you skied?

By majority vote. Take every GPS fix in a descent, and for each one
ask: which named piste's geometry passes within a 40-metre corridor
of this point? Whichever run claims the majority of the points claims
the descent.

The corridor absorbs both GPS error and the width of a real piste;
the majority rule stops a run from being claimed by the piste you
merely crossed at an intersection.

Just as important is what happens when *nothing* claims the points:
the descent is honestly unnamed. Off-piste lines, unnamed connector
tracks, resort areas OSM hasn't mapped — the app says "Unnamed line" and that
descent never enters the record book. We considered snapping unnamed
descents to the nearest run and decided against it: an instrument
that guesses is worse than an instrument that admits ignorance.

## How do you stop half a run from setting a record?

With the **full-drop rule**: for every segment we track the deepest
vertical drop any attempt has recorded, and an attempt only competes
for records if its own drop is at least 80% of that. Below the line,
it's marked *partial* — kept in your history, excluded from the
race.

We needed it fast. The first version of the record book had an
exploit we found quickly: bail out halfway down a run and
you'd post an unbeatable "record," because half a run takes half the
time. Any skier would spot the cheat instantly; the code had to. The
threshold is deliberately forgiving — 80% is our judgement call, not
a measured figure: altitude noise and different pull-out points
shave drop off honest runs, and a rule that disqualified them would
be worse than the exploit.

One subtlety: the "deepest drop" baseline is computed across all
attempts *including today's*, so the first time you ski the full
run, it correctly resets the bar for what "full" means.

## How do you compare two ski runs that took different lines?

By vertical drop, not position. You compare the two runs at the same
depth below the start: when you've dropped 180 m, how long had the
ghost taken to drop 180 m? The difference in time is your delta, and
it holds up even when the two runs took different lines down the
same piste.

Getting there was the genuinely interesting problem. You're forty
seconds into today's descent. Your PR took a different line — entered three
metres higher, swung wider at the second pitch. "Where was the ghost
at forty seconds?" is easy to answer but useless to display, because
position isn't progress: the ghost might be ahead on the clock but
behind on the mountain.

The honest comparison axis is **vertical drop**. Descent is monotone
— you can traverse, but the cumulative drop of a run only grows — so
"how many metres below the start am I?" is a progress bar that works
for any line down the same mountain. We store every attempt's
*descent profile*: elapsed time against cumulative drop, clamped
monotone so altitude wobble can't make the curve dip backwards.

The delta is then an inverse lookup: I've dropped 180 m in 40 s —
when did the ghost pass 180 m? If the ghost needed 43 s, you're
**−3.0 s** up. Comparing at equal progress rather than equal time is
what makes it robust to the two runs taking different lines:
metres of mountain are the shared currency.

The chip stays silent for the first 10 m of drop. Below that, the
math is mostly altitude noise, and a delta that swings wildly in
the first seconds of a run teaches you to ignore it.

## Going live: racing while you ski

The replay version of ghost racing came first; the live version is
the same mathematics on a stricter budget. While you're descending,
the app re-runs the piste matcher every eight or so GPS fixes — often
enough to catch the moment the named run becomes identifiable,
rare enough that the matcher isn't re-running on every single fix.
The moment a name lands, the app looks up your fastest full attempt
on it and the race card appears: run name, your best time, and the
live delta ticking at each fix.

If it's a run you've never recorded, the card says so — "first
descent on record, setting the time to beat" — which turns even an
unraced run into a stake in the ground.

## The chase camera

In the replay, the ghost is drawn as a second dot on real 3D terrain,
and pressing play sends a camera flying down the mountain behind
your marker. The hard part of a chase camera is heading, not
position: phone GPS is typically good to
[about 4.9 m under open sky](https://www.gps.gov/gps-accuracy), so a
bearing drawn between nearby fixes swings with every
fix's error, and a camera that follows it whips the world around.
The fix is an exponential moving average on the bearing — with the
wrap-around at 360° handled, which is the easy detail to miss —
so the camera banks through turns like a drone operator with lazy
wrists rather than a startled bird.

## What we deliberately didn't build

No leaderboards against strangers. Partly philosophy: public ski
leaderboards turn crowded pistes into race tracks, and the person
you'd beat was a nine-year-old in a lesson group. Partly
architecture: Alpy has no server, so there is nowhere a stranger's
time could live. Your ghosts are yours, on your phone.

And no rankings between different runs — a PR on a motorway blue and
a PR on a mogul black are both just PRs. The app measures; it
doesn't grade your taste in terrain.

The result is a racing feature with one opponent, who happens to be
the only one whose defeat means anything: you, last time.

*Ghost racing is free in Alpy — live on the mountain and in the 3D
replay. [How the app compares to others](/compare/) ·
[More engineering posts](/blog/).*
