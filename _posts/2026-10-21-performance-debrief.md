---
title: "The Day, Written: a coach's debrief from your own numbers"
description: "Alpy's end-of-day summary reads like a coach reviewing the data — descent rate, time on snow, the standout run, records, consistency — written on-device and never allowed to invent a number."
---

# The Day, Written: a coach's debrief from your own numbers

<p align="center"><img src="/assets/screens/alpy-ski-debrief.png" alt="The Day, Written: an on-device AI performance summary above the run registers" width="280" style="border-radius:22px; border:1px solid #d0d7de; box-shadow:0 8px 24px rgba(10,17,31,.15);" loading="lazy"></p>


The end of a ski day produces a pile of numbers. Most apps show you
the pile. Alpy also *reads* it to you — a short paragraph in the
voice of a coach going over the data, built from athletic measures
that actually say something:

- **Descent rate** — vertical meters per hour *of descending*, the
  cleanest "how hard did I ski" number there is.
- **Time on snow** — how much of your mountain day was actually spent
  descending ("41 min descending across a 3 h 12 m day" is a very
  normal, very clarifying ratio).
- **The standout run** — your fastest average descent, with its drop,
  time and speed.
- **Records** — personal bests on named runs, with the margin you
  beat them by.
- **Consistency** — how tightly your per-run top speeds grouped.
- **Conditioning** — whether your turn cadence held, rose, or faded
  across the day.
- **Load** — airtime and peak turn G from the accelerometer, always
  labeled as the estimates they are.

## The one rule: never invent

The paragraph is written by Apple's on-device model when your iPhone
has one, and by a deterministic template when it doesn't — the card
labels which voice you're reading. Both voices live under the same
contract: **use only the measured facts provided; never invent
conditions, snow, places, feelings, or numbers.** Facts your day
didn't produce are omitted entirely rather than padded around. If you
set no records, the word doesn't appear.

This matters because AI summaries drift toward flattery and filler.
Ours can't: the prompt hands the model a fixed set of measured
sentences and the job of making them read well — a rephraser, not an
author. When the model isn't available, the template assembles the
same facts in the same register, so the debrief never silently
changes meaning with the hardware.

## Why "athletic" framing

Early versions of this feature read like a diary — pleasant,
forgettable. The rewrite treats your day the way a coach treats a
training log: work done first, quality second, trend third. Skiing
is a sport; your data deserves the sport's vocabulary.

And because everything is computed on the phone from your own GPS and
motion sensors, the debrief arrives with the same privacy as the rest
of [Alpy](../): no account, no server, nothing uploaded.

*The Day, Written sits at the top of every Ski Debrief. For what the
rest of the debrief holds — per-run registers, lift lines, records —
start with [a first day with Alpy](first-day-with-alpy/).*
