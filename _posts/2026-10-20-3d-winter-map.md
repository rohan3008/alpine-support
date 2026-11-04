---
title: "How Alpy got a real 3D winter mountain"
description: "Build log: why the paper chart wasn't enough, why we left MapKit for 3D, the styling bug that ate our relief shading, and the memory and privacy cost."
---

# How Alpy got a real 3D winter mountain

Alpy has always drawn its own piste maps. The resorts' beautiful painted
panoramas — the Niehues school of hand-drawn mountains — are commissioned
artwork we can't bundle, and they're
[geometrically distorted on purpose](/blog/drawn-not-painted-maps/),
so you can't drape them over real terrain either. Our answer was a clean
paper chart: the resort's real OpenStreetMap network, colored by
difficulty, drawn by us. Honest, readable, flat.

The flatness was the complaint. Skiers don't think of a mountain as a
diagram; they think of it the way the lift-line poster shows it —
terrain you can read, with the runs lying on it. We tried to get
there with Apple's MapKit first, and we want to be precise about where
we hit the ceiling, because we hit it in public over several builds:
in our tests, satellite imagery looked spectacular from far away and
turned to summer mud up close; the vector map stayed clean but read
like a road atlas. None of the styles we tried sat in between.

So we moved the 3D view to Mapbox.

## What is Alpy's 3D ski map made of?

Four layers, and every one of them is checkable: Mapbox's global
elevation model, relief shading and contours from Mapbox's outdoors
style, the resort's OpenStreetMap piste network drawn on top, and a
winter restyle that turns the base map snow-white at load time.

- **Elevation.** Mapbox's global terrain model (a
  [raster DEM](https://docs.mapbox.com/data/tilesets/reference/mapbox-terrain-dem-v1/)), with a
  gentle 1.3× vertical exaggeration — enough to read a valley at a
  glance, not enough to lie about a slope.
- **Relief shading and contours** from the base style.
- **The piste network** — the same OpenStreetMap data our paper chart
  uses, encoded as GeoJSON line layers: a white casing under
  difficulty-colored lines, dashed lifts, and run names set *along the
  lines* the way a cartographer would place them. At Zermatt that's 126
  km of pistes, drawn from the same source you can edit yourself on
  openstreetmap.org.
- **Winter.** The base style is Mapbox's general outdoors map, so at
  load time we restyle it: every land fill becomes snowpack white, water keeps its
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
two one-point geometry sources and moves the camera; the day's line
and lifts upload once, the matched piste and ghost line only when the
run changes. Boring ports are the ones
that work on the first compile.

## What does a 3D ski map cost in memory and privacy?

Two things: memory, and one privacy trade — map tiles come from
Mapbox's servers. We tear the map views down properly, render the
home-tab preview as a still image, switch Mapbox telemetry off, and
state the tile requests in the privacy policy. Your GPS tracks still
never leave the phone.

**Memory.** A 3D terrain engine is not free, and we treated that as a
feature requirement: the map views are torn down properly on dismissal
(one retain cycle involving a display-link timer was found and fixed —
if you build with `CADisplayLink`, remember
[it retains its target](https://developer.apple.com/documentation/quartzcore/cadisplaylink/init%28target:selector:%29), so
cleanup for a running link can't live in `deinit`), and the small terrain preview on
the home tab is now a generated *still image* rather than a live map
engine idling in the background for the whole app session.

**Privacy.** Map tiles necessarily come from Mapbox's servers — those
requests carry the map area being viewed, and that's now stated in our
privacy policy. Mapbox's telemetry collection is switched off using the
SDK's own opt-out setting, and the ⓘ attribution button stays on the
map, both because [Mapbox requires attribution on the map](https://docs.mapbox.com/help/dive-deeper/attribution/)
and because that dialog is where the telemetry opt-out lives for users. Everything else about Alpy is
unchanged: no server of ours, no accounts, no analytics, GPS tracks
never leave the phone.

**The paper chart stays.** One tap toggles back to it. Some days you
want the mountain; some days you want the diagram. We like both, and
now neither is pretending to be the other.

---

*Alpy is a free ski app for iPhone with honest instruments: GPS day
tracking, personal records on real named runs, ghost racing, and an
on-device AI debrief. Your GPS tracks never leave your phone.*
