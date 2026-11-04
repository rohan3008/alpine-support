---
title: "The Day, Written: a coach's debrief from your own numbers"
description: "Alpy's end-of-day summary reads like a coach reviewing your data — descent rate, standout run, consistency — written on-device, never inventing a number."
---

# The Day, Written: a coach's debrief from your own numbers

<p align="center"><img src="/assets/screens/alpy-ski-debrief.png" alt="The Day, Written: an on-device AI performance summary above the run registers" width="280" style="border-radius:22px; border:1px solid #d0d7de; box-shadow:0 8px 24px rgba(10,17,31,.15);" loading="lazy"></p>


The end of a ski day produces a pile of numbers. Most apps show you
the pile. Alpy also *reads* it to you — a short paragraph in the
voice of a coach going over the data, built from athletic measures
that actually say something:

- **Descent rate** — vertical meters per hour *of descending*, to us
  the clearest "how hard did I ski" number.
- **Time on snow** — how much of your mountain day was actually spent
  descending (for example, "41 min descending across a 3 h 12 m
  day").
- **The standout run** — the run with your highest average speed,
  with its drop, time and speed.
- **Records** — personal bests on named runs, with the margin you
  beat them by.
- **Consistency** — how tightly your per-run top speeds grouped.
- **Conditioning** — whether your turn cadence held, rose, or faded
  across the day.
- **Load** — airtime and peak turn G from the accelerometer, always
  labeled as the estimates they are.

## Can an AI ski summary make up numbers?

It's built not to. The paragraph is written by Apple's
[on-device model](https://developer.apple.com/documentation/foundationmodels/systemlanguagemodel)
when your iPhone has one, and by a deterministic template when it
doesn't — the card labels which voice you're reading. The model's
instructions are the contract: **use only the facts provided; never
invent conditions, snow, weather, places, people, technique advice
or feelings; do not add numbers that are not given.** The template
can only print the facts it is handed.

Facts your day didn't produce are omitted entirely rather than padded around. If you
set no records, no record line is in the prompt or the template.

We didn't want flattery or filler, so the prompt hands the model a
fixed set of measured sentences and the job of making them read
well — a rephraser, not an author. When the model isn't available,
the template assembles the same facts in the same register, so the
facts you're given don't change with the hardware.

## Why "athletic" framing

Early versions of this feature read like a diary — pleasant,
forgettable. The rewrite treats your day the way a coach treats a
training log: work done first, quality second, trend third. Skiing
is a sport; your data deserves the sport's vocabulary.

And because everything is computed on the phone from your own GPS and
motion sensors, the debrief arrives with the same privacy as the rest
of [Alpy](/): no account, no server, nothing uploaded.

*The Day, Written sits at the top of every Ski Debrief. For what the
rest of the debrief holds — per-run registers, lift lines, records —
start with [a first day with Alpy](/blog/first-day-with-alpy/).*
