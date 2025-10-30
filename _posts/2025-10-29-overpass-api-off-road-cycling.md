---
layout: post
title: "Mapping Off-Road Cycling Areas, Part 2"
permalink: /overpass-api-off-road-cycling
tags: maps cycling
---

After publishing [my first map of off-road cycling density](/overpass-api-cycling-density) in England, I got some great feedback online. On the whole the results seemed to match people's intuition, but there was confusion why areas like Gloucester or Tyneside scored highly while areas like the Peak District did not.

This seems to be a general issue with counting stuff per unit of area. Smaller, more densely populated districts get higher scores than they seem to deserve. However, mapping per capita instead goes too far in the other direction, unduly penalising areas with high population density.

A few people suggested a compromise which is to look at kilometres of off-road cycling routes per kilometre of road. In other words, the length of the off-road cycling network as a percentage of the length of the road network. I also added data for Wales.

<iframe title="Off-Road Cycling % by District" aria-label="Choropleth map" id="datawrapper-chart-P4S79" src="https://datawrapper.dwcdn.net/P4S79/2/" scrolling="no" frameborder="0" style="width: 0; min-width: 100% !important; border: none;" height="788" data-external="1"></iframe><script type="text/javascript">window.addEventListener("message",function(a){if(void 0!==a.data["datawrapper-height"]){var e=document.querySelectorAll("iframe");for(var t in a.data["datawrapper-height"])for(var r,i=0;r=e[i];i++)if(r.contentWindow===a.source){var d=a.data["datawrapper-height"][t]+"px";r.style.height=d}}});</script>

This changes the results in a direction which makes sense. Mole Valley and Chichester are top, the only two districts with off-road cycling networks over half as long as their total road networks. These areas have immense bridleway networks in the North Downs+Surrey Hills, and South Downs respectively.

Meanwhile the Isle of Anglesey, and Kensington and Chelsea were the lowest with around 25x as many roads as off-road cycling routes.
