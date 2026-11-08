---
title: "How we built ghost racing for skiing: the engineering notes"
description: "How Alpy turns OpenStreetMap pistes into segments, handles partial descents, computes F1-style deltas and races your ghost live on the mountain."
---

# How we built ghost racing for skiing: the engineering notes

Alpy lets you race a ghost of yourself down a ski run, live on the
mountain, with an F1-style time delta ticking on your screen. This
post covers the engineering: what made it hard, what we got wrong,
and the four or five small decisions that keep the feature honest.
It's written for people who like knowing how their instruments work,
and you don't need to read code to follow it.

## The problem: ski runs don't have finish lines

Strava's [Live Segments](https://support.strava.com/hc/en-us/articles/207343830-Live-Segments)
race a ride or run against your PR on a segment, a stretch of road
or trail you enter and complete. A ski run is a wide ribbon of snow
with no single line through it. Two descents of the same piste never
trace the same GPS line, never start at the same point, and often
end in different places: one pulls up at the lift, the other carries
on to the restaurant.

So the first decision is what a "segment" even is. We settled on a
named piste in OpenStreetMap. OSM contributors have mapped ski runs
as coordinate chains, tagged with names and
[difficulties](https://wiki.openstreetmap.org/wiki/Key:piste:difficulty).
If we can tell which named run a descent happened on, each descent
becomes an *attempt* on that run, and the record book follows from
there.

## How does Alpy know which run you skied?

By majority vote. Take every GPS fix in a descent and ask, for each
one, which named piste's geometry passes within a 40-metre corridor
of this point. Whichever run claims the majority of the points claims
the descent.

The corridor absorbs both GPS error and the width of a real piste.
The majority rule stops a run from being claimed by a piste you
merely crossed at an intersection.

What happens when *nothing* claims the points matters just as much.
The descent stays unnamed. Off-piste lines, unnamed connector tracks
and resort areas OSM hasn't mapped all show up as "Unnamed line", and
those descents never enter the record book. We considered snapping
unnamed descents to the nearest run and decided against it, because
an instrument that guesses is worse than one that admits it doesn't
know.

## How do you stop half a run from setting a record?

With what we call the full-drop rule. For every segment we track the
deepest vertical drop any attempt has recorded, and an attempt only
competes for records if its own drop is at least 80% of that.
Anything under the line is marked *partial*: it stays in your history
and sits out the race.

We needed it fast. The first version of the record book had an
exploit we found quickly: bail out halfway down a run and you'd post
an unbeatable "record", because half a run takes half the time. Any
skier would spot the cheat instantly, so the code had to as well. The
threshold is deliberately forgiving, and 80% is our judgement call;
we didn't measure it. Altitude noise and different pull-out points
shave drop off honest runs, and a rule that disqualified them would
be worse than the exploit.

One subtlety: the "deepest drop" baseline is computed across all
attempts *including today's*, so the first time you ski the full
run, it resets the bar for what "full" means.

## How do you compare two ski runs that took different lines?

By vertical drop. You compare the two runs at the same depth below
the start: when you've dropped 180 m, how long had the ghost taken to
drop 180 m? The difference in time is your delta, and it holds up
even when the two runs took different lines down the same piste.

This was the most interesting problem in the feature. Say you're
forty seconds into today's descent. Your PR took a different line: it
entered three metres higher and swung wider at the second pitch.
"Where was the ghost at forty seconds?" is easy to answer and useless
to display, because position isn't progress. The ghost might be ahead
on the clock and behind on the mountain.

Vertical drop works as the comparison axis because descent is
monotone. You can traverse, but the cumulative drop of a run only
grows, so "how many metres below the start am I?" is a progress bar
that works for any line down the same mountain. We store every
attempt's *descent profile* (elapsed time against cumulative drop),
clamped monotone so altitude wobble can't make the curve dip
backwards.

The delta is then an inverse lookup. I've dropped 180 m in 40 s, so
when did the ghost pass 180 m? If the ghost needed 43 s, you're
−3.0 s up. Comparing at equal progress instead of equal time is what
keeps the delta sensible when the two runs take different lines,
since both runs cover the same metres of mountain.

The chip stays silent for the first 10 m of drop. Before that, the
math is mostly altitude noise, and a delta that swings wildly in the
first seconds of a run teaches you to ignore it.

## Going live: racing while you ski

The replay version of ghost racing came first. The live version is
the same mathematics on a stricter budget. While you're descending,
the app re-runs the piste matcher every eight or so GPS fixes, which
is often enough to catch the moment the named run becomes
identifiable without running the matcher on every single fix. Once a
name lands, the app looks up your fastest full attempt on it and the
race card appears with the run name, your best time, and the live
delta ticking at each fix.

If it's a run you've never recorded, the card says so ("first
descent on record, setting the time to beat"), so even an unraced run
gets a time on the board.

## The chase camera

In the replay, the ghost is drawn as a second dot on real 3D terrain,
and pressing play sends a camera flying down the mountain behind your
marker. Heading is the hard part of a chase camera. Phone GPS is
typically good to
[about 4.9 m under open sky](https://www.gps.gov/gps-accuracy), so a
bearing drawn between nearby fixes swings with every fix's error, and
a camera that follows it whips the world around. We smooth the
bearing with an exponential moving average and handle the wrap-around
at 360° (the easy detail to miss). The camera then banks through
turns like a drone operator with lazy wrists instead of a startled
bird.

## What we deliberately didn't build

No leaderboards against strangers. Part of that is philosophy: public
ski leaderboards turn crowded pistes into race tracks, and the person
you'd beat was a nine-year-old in a lesson group. Part is
architecture: Alpy has no server, so there is nowhere a stranger's
time could live. Your ghosts stay on your phone, and the one opponent
you race is you, last time.

There are no rankings between different runs either. A PR on a
motorway blue and a PR on a mogul black are both just PRs. The app
measures your times and leaves your taste in terrain alone.

*Ghost racing is free in Alpy, live on the mountain and in the 3D
replay. [How the app compares to others](/compare/) ·
[More engineering posts](/blog/).*
