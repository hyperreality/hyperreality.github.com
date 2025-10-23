---
layout: post
title: "Mapping Off-Road Cycling Areas with Overpass API"
permalink: /overpass-api-cycling-density
tags: maps cycling
---

Which area of England has the densest network of off-road cycle routes? Until recently, I would have had no idea how to answer this question. But with Overpass API, Datawrapper, and an LLM, I found it surprisingly easy to whip up some results.

I enjoy cycling off-road and like to plot routes that avoid roads as much as possible. Will this help me find the ideal place to live?

<iframe title="Cyclable Density by District" aria-label="Choropleth map" id="datawrapper-chart-tgQMX" src="https://datawrapper.dwcdn.net/tgQMX/1/" scrolling="no" frameborder="0" style="width: 0; min-width: 100% !important; border: none;" height="788" data-external="1"></iframe><script type="text/javascript">window.addEventListener("message",function(a){if(void 0!==a.data["datawrapper-height"]){var e=document.querySelectorAll("iframe");for(var t in a.data["datawrapper-height"])for(var r,i=0;r=e[i];i++)if(r.contentWindow===a.source){var d=a.data["datawrapper-height"][t]+"px";r.style.height=d}}});</script>

#### Map Takeaways

 * The map counts bridleways, cycleways, shared used paths, and more (see below)
 * East London and Cambridge have the highest concentration of off-road cycle routes
 * Devon has the lowest concentration
 * The map doesn't reflect the quality of the routes in any way
 * The data correlates with population density, as urban areas tend to have more cycle infrastructure

#### Technology Takeaways

 * Overpass API is a powerful tool for querying geographical data
 * ChatGPT is impressively good at writing queries for it
 * Datawrapper produces beautiful maps with minimal effort
 * OpenStreetMaps tagging has a lot of inconsistencies

#### Analysis

This was a fun exercise but I don't think I would use it in deciding where to live or cycle. Ultimately there is little comparison between a mountain bike trail, a picturesque bridleway, and an urban cycleway. Although all are off-road cycle routes, each serves a completely different purpose.

Further, even if we limit our search to just one type of cyclable route, the quality of them varies hugely - even within the same area. Some bridleways are excellent, others are virtually unrideable. And I would prefer to cycle on a quiet road rather than a busy, interrupted, debris-strewn shared use path.

