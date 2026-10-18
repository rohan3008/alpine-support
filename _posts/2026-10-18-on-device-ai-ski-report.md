---
title: "On-device AI for skiers: a morning report that never phones home"
description: "How Alpy uses Apple's on-device foundation model to write morning reports and day summaries — and the never-invent rule that keeps the AI honest."
---

# On-device AI for skiers: a morning report that never phones home

Since 2025, iPhones with Apple Intelligence carry a capable language
model *on the device*. For an app like Alpy this changes the AI
trade entirely: prose quality without a cloud bill, an API key, or a
single byte of your data leaving the phone.

## What the model is allowed to do

Alpy uses on-device AI in two places: the **morning report** (a few
sentences turning today's measured conditions into plain language)
and **"The Day, Written"** (an end-of-day paragraph in your debrief).

Both run under the same contract we'd give a careful human editor:
*rephrase the telemetry, never invent.* The model receives only
measured facts — temperatures, fresh snow, your run times, your PRs,
your cadence trend — with explicit instructions to add nothing. Facts
that don't exist for the day are omitted from the prompt entirely, so
the model can't even be tempted to mention airtime on a day without
airs. Small on-device models hallucinate more readily than frontier
cloud models, which is why we don't ask this one for world knowledge
— no "best runs at Verbier" from a model that might make them up.

## Labels, always

Every AI-written paragraph in Alpy carries a chip saying who wrote
it: **ON-DEVICE AI** when Apple's model is available, **AUTO
SUMMARY** when an older phone falls back to our deterministic
template. Same information either way; different voice; always
disclosed. AI output is never a safety source — bulletins and weather
stay verbatim from their official providers.

That's the whole architecture: AI as a writer, instruments as the
source of truth, and nothing leaving the phone. The 2026 version of
"no cloud" isn't anti-AI — it's AI that moved in with you.

*Alpy is free, with all AI on-device.
[Privacy policy](/privacy).*
