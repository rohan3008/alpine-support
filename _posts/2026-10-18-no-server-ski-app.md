---
title: "A ski app with no server: what that actually means"
description: "Alpy has no backend at all — no accounts, no sync, no analytics. What a no-server architecture changes about privacy, and what it honestly costs."
---

# A ski app with no server: what that actually means

Most apps' privacy pages say some version of "we take your privacy
seriously." The claim is unfalsifiable: you can't audit their
servers. There's a stronger position available to a small app, and
Alpy takes it: **have no server at all.**

This isn't a policy, it's an architecture, and it changes what's
*possible* rather than what's promised:

- **GPS tracks can't leak** — they're written only to the app's
  storage on your phone. There is no upload endpoint. A breach of our
  infrastructure is impossible because there is no infrastructure.
- **No account exists to be phished,** no password to reuse, no email
  list to sell. The app has never asked who you are.
- **No analytics** — we genuinely don't know how many users the app
  has beyond what Apple's opt-in store stats show. Weather and map
  requests go straight from your phone to the public sources
  (Open-Meteo, OpenStreetMap, avalanche services) with coordinates
  only.
- **AI runs on the device.** The morning report and day summary are
  written by Apple's on-device model. No prompt ever crosses the
  network.

## What it honestly costs

No server means no cloud backup of your season (your phone's own
backup covers it), no cross-device sync, no social feed, and friend-
finding that works by Bluetooth proximity rather than a live map of
your crew across the mountain — physics instead of infrastructure.
Apps with servers do those things well, and if they're what you want,
a subscription app is the right choice.

We'd rather be the app where the privacy claim requires no trust.
"Nothing leaves your phone" isn't in our policy. It's in the
architecture — there's nowhere for anything to go.

*[Privacy policy](/privacy) — short, because there's
little to disclose.*
