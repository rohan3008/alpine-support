---
title: "Why our trail maps are drawn, not painted"
description: "Why ski apps can't bundle resort panorama art, what OpenStreetMap geometry offers instead, and how Alpy draws a mountain twice: chart and 3D terrain."
---

# Why our trail maps are drawn, not painted

The trail map in your jacket pocket is a painting. Not a map in the
cartographic sense — a *painting*, and usually a magnificent one.
Resorts commission panorama artists to compress a three-dimensional
mountain onto one sheet; James Niehues has described
[manipulating the features to show the back side with the front](https://www.maproomblog.com/2021/01/atlas-obscura-interviews-james-niehues/),
so that every lift and run faces the viewer at once. The greatest
practitioners painted hundreds of maps each — Niehues
[255 maps for 175 resorts by 2016](https://en.wikipedia.org/wiki/James_Niehues),
Pierre Novat in France
[more than 250 over a 35-year career](https://export.side.fr/en/9782723495431-plans-des-pistes)
— and their work is genuinely beloved; Niehues' was shown in a 2011
exhibition at Apexart in New York.

## Why can't a free ski app use the resort's trail map?

Because resort trail maps are
[copyrighted](https://www.wipo.int/treaties/en/ip/berne/summary_berne.html)
artwork — and they're distorted on purpose. A free app with no
revenue can't license hundreds of paintings, and shouldn't pretend
otherwise.

The distortion is the art. A panorama is *gloriously* bent — a
diagram of an argument ("here is how our mountain fits together"),
not a chart you could navigate by bearing and distance.

So Alpy had a choice every small ski app faces: fake it (sketchy
clones of someone else's art — honestly worse), skip trail
maps entirely, or find a third way.

## Where does Alpy's trail map data come from?

From OpenStreetMap. Its contributors map ski areas: marked pistes
as coordinate chains with a name and
[difficulty](https://wiki.openstreetmap.org/wiki/Pistes), lifts
with their stations, area boundaries. The geometry is *real* —
contributors [use aerial imagery, GPS devices and field maps](https://www.openstreetmap.org/about)
to keep it accurate, and nothing is bent for a viewpoint — and
it's open data under the
[ODbL license](https://www.openstreetmap.org/copyright).
Zermatt's map in Alpy carries 126 km of piste geometry; across OSM
we count 3,652 named winter-sports areas worldwide.

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
haloed capitals. North is simply up; geometry is simply true. For
catalog resorts it ships inside the app, so it loads instantly; it
reads at arm's length in glare and gloves, and while you're
tracking, a small red dot on it is *you* — something no printed
map can show.

**The 3D terrain view** goes the other direction: the same piste
network draped over real elevation data with relief shading, free
to pitch and rotate. This is where a painting's job — "feel how the
mountain fits together" — gets done by actual terrain instead of
artistic license. It's also where your day replays: your recorded
line drawn down the real mountain, a chase camera flying behind
your marker, your ghost alongside.

Chart for orientation and planning; terrain for understanding and
reliving. A painting tries to be both at once, which is exactly why
it has to bend the mountain.

## Honesty, credits, and etiquette

Three rules keep the system clean. **Credit:** OSM data is credited
on-screen and in the App Store listing — ODbL
[asks for that credit](https://www.openstreetmap.org/copyright), and
the mappers deserve their line. **No guessing:** where OSM is thin,
Alpy shows what exists and says the layout may be incomplete,
rather than hallucinating runs — and anyone can fix the source by
mapping, which improves every OSM-based app at once. **Etiquette:**
catalog resorts' piste maps ship inside the app; any other area's
map is fetched once and cached for thirty days, because the public
[Overpass servers](https://wiki.openstreetmap.org/wiki/Overpass_API)
that answer these queries (the main instance is operated by
FOSSGIS) publish a usage policy that says "cache and rate-limit
calls" — shared infrastructure, not a free CDN.

The painted panorama isn't the enemy — it's a beautiful solved
problem for the chairlift pocket. But a phone knows where you are,
where you've been, and how fast you went, and honoring that takes a
map that's *true* rather than merely gorgeous. We'll take true, and
make it as handsome as we can.

*Both map views are free in Alpy for 3,652 OSM ski areas —
3D terrain by default, the schematic chart one tap away, your live
position on the chart while you track. [The app](/) ·
[More from the blog](/blog/).*
