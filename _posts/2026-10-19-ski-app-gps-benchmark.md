---
title: "Independent science on ski-app GPS: the phone and terrain matter more than the app"
description: "A peer-reviewed study ran four ski apps against survey-grade GNSS. The apps were effectively tied; accuracy depended on the phone and the terrain."
---

# Independent science on ski-app GPS

Every ski tracker shows you numbers, and almost nobody gets to check
how accurate they are. In winter 2022/23 a group of researchers did
(the study was published in 2025). Two skiers ran **four ski apps
simultaneously** (Strava, iSki, Slopes, Skitude) on four phone models,
with a 50 Hz differential-GNSS reference rig carried on the back, over
three days at Davos and Zermatt. It's the only study of its kind we
know of, and it's
[openly published](https://pmc.ncbi.nlm.nih.gov/articles/PMC12349078/)
(Petrella, Ellenberger and Gilgien, *PLOS One*, 2025).

## How accurate is ski-app GPS?

At the median, about 4.5 m of horizontal position error and about
0.5 m/s (~2 km/h) of speed error. The researchers computed speed from
each app's recorded positions. The differences between the four apps
were negligible. What moved the numbers was the phone (high-end beat
low-end) and the terrain, with Zermatt's more obstructed sky doing
worse than Davos.

Here's what they found:

- Median horizontal error was ~4.5 m: ~3.6 to 4.1 m on high-end
  phones and ~6.4 to 6.8 m on low-end ones.
- The differences between apps were negligible. Running side by side
  on the same phones, the four apps were effectively
  indistinguishable, and the authors note the apps read the same
  position data the phone records. The phone and the terrain decided
  the result.
- Median speed error was ~0.5 m/s (~2 km/h). It got worse at high
  speed and at Zermatt, where terrain blocked more of the sky; there
  the median position error was about 1.7 times that at Davos.
- Altitude couldn't be assessed at all. Raw GNSS altitude error runs
  2 to 3× the horizontal error, and the apps' altitude handling was
  opaque.

So when ski apps compete on "GPS quality," they're competing on a
layer where, for the four apps tested, the science says they're tied.
Where they can actually differ is what happens after the fix arrives.
Below is Alpy's whole processing pipeline. I'd rather show the method
than ask you to take the numbers on faith.

## 1. The gate: implausible fixes never get in

Before a fix touches anything, it has to pass two tests of our own,
both set conservatively. A fix reporting horizontal accuracy worse
than 50 m is discarded as noise, and a jump implying more than
150 km/h between fixes is discarded as a receiver glitch. A rejected
glitch is also never used as the comparison baseline for the next
fix, so one teleport can't poison a good point behind it.

## 2. The speed cross-check: speed must agree with the map

iOS reports a speed with every fix, and a single speed can be badly
wrong. In the study (which computed speed from each app's recorded
positions) the worst speed error was 21.5 m/s, over 75 km/h. Above
about 29 km/h, Alpy only lets a speed reading contend for your day's
maximum if the actual displacement between fixes roughly supports it.
The allowance is generous, because the straight line between two
fixes always under-measures a carved path. A spike with no movement
behind it is dropped outright; it isn't averaged in or given an error
bar. The top speed is printed with the phone's own accuracy estimate
for the fastest reading of the day: **54 ±3 km/h**.

## 3. Altitude: the barometer carries it

The study couldn't assess altitude, but it notes that altitude
typically carries two to three times the horizontal error, and that
barometers can only improve relative altitude, not absolute position.
Alpy takes that literally and fuses the barometer's relative altitude
with GPS, which acts as a slow absolute anchor. Run detection and
vertical totals use the fused curve; airtime comes from the
accelerometer instead. The method is written up in detail in
[our vertical-measurement post](/blog/how-ski-apps-measure-vertical/).

## 4. The battery guard: data you keep beats data you had

The worst thing a tracker can do is let the phone die at 15:40 with
the whole day unsaved. A noisy point is minor next to that. (Ski
Tracks'
[release notes](https://apps.apple.com/au/app/ski-tracks/id365724094)
say its Watch app also saves automatically on low battery, so credit
where due.) If your battery reaches 10% while tracking and you're not
on a charger, Alpy stops, saves the day, and tells you. The record
survives even if the phone doesn't.

## 5. Honesty about acquisition

The study warns that "at the beginning of a tracking period or in
difficult GNSS conditions, position errors can be very large." While
the phone reports a fix accuracy worse than 35 m (the first minutes,
deep in a lodge, between canyon walls), Alpy says "Acquiring GPS —
numbers firm up with open sky" instead of showing confident garbage.
The study found median position error about 1.7 times larger in
Zermatt's obstructed terrain, and the least an app can do is admit
when it's in that regime.

## Which ski app has the most accurate GPS?

Among the four apps the study tested, none measurably: on the same
phone they were effectively tied. Buy whichever ski app you like,
because the satellites don't care. What's worth asking is what the
app does between the antenna and the screen. That's where gating,
cross-checking, fusing, saving early and admitting uncertainty make
a difference. Our pipeline is written down above, our numbers carry
their error bars, and the study is
[right here](https://pmc.ncbi.nlm.nih.gov/articles/PMC12349078/).

*Alpy is a free, private ski app for iPhone. Every number labeled by
how it was measured. [The app](/) · [More from the blog](/blog/).*
