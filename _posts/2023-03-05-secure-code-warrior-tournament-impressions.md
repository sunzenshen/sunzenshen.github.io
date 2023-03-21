---
layout: post
title: Secure Code Warrior Impressions
categories: [competitions]
tags: [security, code review, conferences]
description: Impressions from winning the SnowFroc 2023 Secure Code Warrior Tournament
---

Disclosure: Representatives of the company Secure Code Warrior gifted me an etched glass 1st place trophy, as well as a Secure Code Warrior branded thermal coffee mug.

![Receiving the Secure Code Warrior SnowFroc Tournament Champion 2023 trophy on stage.]({{ site.images }}2023_snowfroc_scw_trophy.jpg)

At [SnowFroc 2023](https://www.snowfroc.com/), [Secure Code Warrior](https://www.securecodewarrior.com/) held another tournament based on their learning platform.  A colleague of mine, [Matt Goodrich](https://mattgoodrich.com/) had won the tournament twice before, and I decided to take advantage of his moving to Washington state to enter the competition in his absence.  In the end, I found the competition an oddly engrossing way to practice security code reviews, especially when it became apparent that a small collection of competitors was racing for the most points. It also didn't hurt to win first place, mostly to get a podium picture to send to Matt.  What follows are impressions from the Secure Code Warrior tournament, which may be of niche interest if you are deciding on whether it's worth signing up for a future competition, or if you're evaluating options for a code review training platform.

Secure Code Warrior is a unique take on security training due to its focus on code review. While the mainstay of its assessments are multiple choice questions like with many other security learning platforms, Secure Code Warrior's twist is that the potential answers are sections of code in the context of multi-file diff comparisons.  

Each challenge was broken up in 2 phases:

* Phase 1 (100 points): Either identify the vulnerability category from an insecure code example, or choose where in multiple source code files a requested vulnerability category is present.
* Phase 2 (100 points): Comparing 4 different implementations (represented as multi-file diffs from the original vulnerable code), choose which proposed solution is the best security fix.

I found this emphasis on reviewing code refreshing for a security learning platform, as the act of considering different solution options during code review is not emulated in most other application security trainings.

One suggestion I have for a harder challenge level would be where:

* Phase 1: The player picks the code section that has a problem, without being told the vulnerability type in the question prompt. 
* Phase 2: The player would choose the vulnerability type of the code in question. 
* Phase 3: Like the usual format, choose the best vulnerability fix out of 4 potential diff comparisons.

The reason I believe this format would be appropriate for harder levels was that sometimes the prompted vulnerability category inadvertently helped narrow down the options in the source code selection challenges. A blind category question would more closely emulate the feeling of starting a code review but not yet knowing what sections may be of interest.

When starting the tournament, players chose what language they would like to be tested on. In my case, I decided to choose C++ as the programming language that my problems would be based on.  During the tournament, I noticed that most of my competitors had selected managed/garbage-collected languages like JavaScript and C# for their assessment questions, though one other competitor chose C as their language.  Ironically, by choosing a language infamous for having many gotchas, as with the case with C++ or even C, it's possible that choice affects the relative difficulty of the questions. It might have been easier to identify problems in the code review sections because insecure or broken examples may be easier to come up with in C++.  For example, C++ has unique memory vulnerabilities that showed up in my questions, that may be more obscure in other programming languages.  That said, I'm not sure what the experience was like in other languages, as once I had selected a language it wasn't obvious how to preview another language without interrupting competition progress.

As a way to learn during the competition, a player could choose to get a hint at the cost of overall points to a question. As a competitor, I didn't find the hint system that enticing to use because the hints link to training videos about the vulnerability category being tested. If one was learning but also serious about the competition, it seems like it would be stressful and distracting to burn time having to watch a tutorial video. While guessing incorrectly also deducts points from the potential question score, knowing that an option is wrong was a more direct hint than being given a background tutorial video for the challenge.  The worst that could happen with guess is that maxing out the wrong guesses would return 0 points for the challenge phase.  From a competitive standpoint, it seems that guessing a question and moving on in hope of drawing more familiar questions would be a better use of time due to the relative lack of penalty for guessing.

It seems this lack of penalty for wrong guesses was noticed, as by the end of the competition, the dashboard indicated that my competition had attempted many more questions than I did, but I still won due to having more questions answered accurately. The easiest questions didn't have a huge difference in points to the harder levels, so I still felt it was a good use of time to take time to answer earlier questions more accurately.

I was fortunate to prevail in the end, and I would like to thank work for bombarding me with application security code reviews, which coincidentally prepared me for this competition.