---
layout: post
title: Dissecting fidelSolver's Game Bot for Playing Hack*Match
categories: [presentations]
tags: [C++, Reverse-Engineering]
description: Slides from my December 2018 North Denver Metro C++ Meetup lightning talk.
---

For [December's meeting of the North Denver Metro C++ Meetup](https://www.meetup.com/North-Denver-Metro-C-Meetup/events/255297745/), attendees were encouraged to give 5-10 minute lightning talks.
Around this time, I had been meaning to read through [fidelSolver's](https://www.reddit.com/user/fidelSolver/) code for a [game bot that automatically plays Hack*Match](https://github.com/fidel-solver/exapunks-hack-match), a minigame from the fantasy-virus-writing game [Exapunks](http://www.zachtronics.com/exapunks/). My hope was to learn about the process of writing an automated game-playing bot, so I volunteered to give a lightning talk that presented an overview of how FidelSolver's code monitors and controls the game.

[Footage of their bot in action can be found on their YouTube channel.](https://www.youtube.com/watch?v=vauEdAkAXSE)

My [slides from that talk can be found here](https://docs.google.com/presentation/d/189Mmot1dR8SJpBUtVU_v1IuGTrFM4Wreen1dQWlKjX8/edit?usp=sharing). Feel free to reach out if you have questions on the context of specific slides, either through Email or by directly commenting on the document.

The structure of my talk was as follows:
* Showing the bot in action, to establish context for the code. In addition to the verbal disclaimers that I did NOT write this bot, I also explained the basic rules of the game.
* Introducing fidelSolver, and explaining what little history of them could be found on the internet.
* Explaining some technical difficulties involved with trying to run the code locally through a virtual machine. I also explained an approach of mimicking an x11 window that the code was trying to grab and monitor. This involved saving a screenshot of the game and then loading it through [xloadimage](https://linux.die.net/man/1/xloadimage), to simulate a static screen of the game. While I was able to fudge the code to successfully recognize the static window, the thresholds for image recognition were off, and the code couldn't recognize the game image elements. My theory to this date is that there are environmental differences between running the bot on a virtual machine, versus running it on a native install of Ubuntu.
* The rest of the talk involved explaining my understanding of the code.  Because of the limited time of the lightning talk, I focused primarily on how the bot recognizes elements on the game screen, and how the bot manipuates the X11 window and keyboard controls through the [X Windows System API](https://www.x.org/wiki/)

If any of that piqued your interest, I really recommend looking through the [slides](https://docs.google.com/presentation/d/189Mmot1dR8SJpBUtVU_v1IuGTrFM4Wreen1dQWlKjX8/edit?usp=sharing).
Screenshots from the game are heavily annotated to highlight different aspects of the code, and some of the tricks that fidelSolver employed were quite clever.