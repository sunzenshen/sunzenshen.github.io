---
layout: post
title: CodeCombat Greed
categories: [competitions]
tags: [javascript]
description: I lost the (virtual) war and all I got was this (actually pretty neat) E-book.
---

Out of curiousity, I entered [CodeCombat’s Greed Tournament](http://codecombat.com/play/ladder/greed), about which an official writeup can be found [here](http://blog.codecombat.com/a-31-trillion-390-billion-statement-programming-war-between-545-wizards).

I wasn’t expecting to win anything, but managed to qualify for a free [E-Book](http://shop.oreilly.com/category/ebooks.do). This was quite a surprise, as my [submission](https://gist.github.com/sunzenshen/69162943e479c78cf86a) was coded over the course of a single accidental all nighter. The approach of my solution was very simple and involved segmenting the area around each gold collector in 4 rectangles, and ordering the collector to move in a diagonal direction towards the most wealthy sector. If a collector was within a short range of the nearest item, then the collector would default to grabbing nearest neighbors. After tweaking a simple build queue for the fighting units and watching some simulated rounds, I called it quits and did not follow the tournament results until receiving the final placement E-mail.

Admittedly, I was psyched out by some of the more dynamic systems submitted, and assumed I would have walked away with nothing but the consolation prize of free [AWS credit](http://aws.amazon.com/). In the end though, with all the duplicate player entries accounted for, the arch-mage “Jinrai” ended up placing [#56 on the Ogres team](http://codecombat.com/play/ladder/greed#winners). While not a superstar finish, I got what I wanted out of the [prize pool](http://codecombat.com/play/ladder/greed#prizes).

After reading some of the retrospectives, it was surprising that traditional theory on the traveling salesman problem was not used by the top two players. This made some sense, as the conditions were dynamic to the point that collectors were tricked into fatally running off the map. Michael Heasell’s [retrospective](http://michaelheasell.com/blog/2014/06/19/greed-2014-the-road-to-victory/) was especially interesting, as his “springs” model was inspiring for its intuitive nature.

All in all, the tournament was definitely a fun experience. I probably should feel more remorse for stopping so early in the competition, but it was oddly rewarding to win my desired [prize](http://shop.oreilly.com/product/0636920029236.do) with relatively little effort. The number of writeups and retrospectives were very amusing to read over, in a forehead-slapping “why didn’t I think of that!” way. I’m definitely looking forward to the future events with CodeCombat, where we can witness more impressive feats from the top competitors.
