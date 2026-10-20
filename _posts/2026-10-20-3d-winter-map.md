---
title: "How Alpy got a real 3D winter mountain"
description: "A build log: why the paper chart wasn't enough, why we left MapKit for the 3D view, the one-line styling bug that ate our relief shading, and what a winter terrain map costs in memory and privacy."
---

# How Alpy got a real 3D winter mountain

Alpy has always drawn its own piste maps. The resorts' beautiful painted
panoramas — the Niehues school of hand-drawn mountains — are commissioned
artwork we can't bundle, and they're geometrically distorted on purpose,
so you can't drape them over real terrain either. Our answer was a clean
paper chart: the resort's real OpenStreetMap network, colored by
difficulty, drawn by us. Honest, readable, flat.

The flatness was the complaint. Skiers don't think of a mountain as a
diagram; they think of it the way FATMAP and the lift-line poster show
it — terrain you can read, with the runs lying on it. We tried to get
there with Apple's MapKit first, and we want to be precise about where
that ceiling is, because we hit it in public over several builds:
satellite imagery looks spectacular from far away and turns to summer
mud up close; the vector map stays clean but reads like a road atlas.
There is no setting in between. The apps whose 3D mountains you admire
are not using MapKit for them.

So we did what they do: Mapbox.

## What the terrain is actually made of

The 3D view is four layers, and every one of them is checkable:

- **Elevation.** Mapbox's global terrain model (a raster DEM), with a
  gentle 1.3× vertical exaggeration — enough to read a valley at a
  glance, not enough to lie about a slope.
- **Relief shading and contours** from the base style.
- **The piste network** — the same OpenStreetMap data our paper chart
  uses, encoded as GeoJSON line layers: a white casing under
  difficulty-colored lines, dashed lifts, and run names set *along the
  lines* the way a cartographer would place them. At Zermatt that's 134
  km of pistes, drawn from the same source you can edit yourself on
  openstreetmap.org.
- **Winter.** The base style is a summer hiking map, so at load time we
  restyle it: every land fill becomes snowpack white, water keeps its
  blue, and the relief does the rest.

## The bug worth blogging about

That last step ate an afternoon, and the lesson generalizes.

Our first "winter" pass turned the whole mountain flat. The relief
shading had vanished — and boosting the hillshade layer's strength did
nothing at all. Three styling iterations went nowhere until we stopped
guessing and printed the style's actual layer stack.

The answer: in Mapbox's outdoors style, the layer named `hillshade`
isn't a hillshade layer at all. It's a **fill layer of pre-computed
shadow polygons**, and its color is an *expression* that varies by
illumination class — highlight polygons render near-invisible, shadow
polygons render dark. Our blanket "make every fill white" rule had been
painting the shadows themselves white. And when we tried tinting the
layer a constant alpine blue instead, every polygon — including the
should-be-invisible highlights — flooded the same solid color.

The fix was to leave that one layer completely alone. Over white snow,
its own shading reads like a paper relief map, which was the look we
wanted all along. Two rules we're keeping: *print the layer stack
before styling anything*, and *a layer whose paint is driven by an
expression can't safely take a constant.*

## The replay rides the same mountain

Day Replay — the chase-cam playback of your ski day — now runs on the
same winter terrain. The port was deliberately boring: all the replay
logic (the scrub clock, the smoothed chase heading, the ghost-skier
interpolation) stayed where it was already tested, and the new map is a
dumb renderer that receives positions each frame. Per tick it updates
two one-point geometry sources and moves the camera; the day's line,
the lifts, and the matched piste upload once. Boring ports are the ones
that work on the first compile.

## What it costs, honestly

**Memory.** A 3D terrain engine is not free, and we treated that as a
feature requirement: the map views are torn down properly on dismissal
(one retain cycle involving a display-link timer was found and fixed —
if you build with `CADisplayLink`, remember it retains its target, so
cleanup can never live in `deinit`), and the small terrain preview on
the home tab is now a generated *still image* rather than a live map
engine idling in the background for the whole app session.

**Privacy.** Map tiles necessarily come from Mapbox's servers — those
requests carry the map area being viewed, and that's now stated in our
privacy policy. Mapbox's telemetry collection is switched off using the
SDK's own opt-out setting, and the ⓘ attribution button stays on the
map, both because Mapbox's terms require it and because that dialog is
the user-facing opt-out control. Everything else about Alpy is
unchanged: no server of ours, no accounts, no analytics, GPS tracks
never leave the phone.

**The paper chart stays.** One tap toggles back to it. Some days you
want the mountain; some days you want the diagram. We like both, and
now neither is pretending to be the other.

---

*Alpy is a free ski app for iPhone with honest instruments: GPS day
tracking, personal records on real named runs, ghost racing, and an
on-device AI debrief. Nothing you do in it leaves your phone.*
