---
layout: post
title: "Mapping Walking Areas in England and Wales"
permalink: /overpass-api-walking
tags: maps walking
---

I love exploring areas with a lot of footpaths that lead away from roads. This map aims to find the local authority districts with the highest proportion of "walkable" routes compared to "drivable" routes:

<iframe title="Off-Road Walking by District" aria-label="Choropleth map" id="datawrapper-chart-gbIwg" src="https://datawrapper.dwcdn.net/gbIwg/1/" scrolling="no" frameborder="0" style="width: 0; min-width: 100% !important; border: none;" height="788" data-external="1"></iframe><script type="text/javascript">window.addEventListener("message",function(a){if(void 0!==a.data["datawrapper-height"]){var e=document.querySelectorAll("iframe");for(var t in a.data["datawrapper-height"])for(var r,i=0;r=e[i];i++)if(r.contentWindow===a.source){var d=a.data["datawrapper-height"][t]+"px";r.style.height=d}}});</script>

The technique used to generate the map is described in [my post on off-road cycling density](/overpass-api-cycling-density).

What is counted as "walkable"? Basically anything that you can legally walk on, that isn't the pavement or a road:

 * Public Footpaths
 * Bridleways
 * Restricted Byways
 * "Tracks" where foot access is explicitly allowed
 * Byways Open to All Traffic (BOATs) [1]

What are the top districts for walking?

 1. High Peak - 2090
 2. Rossendale - 1948
 3. New Forest - 1930
 4. Ribble Valley - 1871
 5. Mole Valley - 1760

Note that Isles of Scilly has an anomalously high score of over 5000; the islands have lots of walking trails and very few roads. They are overall the best but they are such a small area and mess up the scale of the rest of the map, so have been omitted from the map.

![](/assets/osm/scilly.jpg)

And the bottom districts for walking?

 1. Slough - 252
 2. Wolverhampton - 277
 3. Knowsley - 287
 4. South Holland - 289
 5. Brent - 290

Now I really do need to get out and explore more of the UK!

[1] These are also open to vehicles, but in my experience are generally good walking routes.
