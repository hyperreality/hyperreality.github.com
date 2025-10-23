---
layout: post
title: "Hack The Box: Backfire Machine"
permalink: /hackthebox-backfire
tags: infosec
---

After years of playing the cybersecurity labs at [Hack The Box](https://hackthebox.com/), I finally had an idea for a machine. I spent some time in 2024 researching [vulnerabilities in open source Command and Control (C2) frameworks](https://blog.includesecurity.com/2024/09/vulnerabilities-in-open-source-c2-frameworks/), and simultaneously [another researcher Chebuya](https://blog.chebuya.com/) was working on the same topic.

We found that two of our exploits made a chain, combining for a full remote compromise of a C2 server behind a firewall. The context would be "hacking back" by taking over a hacker team's own infrastructure. The name "Hackback" had already been used, so ["Backfire"](https://www.hackthebox.com/machines/backfire) was what we decided on.

![Backfire](/assets/backfire.png)

### Walkthroughs

As usual for Hack The Box machines, after the machine was retired, a [video walkthrough](https://www.youtube.com/watch?v=dZjd4XTms7E) was posted by Ippsec, and a [text walkthrough](https://0xdf.gitlab.io/2025/06/07/htb-backfire.html) by 0xdf.

These are brilliant teachers, and I admire their ability to dive deep but also explain each step clearly. Every week I read through 0xdf's latest writeup and note down any techniques I haven't seen before. It was great to see them explore Backfire.

### Feedback

![Polarising reviews](/assets/backfire-reviews.png)

Feedback for Backfire through Hack The Boxes's rating system was somewhat polarised. A lot of players loved the machine, mentioning how original it was and how much they learned. However there was a fair amount of negative feedback too. Perhaps the majority of this was due to the fact that the machine was classified as Medium difficulty when it should have been Hard.

Some feedback was that the machine was "unrealistic". There's often a concern that Hack The Box and CTFs showcase unrealistic vulnerabilities as opposed to real world security knowledge. But I think this is way off the mark here - the machine runs unmodified/barely modified software with active vulnerabilities. You could even hack other Hack The Box players with the exploits!

Lastly, there was feedback that the first step could be frustrating, and I agree with this. I believe that good puzzles should start easier and progress in difficulty, but Backfire did this the other way round. The biggest hurdle was near the beginning and the machine became more linear towards the end. This was simply because we couldn't find any other way to arrange the vulnerabilities so that they made sense. With enough consideration though, I'm sure there would have been ways to design the machine in a more forgiving way, which I will take into account if I make another in future.

