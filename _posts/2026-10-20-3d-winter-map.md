---
title: "How Alpy got a real 3D winter mountain"
description: "Build log: why the paper chart fell short, why we moved from MapKit to Mapbox for 3D, the styling bug that ate our relief shading, and the memory and privacy cost."
---

# How Alpy got a real 3D winter mountain

Alpy has always drawn its own piste maps. The resorts' beautiful painted
panoramas (the Niehues school of hand-drawn mountains) are commissioned
artwork we can't bundle, and they're
[geometrically distorted on purpose](/blog/drawn-not-painted-maps/),
so you can't drape them over real terrain either. Our answer was a clean
paper chart of the resort's real OpenStreetMap network, colored by
difficulty and drawn by us. It was readable and accurate, and it was
flat.

People complained about the flatness. Skiers think of a mountain the
way the lift-line poster shows it, as terrain you can read with the
runs lying on it, and a diagram doesn't match that. We tried to get
there with Apple's MapKit first. I want to be precise about where we
hit the ceiling, because we hit it in public over several builds. In
our tests, satellite imagery looked spectacular from far away and
turned to summer mud up close, while the vector map stayed clean but
read like a road atlas. None of the styles we tried sat in between,
so we moved the 3D view to Mapbox.

## What is Alpy's 3D ski map made of?

Four layers, and you can check every one of them: Mapbox's global
elevation model, relief shading and contours from Mapbox's outdoors
style, the resort's OpenStreetMap piste network drawn on top, and a
winter restyle that turns the base map snow-white at load time.

- Elevation comes from Mapbox's global terrain model (a
  [raster DEM](https://docs.mapbox.com/data/tilesets/reference/mapbox-terrain-dem-v1/)),
  with a gentle 1.3× vertical exaggeration. That's enough to read a
  valley at a glance without lying about a slope.
- Relief shading and contours come from the base style.
- The piste network is the same OpenStreetMap data our paper chart
  uses, encoded as GeoJSON line layers: a white casing under
  difficulty-colored lines, dashed lifts, and run names set *along the
  lines* the way a cartographer would place them. At Zermatt that's 126
  km of pistes, drawn from the same source you can edit yourself on
  openstreetmap.org.
- For winter, we restyle the base map at load time, since Mapbox's
  outdoors style is a general-purpose map. Every land fill becomes
  snowpack white, water keeps its blue, and the relief does the rest.

## The bug that flattened the mountain

That last step ate an afternoon, and the lesson applies to any Mapbox
style work.

Our first "winter" pass turned the whole mountain flat. The relief
shading had vanished, and boosting the hillshade layer's strength did
nothing at all. Three styling iterations went nowhere until we stopped
guessing and printed the style's actual layer stack.

It turns out that in Mapbox's outdoors style, the layer named
`hillshade` isn't a hillshade layer. It's a **fill layer of
pre-computed shadow polygons**, and its color is an *expression* that
varies by illumination class: highlight polygons render
near-invisible and shadow polygons render dark. Our blanket "make
every fill white" rule had been painting the shadows themselves white.
When we tried tinting the layer a constant alpine blue instead, every
polygon, including the highlights that should have been invisible,
flooded the same solid color.

The fix was to leave that one layer completely alone. Over white snow,
its own shading reads like a paper relief map, which was the look we
wanted all along. We're keeping two rules from this: *print the layer
stack before styling anything*, and *a layer whose paint is driven by
an expression can't safely take a constant.*

## The replay rides the same mountain

Day Replay, the chase-cam playback of your ski day, now runs on the
same winter terrain. I kept the port deliberately boring. All the
replay logic (the scrub clock, the smoothed chase heading, the
ghost-skier interpolation) stayed where it was already tested, and the
new map is a dumb renderer that receives positions each frame. Per
tick it updates two one-point geometry sources and moves the camera.
The day's line and lifts upload once, and the matched piste and ghost
line upload only when the run changes. It worked on the first compile.

## What does a 3D ski map cost in memory and privacy?

It costs memory, and there's one privacy trade: map tiles come from
Mapbox's servers. We tear the map views down properly, render the
home-tab preview as a still image, switch Mapbox telemetry off, and
state the tile requests in the privacy policy. Your GPS tracks still
never leave the phone.

A 3D terrain engine uses a lot of memory, so we treated memory as a
feature requirement. The map views are torn down properly on
dismissal. We found and fixed one retain cycle involving a
display-link timer. If you build with `CADisplayLink`, remember
[it retains its target](https://developer.apple.com/documentation/quartzcore/cadisplaylink/init%28target:selector:%29),
so cleanup for a running link can't live in `deinit`. The small
terrain preview on the home tab is now a generated *still image*
instead of a live map engine idling in the background for the whole
app session.

On privacy, map tiles have to come from Mapbox's servers. Those
requests carry the map area being viewed, and our privacy policy now
says so. Mapbox's telemetry collection is switched off using the SDK's
own opt-out setting. The ⓘ attribution button stays on the map,
because [Mapbox requires attribution on the map](https://docs.mapbox.com/help/dive-deeper/attribution/)
and because that dialog is where the telemetry opt-out lives for
users. Everything else about Alpy is unchanged: no server of ours, no
accounts, no analytics, and GPS tracks never leave the phone.

The paper chart stays, one tap away. Some days you want the mountain
and some days you want the diagram, and I like having both.

---

*Alpy is a free ski app for iPhone with honest instruments: GPS day
tracking, personal records on real named runs, ghost racing, and an
on-device AI debrief. Your GPS tracks never leave your phone.*
