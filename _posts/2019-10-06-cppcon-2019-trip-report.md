---
layout: post
title: CppCon 2019 Trip Report 
categories: [reports]
tags: [cpp, conventions]
description: Postcard from sunny Aurora, Colorado
---

Yet Another CppCon 2019 Trip Report
===================================

[CppCon](https://cppcon.org/) is the main(stream) C++ programming language conference in the US, and it has recently relocated near my neck of the prairie in Aurora, Colorado.
I've always been a little skeptical of the usefulness of conference trip reports for the dear reader,
but I've learned first hand that handwritten notes get lost in some inexplicable black hole as soon as they are archived on the bookshelf.
The sections of this trip report will focus on aspects of the conference which can be independently researched (such as the talks which are usually uploaded on the [CppCon Youtube channel](https://www.youtube.com/user/CppCon/featured)) or considered for future years (such as whether to volunteer or not, or what the classes were like).

Venue
=====
The venue, the [Gaylord Rockies](https://www.marriott.com/hotels/travel/dengr-gaylord-rockies-resort-and-convention-center/), is massive, and was hosting several other conferences in the adjacent ballrooms.
This proximity drew in some curious non-programmers, and it was actually kind of fun trying to explain what CppCon was about to off-duty police officers who were raising funds for the 
[Law Enforcement Torch Run for the Special Olympics](https://www.specialolympics.org/about/partners/law-enforcement-torch-run).
And apparently [Discount Tire](https://www.discounttire.com/) throws fancy tuxedo and gown balls for their employees???

There were some challenges that the venue imposes, such as the extreme parking prices, lack of rooms for all the attendees that wanted to stay, and the relative scarcity of nearby hotels and restaurants (translation: the Gaylord is in the middle of the nowhere).
But most insulting of all, the promo renders of the venue [depict the Rocky Mountains on the wrong side of the building](https://i.ytimg.com/vi/WA-crlCfHTc/maxresdefault.jpg)!!! (The real life mountain view is still fabulous, though.) 

Overall, despite the annoyances of the venue, I'm still excited to have CppCon so conveniently close to home for the next few years.

Volunteering
============
This year, I volunteered part time at the conference, in exchange for free admission during the week.
Volunteering also discounts the cost of the pre-and-post conference classes.
Is volunteering worth it? I really enjoyed the experience and hope to volunteer again next year!
You may sometimes miss a talk due to conflicting shift responsibilities,
but it's a lot of fun working and hanging out with other volunteers who are passionate enough about C++ and software engineering to give their time to the conference.

One piece of advice I would give though, is that volunteers should sign up for shifts as soon as the scheduling system is published.
The most popular slots were those helping speakers set up their talks, which allows you to watch the talk (with the responsibility of flashing reminder cards to the speakers)!
If you were like me and waited until the weekend to decide, you may end up with a lot of shifts manning the book store or coat check.
But even those responsibilities were still fun due to the interesting conversations with fellow shift volunteers.

Pre-Conference Class: Concurrency with Modern C++
=================================================
For the pre-conference class, I took [Rainer Grimm's](https://www.modernescpp.com) class [Concurrency with Modern C++](https://cppcon.org/class-2019-concurrency-with-modern-cpp/).
I thought the class was a great exploration of the foundations of concurrency in C++, such as the memory model of C++ and the standard library APIs for locks, atomics, futures, condition variables, and other functionality.

Truthfully though, I felt that the class didn't actually reach the real reason I took the class, namely the coverage of concurrent/parallel data structures and algorithms.
The class syllabus promised such topics, but the pace of the class didn't quite allow us to reach that point in two days.
However, we got to keep electronic copies of the course slides and code samples, which did include coverage of such topics.
And as an added bonus, students also received E-book copies of Rainer's latest 2 books, ["The C++ Standard Library" and "Concurrency with Modern C++"](https://leanpub.com/b/thecstandardlibraryandconcurrencywithmodernc).

Rainer did a great job of exploring live code demos of some tricky concurrency bugs, and was extremely helpful with answering questions that arose during those interactive sessions.
He also demonstrated some of the tooling available for diagnosing concurrency bugs, such as sanitize flags in gcc and clang.

The weeks before, I had actually done some class prework of going through the video class [High-Performance Computing and Concurrency](https://www.oreilly.com/library/view/high-performance-computing-and/9781491967560/)
by [Fedor G. Pikus](http://www.pikus.net/~pikus/). To compare the two styles of class, Fedor's online course had more time to present lecture content than the 2 day live class,
but it was much easier to understand Rainer's coding demos when you can ask for live clarification!

Talking with students from other classes, I heard that [Anthony William's](https://www.justsoftwaresolutions.co.uk/blog/) class 
[More Concurrent Thinking in C++: Beyond the Basics](https://cppcon.org/class-2019-concurrent-thinking/)
took very little time to cover the basics of concurrency/parallelism in C++, and instead jumped directly into higher-level concepts such as a revisitation of the 
[Dining Philosopher's problem](https://en.wikipedia.org/wiki/Dining_philosophers_problem) with modern C++.

For anyone deciding between the two concurrency classes, I would say that it depends on your familiarity with the concurrency APIs offered by C++11 and later standards.
If you don't need an explanation on the difference between threads and futures, it may be worth just going straight into the Beyond the Basics class.


Post-Conference Class: Exploiting Modern C++: Building Highly Dependable Software
=================================================================================
(Disclosure: Matthew Butler and I work for the same company at this time of writing, and it's probable that our prior association may make me less likely to say mean things about him in this blog?
Also, he and Rainer Grimm did not receive any monetary compensation for my taking their classes. As a volunteer, the cost of your discounted class attendance goes entirely to the Gaylord, 
and apparently each day the Gaylord management needs $100/person to deliver a $25 lunch voucher and two snack periods...?  I guess those were some *really* expensive muffins/bagels at the morning snacks...)

After the conference, I took [Matthew Butler's](https://maddphysics.com/) class [Exploiting Modern C++: Building Highly-Dependable Software](https://cppcon.org/class-2019-exploiting/).
This was a [blue team](https://en.wikipedia.org/wiki/Blue_team_(computer_security)) focused class that focused mainly on software construction errors that can cause bugs in C++.
The introduction to [threat hunting](https://www.youtube.com/watch?v=pgEc__9Cltc) and the perspective of the [red team](https://en.wikipedia.org/wiki/Red_team)/threat-actors was interesting,
but the real highlight of the class were the discussions with other students on their experiences with starting or maintaining an [application security](https://en.wikipedia.org/wiki/Application_security)
presence in the [SDLC](https://en.wikipedia.org/wiki/Systems_development_life_cycle) of their respective companies.
Another highlight was the examination of some notorious C++ bugs (such as [Dirty COW](https://dirtycow.ninja/)), as well as what the results of undefined behavior look like under [Compiler Explorer](https://godbolt.org/).


Talks
=====

When I wasn't busy selling copies of [The C++17 Lands poster](https://fearlesscoder.blogspot.com/2017/02/the-c17-lands.html) at the conference store, I managed to attend talks during off-shifts and speaker-assisting time-slots. 
Having read some of the [existing trip reports](https://cppcon.org/milestone-new-home-trip-reports/) listed on the CppCon page, I'm not sure if an exhaustive list of the talks I went to is all that understandable to any reader (even if the reader is me from the future!).
Instead, I would recommend taking a look at the titles of the [talks uploaded to the CppCon Youtube channel](https://www.youtube.com/playlist?list=PLHTh1InhhwT6KhvViwRiTR7I5s09dLCSw) and reading the abtracts provided in the video descriptions.

That aside, what follows are my comments on a sample of talks I attended.

Matthew Butler presented another run of his C++Now 2019 talk, [“If You Can't Open It, You Don't Own It”](https://www.youtube.com/watch?v=WzKIev9ijQw),
which explores how layers in the Roots of Trust concept can affect the security of the applications we write,
even if we take the integrity of things like the supply chain of consumer hardware and the integrity of our compiler software for granted.
Between the CppCon and C++Now version of this talk, I would actually recommend the C++Now version as it has an extra half hour of content and may have been less compressed than the CppCon version.

[Preventing Spectre One Branch at a Time: The Design and Implementation of Fine Grained Spectre v1 Mitigation APIs](https://www.youtube.com/watch?v=ehNkhmEg0bw)
discusses the mitigations available for Spectre v1,
such as [lfence](https://newsroom.intel.com/wp-content/uploads/sites/11/2018/01/Intel-Analysis-of-Speculative-Execution-Side-Channels.pdf) insertions into assembly code
and [Speculative Load Hardening](https://llvm.org/docs/SpeculativeLoadHardening.html) of compiler output.
I thought that it was interesting that this talk suggests
[Chandler Carruth's CppCon 2018 talk on Spectre](https://www.youtube.com/watch?v=_f7O3IfIR2k) as "recommended background".
It's possible that depending on your preference of details-first versus overview-first learning, these talks can be watched in either order.

[Compiler Explorer: Behind The Scenes](https://www.youtube.com/watch?v=kIoZDUd5DKw) by Matt Godbolt was an update on the current challenges of running Compiler Explorer on the cloud, and also a demonstration of some lesser-known features (such as optimization threshold analysis by Clang).

[Abusing Your Memory Model for Fun and Profit](https://www.youtube.com/watch?v=N07tM7xWF1U) was a dense, code-sample-heavy talk that also explored how patterns such as separating thread creation from management, or "lazy futures" can be implemented as generic template algorithms. Worth going through slowly if you are interested in writing fast, concurrent code.

[Safe Software for Autonomous Mobility With Modern C++](https://www.youtube.com/watch?v=5WbdLUc9Jls) discusses the issues encountered when working toward
compliance with [ISO 26262](https://en.wikipedia.org/wiki/ISO_26262) for autonomous vehicle safety. Highlights covered the avoidance of memory allocations at runtime, and how use of large open-source libraries such as [Boost](https://www.boost.org/) or [POCO](https://pocoproject.org/) can utterly destroy your chances of ever passing code review qualification due to their massive scope.
This talk also provided another anecdote for the hazards of exceptions, as they can introduce branches invisibly, and cause gaps in branch coverage even when code coverage is theoretically 100%. This talk also recommended [foonathan's memory allocator framework](https://github.com/foonathan/memory).

At this point, it's been weeks after CppCon and I still haven't kicked this trip report out the door. As this post is growing into TLDR territory, it looks like it's time to turn this report into a listicle...

Recommendations from colleagues and friends:
============================================

The following is a list of talks that friends/colleagues saw and recommended, in no particular order:

* [Sean Parent “Better Code: Relationships”](https://www.youtube.com/watch?v=ejF6qqohp3M)
* [Andrei Alexandrescu “Speed Is Found In The Minds of People"](https://www.youtube.com/watch?v=FJJTYQYB1JQ)
* [Eric Niebler, David Hollman “A Unifying Abstraction for Async in C++”](https://www.youtube.com/watch?v=tF-Nz4aRWAM)
* [Chandler Carruth “There Are No Zero-cost Abstractions”](https://www.youtube.com/watch?v=rHIkrotSwcc)
* [Ben Deane “Everyday Efficiency: In-Place Construction (Back to Basics?)”](https://www.youtube.com/watch?v=oTMSgI1XjF8)
* [Conor Hoekstra “Algorithm Intuition (part 1 of 2)”](https://www.youtube.com/watch?v=pUEnO6SvAMo)
* [Conor Hoekstra “Algorithm Intuition (part 2 of 2)”](https://www.youtube.com/watch?v=sEvYmb3eKsw)
* [Phil Nash “The Dawn of a New Error”](https://www.youtube.com/watch?v=ZUH8p1EQswA)
* [Stephen Dewhurst “TMI on UDLs: Mechanics, Uses, and Abuses of User-Defined Literals”](https://www.youtube.com/watch?v=gxMiiI19VnQ)
* [Hana Dusíková “A State of Compile Time Regular Expressions”](https://www.youtube.com/watch?v=8dKWdJzPwHw)
* [Anthony Williams "Concurrency in C++20 and Beyond"](https://www.youtube.com/watch?v=jozHW_B3D4U)
* [Matt Godbolt "Path Tracing Three Ways: A Study of C++ Style"](https://www.youtube.com/watch?v=HG6c4Kwbv4I)
* [Ben Saks "Better Code with C++ Attributes"](https://www.youtube.com/watch?v=teUA5U6eYQY)
* [Bob Steagall "The Business Value of a Good API"](https://www.youtube.com/watch?v=S7gGtYqtNNo)
* [Corentin Jabot "Dependency Management at the End of the Rainbow"](https://www.youtube.com/watch?v=k3Q-fPBe9Z0)

Talks/resources from the past:
=====================================

These were talks and other resources that were mentioned at the conference, yet were *not* part of CppCon 2019. I figure it's a sign of staying power and relevance if a speaker goes out of their way to reference an older talk.

* [GoingNative 2013 C++ Seasoning - Sean Parent](https://www.youtube.com/watch?v=W2tWOdzgXHA) gets the top spot for being constantly mentioned in speaker talks and hallway conversations.
* [CppCon 2017: Louis Brandy “Curiously Recurring C++ Bugs at Facebook”](https://www.youtube.com/watch?v=lkgszkPnV8g)
* [C++Now 2019: Oded Shimon “Undefined Behavior - Not what you expected”](https://www.youtube.com/watch?v=QDxsf7Iv23w) is only 3 minutes and shows a baffling compiler optimization as a consequence of undefined behavior in the code sample.
* [C++Now 2018: Jason Turner “Initializer Lists Are Broken, Let's Fix Them”](https://www.youtube.com/watch?v=sSlmmZMFsXQ)
* [C++ and Beyond 2012: Andrei Alexandrescu - Systematic Error Handling in C++](https://channel9.msdn.com/Shows/Going+Deep/C-and-Beyond-2012-Andrei-Alexandrescu-Systematic-Error-Handling-in-C)
* Concurrent data structures are very hard to get right, but Rainer Grimm recommends [Max Khizhinsky's C++ library of Concurrent Data Structures](https://github.com/khizmax/libcds).
* [Herb Sutter's proposal for atomic smart pointers](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2014/n4162.pdf) was mentioned in both Rainer's concurrency class and Matthew's security class. The thing to remember about `std::shared_ptr<T>` is that while the shared_ptr is atomic-friendly, the `<T>` that it is holding is NOT protected.
* [How To Write Shared Libraries by Ulrich Drepper](https://www.akkadia.org/drepper/dsohowto.pdf) was mentioned in the [Milian Wolff “How to Write a Heap Memory Profiler”](https://www.youtube.com/watch?v=YB0QoWI-g8E) talk. Drepper is the same author of [What Every Programmer Should Know About Memory](https://www.akkadia.org/drepper/cpumemory.pdf) fame.

