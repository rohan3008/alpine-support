---
title: "Counting ski turns from GPS: an honest estimate"
description: "How a phone estimates turns from heading swings, why the number has a tilde in front of it, and what turn cadence says about fatigue."
---

# Counting ski turns from GPS: an honest estimate

Alpy's debrief shows "~14 turns" for a run — and that tilde is doing
real work. Here's how a phone counts turns, and why any app showing
you a turn count *without* a tilde is overselling its data.

## The method

A GPS track is a chain of fixes, each with a heading. Skiing linked
turns swings that heading left-right-left in a rhythm, so the app
watches for sustained heading swings past a threshold (Alpy uses 30°
with hysteresis, so jitter doesn't double-count) and calls each full
swing a turn. Carved GS arcs, skidded snow-plough, snowboard turns —
the physics read the same.

What the method can't see: short-radius turns inside the distance
between two GPS fixes. A phone logs a fix roughly every second at
~10 m intervals at speed. Tight slalom turns at 1-per-second blur
together; the estimate reads low. That's why it's "~14," never "14."

## Why bother with an imperfect count?

Because the *trend* is more honest than the number. Turn cadence —
turns per minute, run by run — barely cares about absolute accuracy:
if the method undercounts consistently, the day's curve still shows
the real pattern. Alpy plots exactly that as a Day Rhythm chart, and
with four or more comparable runs it will tell you your cadence faded
22% from the morning — the legs knew before you did. (With three runs
it refuses to claim a trend; small samples make confident liars.)

Estimates are fine instruments as long as they're labeled. The
failure mode isn't imprecision — it's precision theater.

*Turn estimates, cadence and the day debrief are free in Alpy.
[About](/).*
