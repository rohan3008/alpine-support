---
title: "Why our trail maps are drawn, not painted"
description: "The strange world of ski resort panorama art, why apps can't just bundle it, what OpenStreetMap geometry offers instead — and how Alpy renders a mountain twice: schematic chart and 3D terrain."
---

# Why our trail maps are drawn, not painted

The trail map in your jacket pocket is a painting. Not a map in the
cartographic sense — a *painting*, and usually a magnificent one.
For half a century, resorts have commissioned panorama artists to
compress a three-dimensional mountain onto one sheet: entire
massifs bent around sightlines that don't exist, valleys widened,
peaks rotated, so that every lift and run faces the viewer at once.
The greatest practitioners — James Niehues in North America,
Pierre Novat in France — painted hundreds of resorts each, and
their work is genuinely beloved; Niehues' maps have hung in art
museums.

Two things follow from trail maps being art. First: they're
*gloriously* distorted. A panorama is a diagram of an argument
("here is how our mountain fits together"), not a chart you could
navigate by bearing and distance. Second, and decisive for an app:
they're copyrighted artwork, commissioned and owned. A subscription
ski app can license them; a free app with no revenue cannot bundle
hundreds of paintings, and shouldn't pretend otherwise.

So Alpy had a choice every small ski app faces: fake it (sketchy
clones of resort art — legally gray, honestly worse), skip trail
maps entirely, or find a third way.

## The commons had already mapped the mountain

OpenStreetMap contributors have spent two decades mapping ski
areas: every marked piste as a coordinate chain with a name and
difficulty, every lift with its stations, refuges, area boundaries.
The geometry is *real* — surveyed from GPS traces and imagery, not
bent for a viewpoint — and it's open data under the ODbL license.
Zermatt alone carries 134 km of named piste geometry; across OSM
we count 3,652 named ski areas worldwide.

Real geometry means an app can do things a painting never could:
draw your live position *on* the network, match your GPS line to a
named run, measure piste kilometres honestly. The trade is visual:
raw OSM rendering looks like engineering output, not a mountain.
The answer was to design our own cartography on top of it — twice.

## Rendering one mountain two ways

**The schematic chart** is Alpy's homage to the paper map's
*spirit* without copying anyone's painting: the real OSM network
drawn as a clean diagram on a warm paper ground — runs colour-coded
by difficulty in the European convention, lifts as dashed lines
with terminal dots, the longest named descents labelled in small
haloed capitals. North is simply up; geometry is simply true. It
loads instantly, reads at arm's length in glare and gloves, and
while you're tracking, a small red dot on it is *you* — the one
feature every paper map has lacked since 1936.

**The 3D terrain view** goes the other direction: the same piste
network draped over real satellite imagery and elevation, free to
pitch and rotate. This is where a painting's job — "feel how the
mountain fits together" — gets done by actual terrain instead of
artistic license. It's also where your day replays: your recorded
line drawn down the real mountain, a chase camera flying behind
your marker, your ghost alongside.

Chart for orientation and planning; terrain for understanding and
reliving. A painting tries to be both at once, which is exactly why
it has to bend the mountain.

## Honesty, credits, and etiquette

Three rules keep the system clean. **Credit:** OSM data is credited
on-screen and in the listing — ODbL isn't just a legal license,
it's two decades of volunteers who deserve their line. **No
guessing:** where OSM is thin (notably parts of Japan, where famous
resorts carry unexpected tags), Alpy shows what exists and says so,
rather than hallucinating runs — and anyone can fix the source by
mapping, which improves every OSM-based app at once. **Etiquette:**
piste geometry is fetched once and cached for thirty days per
resort, because the Overpass servers that answer these queries are
volunteer-run infrastructure, not a free CDN.

The painted panorama isn't the enemy — it's a beautiful solved
problem for the chairlift pocket. But a phone knows where you are,
where you've been, and how fast you went, and honoring that takes a
map that's *true* rather than merely gorgeous. We'll take true, and
make it as handsome as we can.

*Both map views are free in Alpy for 3,652 OSM ski areas —
schematic chart by default, 3D one tap away, your position live on
both. [The app](/) · [More from the blog](/blog/).*
