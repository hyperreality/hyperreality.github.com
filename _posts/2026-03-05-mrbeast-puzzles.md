--- 
layout: post
title: "Mr Beast Million Dollar Puzzle: Twice Bitten, Thrice Shy"
permalink: /mrbeast-million-dollar-puzzle
tags: internet puzzle games
---

## $100,000 "World's Hardest Riddle"

Back in July 2020 Mr Beast published a ["Solve This Riddle For $100,000" challenge](https://www.youtube.com/watch?v=fZDUxJ-7Y4A). For my puzzle-loving friends, stuck indoors, this was an unmissable opportunity.

![](/assets/mrbeast/100k.jpg)

Mr Beast called it "The World's Hardest Riddle" but it was mainly a series of extremely tedious web challenges, including:
 * a page that generated thousands of QR codes, only one of which worked
 * a flappy bird clone that was impossible to play due to server lag
 * a button that you had to press after exactly 69.069 seconds had elapsed

#### No Winner

My team completed the challenges in about 8 hours, and we thought we'd won it! We were gutted to discover that another team got there 5 minutes quicker.

Later we learned something stranger: the other team never received a prize, and no winner was ever publicly announced. That was odd because a winning condition required the winner to agree to appear in a Mr Beast video.

If I had to speculate, the challenges were so hostile that many teams used scripts and automation to bypass the worst parts, and the organizers decided the finishing methods didn't count as fair play. 

## $1,000,000 Salesforce Puzzle

On Feb 7th 2026 Mr Beast published a ["Watch My Super Bowl Ad To Win $1,000,000!" video](https://www.youtube.com/watch?v=OBQELGS13XA). This was a collaboration with Salesforce to advertise their AI Slackbot. The puzzle's home page and instructions were launched on [mrbeast.salesforce.com](https://mrbeast.salesforce.com/).

![](/assets/mrbeast/vault.jpg)

The puzzles themselves were made by a company called [Lone Shark Games](https://lonesharkgames.com/) with a good reputation, so expectations were high - although Lone Shark Games apparently had less than a month to make the whole thing. [Solutions](https://delfinadap.github.io/mrbeast-51-locations/) have been meticulously [documented](https://writeup.retrocraft.ca/) by some of the top players.

### Stage 0

![](/assets/mrbeast/stage0.jpg)

The first set of puzzles were found in links in pinned Mr Beast video comments, and were word search and picture-based style puzzles. Together they decoded to the phrase: 

> EVERY CHALLENGE LEADS TOWARDS LOCATION NAME SOMEWHERE AROUND WORLD

### Stage 1 (51 locations)

Stage 1 contained 51 varied location puzzles, hidden across Mr Beast and influencer videos, especially the ["Mr Beast Vault" video](https://www.youtube.com/watch?v=Lp9OEfkWfLI).

Solving them was a massive community effort that mainly took place on the Lone Shark Games Discord server. It was nice to see the amount of public solving and information sharing. There was a big variety of puzzles that used creative techniques I haven't seen before.

A frequent complaint I saw was how trigger-happy the moderators of the Discord server were at banning people. I didn't take much notice of this until bizarrely I got banned without ever posting there. The top players moved to the Serious Mr Beast Scavenger Hunters Discord.

Most puzzles seemed fun and fair; some were brutally obscure until you coaxed hints out of the Salesforce bot:

![](/assets/mrbeast/stage1.jpg)

The hunt was intended to market the Salesforce AI bot, which turned out to be a generic LLM chatbot that you had to go through two rounds of email authentication to access. Useful clues only came from "Beastbot" which just grepped your messages for key phrases.

There was a Sudoku puzzle which was about 100x as technical as anything else, where each player who visited a website got a different numbered Sudoku numbered from 100000 to 900000. We needed to reverse engineer the Sudoku generation algorithm to find what the Sudokus numbered 1 to 25 would have been. By taking the sum of isolated numbers in those grids, and using those sums to index into a phrase in the famous Mr Beast counting to 100k video, we found another location. 

### Stage 2 (40 locations)

Stage 2 had 40 more location puzzles grouped into car, horse and plane trips on the website [beast.travel](https://beast.travel):
 * Car trips were rebus puzzles
 * Horse trips were cryptic crossword clues leading to what3words locations
 * Plane trips were Geoguessr-style views

Each of the 40 location puzzles also had a mysterious 12 letter word associated with it:

![](/assets/mrbeast/stage2.jpg)

Soon a "Trips By Boat" page appeared where all 91 locations discovered so far could be sorted into position based on word lengths:

![](/assets/mrbeast/boat.jpg)

Coloured vehicles at certain letters spelled out a crucial instruction showing the format of the final answer:

> IN JIMMYS VAULT FIRST PART STICKS ROAMY RESULTS IN BETWEEN STAGE ONE ANSWER PAIRS LAST PART HE SHOWED AT START

This was around the time I properly joined in the puzzle hunt, and it was enjoyable trying to figure out what to do next. Daily hints dropped by the creators were essential in narrowing down the possibilities.

A "Trips By Roamy" page also appeared that slowly revealed lines of three locations together, referenced by their corresponding coloured vehicle, building up the scaffolding for an answer.

![](/assets/mrbeast/roamy.jpg)

To solve, you needed to infer several hidden constraints:
 * Stage 2 locations are found on [geodesic lines](https://en.wikipedia.org/wiki/Geodesic) between pairs of Stage 1 locations
 * Car, Horse, and Plane locations are clustered in groups
 * All Stage 2 locations and Stage 1 locations are used to form a 40 part trip, meaning 30 of the 50 Stage 1 locations are reused, and 20 are only seen once
 * This leads to 9 separate groups of triplets chained together
 * Plotting the geodesic lines makes letters and numbers visually appear

The difficulty was that few of the Stage 2 locations were located perfectly between Stage 1 locations on geodesic lines, and several correct answers turned out to be way off (up to 20km). We also didn't have precise co-ordinates for all the locations. Many players were using vibe-coded scripts to try to find chains of correct location triplets by closest match, however due to the large tolerances and fact that many triplets didn't chain, this didn't work too well.

The biggest breakthrough was realising that the first letters of the 12-letter words anagrammed to `NUMBERS FOR THIS HALF WOULD SMELL AS SWEET AS ONE`. We believe we were one of the first teams to notice this, when we saw that the first letters followed a really nice frequency distribution. This anagram then locked in an order for most of the Stage 2 locations.

It was only through a manual process of working through the anagram and map simultaneously (and getting help from someone called formerlycharles) that we eventually figured the full puzzle out. Most notably, `NUMBERS` corresponded with a clear "R" drawn on the map in North America which also seemed a valid start for "Rose" which the anagram phrase referenced, from Romeo and Juliet.

Plotting the lines gave the following (not 100% accurate but close enough):

![](/assets/mrbeast/drawn_map.png)

Reading the red, then yellow (mirrored), then blue lines in order gives the characters:

> R62 L39 R05

This forms the first part of a combination code for Jimmy's vault. The characters were hard to spot until almost all the lines were drawn correctly. Many other players built great tools to visualize it - LLMs have really changed the game for this sort of puzzle.

The characters roughly correspond to "ROSE" spelled twice. If laid out in rows of 10, the phrase `NUMBERS FOR THIS HALF WOULD SMELL AS SWEET AS ONE` also spells "ROSE" at the end:

```
NUMBERSFOR
THISHALFWO
ULDSMELLAS
SWEETASONE
```

This was one of the most creative and clever multi-layered puzzles I've ever seen.


### Endgame Frustration

If the `R62 L39 R05` vault code from Stage 2 had unlocked the $1,000,000, I feel this would have been a satisfying ending. Whichever player managed to figure out the map constraints first, based on limited information, deserved the prize.

Everyone is now stuck on the maddeningly vague "LAST PART" referenced in the answer phrase.

Going against best practice learned from years of puzzles and capture the flag contests, there is no format given for the final answer. You would expect it to be a 6 part vault code, but if so it would certainly be solved by now, and a previous hint suggests there is something more than that.

There are several photos on Mr Beast social media that could plausibly contain more of the answer. Nobody knows how many of these there are, what order they go in, or what other information should be included. 

![](/assets/mrbeast/rose.jpg)

Maybe there is an elegant solution that snaps everything into place. And sure, it's a million dollars, it's not gonna be straightforward. But after thousands of people worked for weeks, motivated by life-changing money, making structured progress, it's a bit of a let down. I've been burned too many times before by overly guessy [puzzles that have no clear path forward](https://github.com/puzzlehunt/gsmgio-5btc-puzzle/issues/84) and have lost interest in this one.
