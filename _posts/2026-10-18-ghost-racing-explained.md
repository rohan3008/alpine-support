---
title: "Ghost racing: racing yourself down a ski run"
description: "How Alpy turns every named piste into a segment and lets you race your own fastest descent — live on the mountain and in a 3D replay."
---

# Ghost racing: racing yourself down a ski run

Video games solved motivation decades ago: the *ghost* — a replay of
your best lap driving alongside you. Cycling and running apps
borrowed it (Strava's Live Segments is the famous one). Skiing never
really got it, because ski runs don't have start gates and finish
lines.

Except they do: OpenStreetMap maps the world's pistes by name. If an
app can tell which named run you're descending, every run becomes a
segment — and your own history becomes the ghost.

## How Alpy builds a ghost

When you ski a named run, Alpy matches your GPS line against the OSM
piste network (a majority vote inside a 40 m corridor — off-piste
honestly matches nothing). Ski the same run again and the app finds
your fastest *full* previous descent and races you against it:

- **Live, while skiing:** a race card appears with an F1-style gap
  that ticks in real time — green **−1.2 s** when you're up on
  yourself, red **+0.8 s** when the ghost is ahead.
- **In the replay:** your best descent is drawn as a second dot on
  real 3D terrain, running beside today's line.

## The honesty rules

Two guards keep the racing fair. A **partial descent never races a
full one** — bailing halfway down in half the time isn't a record, so
any attempt under 80% of the segment's deepest recorded drop is
marked partial and excluded. And the gap is computed by *vertical
progress*, not clock time at a position: the question is "when did
the ghost reach the depth I'm at now?", which works even though no
two GPS lines down a piste are identical.

There's no leaderboard against strangers and no server keeping score.
It's you against who you were — which, on the fourth run of the day
with your legs going, turns out to be the only race that matters.

*Ghost racing is free in Alpy, like everything else.
[How it compares to other ski apps](/compare).*
