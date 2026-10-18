---
title: "The Alpy blog — honest ski-tech writing"
description: "How ski tracking actually works: GPS vs barometer, turn estimates, ghost racing, avalanche bulletins, pass coverage, on-device AI. First-party writing from the makers of Alpy."
---

# The Alpy blog

Writing about how ski tracking actually works — measurement, honest
estimates, open data, and what a no-server app can and can't do.
Every number here traces to the app or a named source.

{% for post in site.posts %}
- **[{{ post.title }}]({{ post.url | relative_url }})** — {{ post.description }}
{% endfor %}

*Alpy is a free, privacy-first ski app for iPhone.
[What it does](../) · [Alpy vs Slopes](../compare) ·
[Resort data](../resorts/)*
