---
title: "Why our trail maps are drawn, not painted"
description: "Why ski apps can't bundle resort panorama art, what OpenStreetMap geometry offers instead, and how Alpy draws a mountain twice: chart and 3D terrain."
---

# Why our trail maps are drawn, not painted

The trail map in your jacket pocket is a painting, and usually a
magnificent one. Resorts commission panorama artists to compress a
three-dimensional mountain onto one sheet; James Niehues has described
[manipulating the features to show the back side with the front](https://www.maproomblog.com/2021/01/atlas-obscura-interviews-james-niehues/),
so that every lift and run faces the viewer at once. The greatest
practitioners painted hundreds of maps each: Niehues
[255 maps for 175 resorts by 2016](https://en.wikipedia.org/wiki/James_Niehues),
and Pierre Novat in France
[more than 250 over a 35-year career](https://export.side.fr/en/9782723495431-plans-des-pistes).
People love this work. Niehues' was shown in a 2011 exhibition at
Apexart in New York.

## Why can't a free ski app use the resort's trail map?

Because resort trail maps are
[copyrighted](https://www.wipo.int/treaties/en/ip/berne/summary_berne.html)
artwork, and they're distorted on purpose. A free app with no revenue
can't license hundreds of paintings, and shouldn't pretend otherwise.

The distortion is the art. A panorama is *gloriously* bent. It's a
diagram of an argument ("here is how our mountain fits together"),
and you couldn't navigate by bearing and distance on it.

So Alpy had the choice every small ski app faces. It could fake it
with sketchy clones of someone else's art (honestly worse), skip
trail maps entirely, or find a third way.

## Where does Alpy's trail map data come from?

From OpenStreetMap. Its contributors map ski areas: marked pistes as
coordinate chains with a name and
[difficulty](https://wiki.openstreetmap.org/wiki/Pistes), lifts with
their stations, area boundaries. The geometry is real. Contributors
[use aerial imagery, GPS devices and field maps](https://www.openstreetmap.org/about)
to keep it accurate, nothing is bent for a viewpoint, and it's open
data under the
[ODbL license](https://www.openstreetmap.org/copyright).
Zermatt's map in Alpy carries 126 km of piste geometry; across OSM we
count 3,652 named winter-sports areas worldwide.

Real geometry lets an app do things a painting never could: draw your
live position *on* the network, match your GPS line to a named run,
and measure piste kilometres honestly. The cost is visual. Raw OSM
rendering looks like engineering output and nothing like a mountain,
so we designed our own cartography on top of it, twice.

## Rendering one mountain two ways

The schematic chart is Alpy's homage to the paper map's *spirit*
without copying anyone's painting. It draws the real OSM network as a
clean diagram on a warm paper ground, with runs colour-coded by
difficulty in the European convention, lifts as dashed lines with
terminal dots, and the longest named descents labelled in small
haloed capitals. North is up and the geometry is true. For catalog
resorts it ships inside the app, so it loads instantly. It reads at
arm's length in glare and gloves, and while you're tracking, a small
red dot on it is *you*, which no printed map can show.

The 3D terrain view goes the other way: the same piste network draped
over real elevation data with relief shading, free to pitch and
rotate. The painting's job of letting you feel how the mountain fits
together gets done here by actual terrain instead of artistic license.
It's also where your day replays, with your recorded line drawn down
the real mountain, a chase camera flying behind your marker, and your
ghost alongside.

So the chart is for orientation and planning, and the terrain is for
understanding and reliving the day. A painting tries to be both at
once, which is exactly why it has to bend the mountain.

## Honesty, credits, and etiquette

We follow three rules here. OSM data is credited on-screen and in the
App Store listing, because ODbL
[asks for that credit](https://www.openstreetmap.org/copyright) and
the mappers deserve their line. Where OSM is thin, Alpy shows what
exists and says the layout may be incomplete instead of making up
runs, and anyone can fix the source by mapping, which improves every
OSM-based app at once. And while catalog resorts' piste maps ship
inside the app, any other area's map is fetched once and cached for
thirty days. The public
[Overpass servers](https://wiki.openstreetmap.org/wiki/Overpass_API)
that answer these queries (the main instance is operated by FOSSGIS)
publish a usage policy that says "cache and rate-limit calls". They're
shared infrastructure, and we treat them that way.

The painted panorama does its job beautifully in a chairlift pocket.
A phone also knows where you are, where you've been and how fast you
went, and using that needs a map whose geometry is *true*. We'll take
true, and make it as handsome as we can.

*Both map views are free in Alpy for 3,652 OSM ski areas: 3D terrain
by default, the schematic chart one tap away, and your live position
on the chart while you track. [The app](/) ·
[More from the blog](/blog/).*
