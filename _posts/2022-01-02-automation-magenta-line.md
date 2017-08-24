---
layout: post
title: Automation and Children of the Magenta Line
permalink: /automation-magenta-line
tags: engineering
---

I've recently been reading [Admiral Cloudberg's](https://admiralcloudberg.medium.com/) analyses of famous aviation disasters. They are clear, well-researched articles which present complex events in a way that a layman can understand. The articles end by showing how each incident led to improvements in procedure, engineering, or personnel training.

There's much that can be learned from these incidents and practices of the airline industry, that can be applied to other fields. A common thread in the reports is a large number of unfavourable conditions appearing at the same time. For instance, the [1977 Tenerife airport disaster](https://imgur.com/a/uyheX) remains the deadliest in aviation history in terms of airliner passenger fatalities. There was a long chain of factors that led up to the crash of two airplanes on the runway:

![Tenerife disaster factors](/assets/tenerife_disaster.png)

In this case and others a lot of people lay 100% of the blame on a single factor: the pilot's poor judgement, but the whole story should be considered. Many planes that crashed were flown by experienced pilots with excellent records, and it's often because a series of unusual circumstances put them under pressure and enabled them to make uncharacteristically terrible decisions. Since then, precautionary measures have been added by aviation authorities to ensure that crew feel empowered to challenge captains (modern crew resource management / CRM). And radio communication between aircraft and air traffic control has become clearer and more direct.

The writeup reminded me of the [Swiss cheese model of accident causation](https://en.wikipedia.org/wiki/Swiss_cheese_model), which comes up in IT operations and security engineering. Robust systems have multiple layers of defences, so that the holes or weaknesses of one layer are counteracted by the strengths and safeguards of other layers. Accidents can occur when the holes in multiple layers align, allowing a hazard to pass through.

Another interesting theme from this reading was "automation dependency". In engineering fields we generally regard automation as a great thing, as it takes care of low-level tasks, reduces human error, and lowers costs. But, if the humans operating the system do not fully understand how it works, or become complacent about automation, this can lead to catastrophe. If you have time, this video is an aviation classic:

[https://vimeo.com/groups/364219/videos/159496346](Children Of The Magenta Line Vimeo Video)

In my first site reliability engineering job, I was fortunate to work with experienced engineers who were experts at triaging and fixing systems problems. When all hell was breaking loose, pagers were alarming, and customers were starting to call up, they calmly investigated to find the root cause. They knew that if they misdiagnosed and tried to solve the wrong problem, the situation could get a lot worse. Understanding what is actually happening, and not drawing overly quick conclusions by becoming over-reliant on a single potentially faulty indicator, were key lessons that I learned. Of course, I imagine all this is easier said than done, if you're piloting an aircraft in a critical situation. So I have a huge respect for those who can keep a cool head and guide complicated systems away from disaster.