The [Strava heatmap](https://www.strava.com/maps/global-heatmap?hl=en-GB&sport=MountainBikeRide&style=dark&terrain=false&labels=true&poi=true&cPhotos=true&gColor=blue&gOpacity=100#9.7/51.3196/-0.4579) is the most valuable data in my opinion, as it shows where people actually ride. 

### Process

The rest of the blog documents how I produced the map. Here's a [link to the data](https://gist.github.com/hyperreality/3b510afadc7c9089ed33f1222f0359e7).

#### Bridleways

The closest previous work was a [website which maps bridleways](https://bridleways.uk/counties). Bridleways are horse-riding routes which cyclists have also been allowed to ride on [since 1968](https://en.wikipedia.org/wiki/Countryside_Act_1968). My initial idea was just to grab the per-county bridleway length calculations from that site, but I wanted to go to the source of the data. Then I could include all off-road cycle routes, and show the availability of those routes in smaller areas across the country.

I saw that site gets its data from OpenStreetMap, a community-driven map database that is particularly good for outdoor mapping like hiking trails and cycling routes. OpenStreetMap data is used by platforms like Strava and Komoot.

#### Overpass Turbo

I found [Overpass Turbo](https://overpass-turbo.eu/), a great resource for freely querying OpenStreetMap data. Overpass has a tricky [query language](https://wiki.openstreetmap.org/wiki/Overpass_API/Overpass_QL) which ChatGPT was awesome at assisting with.

![](/assets/osm/overpass.jpg)

OpenStreetMap uses the term ["highway"](https://wiki.openstreetmap.org/wiki/Highways) as a catch-all for roads, paths, and tracks. Highways are tagged with information about their designation and who is permitted to use them. By navigating to a part of the map you know well and running the following query, you can view the tags on all the highways:

<script src="https://gist.github.com/hyperreality/acd05c622667ddf8a0fb2446ababd851.js"></script>

#### Inconsistent Data

Exploring the OpenStreetMap tagged data, I discovered it was often inconsistent and confusing in terms of how it indicated cycle access. Partly I think this is due to it being a community map with different users adding different tags to represent the same information. It's also probably to do with how complicated the access situation is in England (and the rest of the UK, besides Scotland). The following are places where you can usually ride your bike:
 * bridleways 
 * [restricted byways](https://www.cpre.org.uk/discover/permissive-to-public-know-your-pathways/)
 * BOATS (byways open to all traffic)
 * shared used paths
 * permissive paths
 * cycle tracks
 * canal towpaths

The following is marked as a bridleway but (presumably incorrectly) with a designation of `public_footpath`:

![](/assets/osm/footpath.jpg)

Meanwhile the following is a bridleway, but a local bylaw prohibits cycling, and the tags correctly show this:

![](/assets/osm/bridleway.jpg)

The following is a track, a kind of miscellaneous highway, which is on private land, but with permissive bicycle access:

![](/assets/osm/private.jpg)

That's one of the best cycle routes in the area, and if you are just looking at bridleways or cycle paths, you'll miss it. So writing a query to capture all these highways is not immediately straightforward.


#### Length Query

Bearing that in mind, I enumerated all the ways that off-road cycle routes are represented and summed the length of them in a given area. The resulting [Overpass query](https://gist.github.com/hyperreality/b93014b232b38d895e4721a8a3f6f3fd) is not perfect but provides a close enough approximation.

I tested on the county of Surrey, and the query returned 11190 cyclable ways with a total length of 2070 kilometres.

#### Ceremonial Counties Density

ChatGPT helped me with a small script to run this query for each of the 48 ceremonial counties in England. I fetched a list of counties together with their areas from [here](https://populationdata.org.uk/english-counties-by-population-and-area/).

I had some trouble with the OpenStreetMap data, since Hertfordshire, Norfolk, Suffolk, Worcestershire, Warwickshire, Shropshire, Northumberland, Greater Manchester, and the City of London were not marked as ceremonial counties, so those areas had to be selected using an [administrative boundaries tag](https://wiki.openstreetmap.org/wiki/Tag%3aboundary=administrative).

I also got a surprisingly low density result for Tyne and Wear. It turns out that the area figure reported on the website above was missing a zero, and after correcting that Tyne and Wear is one of the top counties.

I then plotted the results using [Datawrapper](https://www.datawrapper.de/):

<iframe title="Cyclable Density" aria-label="Choropleth map" id="datawrapper-chart-dhW79" src="https://datawrapper.dwcdn.net/dhW79/1/" scrolling="no" frameborder="0" style="width: 0; min-width: 100% !important; border: none;" height="788" data-external="1"></iframe><script type="text/javascript">!function(){"use strict";window.addEventListener("message",function(a){if(void 0!==a.data["datawrapper-height"]){var e=document.querySelectorAll("iframe");for(var t in a.data["datawrapper-height"])for(var r,i=0;r=e[i];i++)if(r.contentWindow===a.source){var d=a.data["datawrapper-height"][t]+"px";r.style.height=d}}})}();</script>

Cool! Datawrapper helps you make really nice visualisations with relatively little effort. However...

#### Density Limitation

An obvious issue with the Cyclable Density metric is the strong correlation it has with population density. Urban areas are more likely to have cycle infrastructure, therefore the map ends up resembling a population density map:

![](/assets/osm/population-density.jpg)

Nevertheless, there's still some observations that can be drawn. For instance, Essex, Kent, and East Sussex are clearly behind the rest of the Home Counties for off-road cycle routes. Wiltshire and Dorset on the other hand are doing pretty well.

#### Per capita

Attempting to compensate for the urban density effect, I divided the cyclable length by population instead, to get the per-capita provision of off-road cycle paths:

<iframe title="Cyclable Metres Per Capita" aria-label="Choropleth map" id="datawrapper-chart-zivNd" src="https://datawrapper.dwcdn.net/zivNd/2/" scrolling="no" frameborder="0" style="width: 0; min-width: 100% !important; border: none;" height="804" data-external="1"></iframe><script type="text/javascript">window.addEventListener("message",function(a){if(void 0!==a.data["datawrapper-height"]){var e=document.querySelectorAll("iframe");for(var t in a.data["datawrapper-height"])for(var r,i=0;r=e[i];i++)if(r.contentWindow===a.source){var d=a.data["datawrapper-height"][t]+"px";r.style.height=d}}});</script>

This completely changes the map, with urban areas now having the lowest scores. This map highlights that Cumbria is the place to go if you want cycle routes all to yourself!

#### Local Authority Districts

The county area data is not really granular enough, so I went a level deeper by mapping [local authority districts](https://en.wikipedia.org/wiki/Districts_of_England). There are 296 local authority districts in England.

Learning my lesson from before on inconsistent OpenStreetMaps tagging, I found what appeared to be a definitive way to query districts using [GSS codes](https://en.wikipedia.org/wiki/GSS_coding_system). I pulled a list of the districts mapped to GSS codes from [here](https://geoportal.statistics.gov.uk/datasets/5779a9578f0e48ccacef6af41546b56b_0/explore) and joined that up with areas from Wikipedia.

Once again however I had to special-case some districts with an administrative boundaries tag selector. OpenStreetMaps does not seem to have up-to-date GSS codes tags for East Staffordshire, Lichfield, Stafford, Staffordshire Moorlands, Tamworth, North Warwickshire, Nuneaton and Bedworth, Rugby, and Warwick.


