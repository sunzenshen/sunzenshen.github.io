---
layout: post
title: LambdaConf 2014 Resources
categories: [events]
tags: [functional programming, conferences, social]
description: Notes on LambdaConf 2014.
---

On April 19th, I spent the day at [LambdaConf](http://www.degoesconsulting.com/lambdaconf/),
a local conference focused on functional programming topics.
The organizer [John DeGoes](https://twitter.com/jdegoes) put together a great team of volunteers and the whole [schedule](http://twileshare.com/uploads/Lambda_Conf_Print_Page.pdf) ran without any issues from my perspective.
I was very much inexperienced with the functional programming paradigm, and my brain had the sensation of melting near the end of the day.
Given that perspective, I’ll spare everyone any uninformed analysis.

Since then, I could not find a central location for reviewing the talks and GitHub repositories,
including the main conference page.
So for my own reference, here’s an incomplete list of resources pulled from various tweets,
itineraries and Google searches:

Events Attended
---------------

**The Silent Productivity Killer by Paul Phillips:**  
[Keynote slides](http://www.slideshare.net/extempore/keynote-lambdaconf2014)  
Conference started off with a keynote by the controversial Paul Phillips
about the state of build times for the Scala compiler.
Unfortunately, the slides do not convey the amusingly heated shouting and arm-waving about the Scala compiler.
I did find another talk of his with a similar sentiment [here](https://www.youtube.com/watch?v=uiJycy6dFSQ).

**Intro to Functional Game Programming with Scala by John Degoes:**  
[Tutorial](https://github.com/jdegoes/lambdaconf-2014-introgame/blob/master/README.md)  
As an FP newbie, I appreciated this workshop the most.
We went over this same tutorial,
and it was really helpful to have John DeGoes present to answer questions and perform a live coding demonstration.
We didn’t make it to the end,
but I remember monads coming into the picture over and over again.
That repetition actually helped my absorbing the concept, if only a bit at a time.

**Macros, Modules, and Languages in Racket by Matthew Flatt:**  
[Workshop repository](https://github.com/mflatt/web-macro-tutorial)

**Monads: Why Should You Care? by [Harold Carr](http://haroldcarr.com/):**  
[Talk slides](https://github.com/haroldcarr/learn-haskell-coq-ml-etc/tree/master/haskell/paper/haroldcarr/2014-04-19-monads-at-lambdaconf-boulder)

**Building Webapps in Clojure by Ryan Neufeld:**  
[Workshop repository](https://github.com/rkneufeld/pedestal-workshop)  
My impression from the talk was that the Pedestal framework hid much of the underlying behavior.
While handy for FP experts,
this abstraction made it hard for newbies like me to understand what was happening on the language level,
especially for those not familiar with writing production Clojure applications.
The live coding demonstration was impressive though,
and wished I knew enough Clojure to appreciate the resulting example code.

**Haskell in 60 minutes by [Brian Mckenna](https://twitter.com/puffnfresh):**  
[Gist with the results of Brian’s live coding session](https://gist.github.com/puffnfresh/9824390)  
This was actually from a [meetup](http://www.meetup.com/frontier-developers/events/169067772/) held a month before LamdaConf.
My own notes from the live coding session turned into a mess by the end of the hour,
so it was helpful to have a definitive gist written by someone who knew what he was actually doing.


Missed Events
-------------
**Idris workshop by [Brian Mckenna](https://twitter.com/puffnfresh):**  
[Talk slides](http://brianmckenna.org/files/presentations/idris-workshop-slides.pdf)  
[Workshop sample code](https://github.com/puffnfresh/idris-workshop)  
The topic of the talk (dependently typed programming) was fairly intimidating,
given my limited exposure to Haskell and even mainstream functional programming.
From hearsay, this was apparently the best talk of the conference.

**How to Write a Perfect Program by Kris Nuttycombe**  
[Talk slides](https://github.com/nuttycom/lambdaconf-2014)

**Complexity and Reasoning in Functional Programming by Kris Nuttycombe:**  
[Workshop repository](https://github.com/nuttycom/lambdaconf-2014-workshop)

**Scala Pattern Matching in Depth by Derek Chen-Becker:**  
[Workshop repository](https://github.com/dchenbecker/lambdaconf2014)

**Functional Web Application with Purescript by Phil Freeman:**  
[Talk slides](https://github.com/paf31/purescript-slides)  
[Workshop repository](https://github.com/paf31/lambdaconf)

Misc Notes
----------
[Rob Norris](https://twitter.com/tpolecat) has a great [writeup](http://tpolecat.github.io/2014/04/22/lambdaconf.html) of all the events I couldn’t attend due to the multiple tracks.
