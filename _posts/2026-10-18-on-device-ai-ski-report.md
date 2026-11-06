---
title: "On-device AI for skiers: a morning report that never phones home"
description: "How Alpy uses Apple's on-device foundation model to write morning reports and day summaries — and the never-invent rule that keeps the AI honest."
---

# On-device AI for skiers: a morning report that never phones home

iPhones that support Apple Intelligence carry a language model *on
the device* that apps can use through Apple's
[Foundation Models framework](https://developer.apple.com/documentation/foundationmodels/systemlanguagemodel).
Apple
[says](https://www.apple.com/newsroom/2025/09/apples-foundation-models-framework-unlocks-new-intelligent-app-experiences/)
the inference is free, private and available offline, on any
Apple Intelligence-compatible device with Apple Intelligence turned
on. For an app like Alpy this changes the AI trade entirely: prose
quality without a cloud bill, an API key, or a single byte of your
data leaving the phone.

## What does on-device AI do in a ski app?

In Alpy, it writes — and only writes. Apple's on-device model turns
measured numbers into plain sentences: a morning report from today's
conditions and an end-of-day paragraph from your runs. Its
instructions forbid inventing facts or adding numbers it wasn't
given, and every paragraph it writes is labeled as AI.

Alpy uses on-device AI in two places: the **morning report** (a few
sentences turning today's measured conditions into plain language)
and **"The Day, Written"** (an end-of-day paragraph in your debrief).

Both run under the same contract we'd give a careful human editor:
*rephrase the telemetry, never invent.* The model receives only
measured facts — temperatures, fresh snow, your run times, your PRs,
your cadence trend — plus, for the morning report, the avalanche
bulletin's own text, with explicit instructions to add nothing. In
the day summary, facts that don't exist for the day are omitted from
the prompt entirely, so the model is never handed airtime to mention
on a day without airs. Apple's own
[guide to the on-device model](https://developer.apple.com/documentation/foundationmodels/generating-content-and-performing-tasks-with-foundation-models)
points tasks that need extensive world knowledge at extra tools, so
we don't ask it for world knowledge at all — no "best runs at
Verbier" from a model that might make them up.

One exception, so nobody is surprised: the resort guides on the
Resort tab (a resort's character, run picks, food and après) were
written ahead of time by a cloud model, Anthropic's Claude, from its
general knowledge, and ship inside the app. Each one is labeled with
the model and the month it was written, plus a warning that names
can drift, so check runs on the trail map. Nothing in the app
contacts an AI service while you use it.

## How do you know when a ski report was written by AI?

Every AI-written paragraph in Alpy is labeled, and the two on-device
ones carry a chip saying who wrote them: **ON-DEVICE AI** when
Apple's model is available, **AUTO** (on
the morning report) or **AUTO SUMMARY** (on the debrief) when the
phone falls back to our deterministic template. Same measured
inputs either way; different voice; always disclosed. AI output is never
the safety source — the bulletin's danger level and the weather
numbers are shown as their providers publish them, above the prose.

That's the whole architecture: AI as a writer, instruments as the
source of truth, and nothing leaving the phone. The 2026 version of
"no cloud" isn't anti-AI — it's AI that moved in with you.

*Alpy is free, and the AI that runs in the app runs on your phone.
[Privacy policy](/privacy/).*
