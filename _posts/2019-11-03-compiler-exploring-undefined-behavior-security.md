---
layout: post
title: Compiler Explorer - Investigating undefined behavior and optimization in C++ 
categories: [presentations]
tags: [C++, assembly, undefined-behavior, nasal-demons, security]
description: Slides from my October 2019 DC303 talk.
---

Abstract: [Compiler Explorer](https://godbolt.org/) is a neat tool not just for exploring the assembly output of compiled source code, but to analyze weird bugs that result from [compiler optimization](https://en.wikipedia.org/wiki/Optimizing_compiler) and [undefined behavior](https://en.wikipedia.org/wiki/Undefined_behavior).


**Slides from my [DC303 talk](https://www.meetup.com/DC303Denver/events/wgcpkqyznbhc/) on [Compiler Explorer](https://godbolt.org/) can be found here:**

[https://docs.google.com/presentation/d/1Po9820xsBw6P_aZTNxFt8U4qjVOJIL_Y0Mo8WVyKoQw/](https://docs.google.com/presentation/d/1Po9820xsBw6P_aZTNxFt8U4qjVOJIL_Y0Mo8WVyKoQw/edit?usp=sharing)

The format of this talk relies heavily on audience participation, but the individual examples are all sourced to the original articles for additional context. Examples include:
* [a notorious Linux Kernel bug, where one lazy null pointer dereference resulted in a proven exploit](https://lwn.net/Articles/342330/)
* [undefined behavior that really will erase your hard disk](https://blog.tchatzigiannakis.com/undefined-behavior-can-literally-erase-your-hard-disk/) (on linux distributions don't protect the root directory)
* [when clearing buffers fails enough to the point of creating an entry during CWE's teenage [ID #'s]](http://open-std.org/JTC1/SC22/WG21/docs/papers/2019/p1315r3.html)
* [an absentminded ASSERT that just ruins everything (for one particular logging bug)](https://www.youtube.com/watch?v=QDxsf7Iv23w)
* [that one concurrency bug that Facebook engineers keep making because they forget to type one letter](https://www.youtube.com/watch?v=lkgszkPnV8g)
* [when the compiler really thinks that your overflow detection is too paranoid and throws it in the garbage without telling you](https://www.kb.cert.org/vuls/id/162289/)

This talk came about as I was talking about [Matthew Butler's](https://maddphysics.com/) course [Exploiting Modern C++: Building Highly-Dependable Software](https://cppcon.org/class-2019-exploiting/) at the DC303 meetup.
The topic of who should present the next month came up, and others suggested that the topic of undefined behavior causing C++ security bugs would be of interest.
Matthew Butler was gracious enough to give the green light to present any topic from his 2-day course as a 2 hour talk, so he gets a credit slide.
