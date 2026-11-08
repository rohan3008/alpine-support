---
title: "A ski app with no server: what that actually means"
description: "Alpy has no backend at all: no accounts, no sync, no analytics. What a no-server architecture changes about privacy, and what it costs you."
---

# A ski app with no server: what that actually means

A privacy page that says "we take your privacy seriously" asks for
trust. The claim is unfalsifiable, because you can't audit the
servers behind it. A small app can take a stronger position, and Alpy
does: it has no server at all.

## What does "no server" mean for a ski app?

It means there is nowhere for your data to go. Alpy has no backend:
no accounts, no sync, no analytics. GPS tracks are written only to
the app's storage on your phone, the AI runs on the device, and
weather and map requests go straight from your phone to the
services that answer them.

Because that's built into the architecture, some things simply can't
happen:

- GPS tracks can't leak. They're written only to the app's storage on
  your phone, there is no upload endpoint, and no server of ours holds
  your tracks, so there is nothing of ours to breach.
- No account exists to be phished, no password to reuse, no email
  list to sell. The app has never asked who you are.
- There are no analytics. We don't know how many users the app has
  beyond what App Store Connect reports, and the Mapbox map SDK's
  telemetry is switched off in the app. Weather, map and bulletin
  requests go straight from your phone to their sources (Open-Meteo,
  OpenStreetMap's public Overpass API, the SLF and avalanche.org
  bulletin feeds, and Mapbox for the 3D map tiles). The weather and
  map requests carry a location; none carries your track or who you
  are.
- AI runs on the device. The morning report and day summary are
  written by Apple's
  [on-device model](https://developer.apple.com/documentation/foundationmodels/systemlanguagemodel),
  and Alpy sends no prompt over the network.

## What do you give up with a no-server ski app?

No server means no Alpy cloud backup of your season (your phone's own
[iCloud Backup includes app data](https://support.apple.com/en-us/108770)),
no cross-device sync and no social feed. Friend-finding works by
Bluetooth proximity instead of a live map of your crew across the
mountain. Apps with servers can do those things, and if they're what
you want, a subscription app is the right choice.

We'd rather be the app whose privacy claim requires no trust.
"Nothing leaves your phone" holds because of how Alpy is built: there's
nowhere for anything to go.

*[Privacy policy](/privacy/): short, because there's little to
disclose.*
