---
layout: post
title: Additional Resource Recommendations for the Beginning Secure Software Practitioner
categories: [recommendations]
tags: [C#, security, OWASP]
description: I passed a cert! But can't talk about it, so let me steer you to related resources instead!
---

I recently completed (ISC)2's [Secure Software Practitioner - .NET](https://www.youracclaim.com/badges/b63c3ea0-449c-47f9-8394-43356f0f7845/public_url) course, along with the associated exam.
It's an achievement that I find awkward to boast about, given the mixed feelings about certifications in general,
especially regarding the controversy of whether they are effective for teaching and evaluation.
That said, I learned a lot just studying for the exam, and am grateful for my employer signing me up for the course.
Given that I signed an NDA for the exam itself, I struggled to come up with a way to celebrate on this blog while having something meaningful to share.

Along the way, I ran into the a bunch resources that helped add perspective to the topic discussed.
I don't kid myself as being any more than a newbie regarding security topics at this point,
but I wanted to share a couple recommendations specifically tailored for beginners.
Other, more qualified, experts have their own comprehensive guides,
but I hope these two sources are an approachable start for those who would like to begin exploring in a safe environment:

Live Overflow
-------------
* https://liveoverflow.com/
It's one thing to get an overview and demonstration about a threat or exploit,
but that's a separate thing from learning the mindset of how to probe a black box of a system.
I really enjoyed this Youtube channel for its informative background explanations of binary hacking and web application exploitation,
along with the detailed breakdown of concepts applied in the CTF exercises.
The narrator's humble but passionate attitude is also a warm welcome for such a daunting topic.

OWASP WebGoat (and Zed Attack Proxy)
------------------------------------
* https://www.owasp.org/index.php/Category:OWASP_WebGoat_Project
* https://www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project
A narrator can talk your ear off about the [OWASP Top 10](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project) over a set of lecture slides,
but I find that the "what's the harm?" question is better answered with hands on experimentation.
You can learn a lot just from reading the solution writeups, and then playing with the scenarios interactively.
I particularly appreciated the exercises where you crafted malicious E-mails and comments to plunder imaginary bank accounts and admin credentials.
Remember to unplug your internet or isolate your VM, as running an insecure web service on your computer is about as unsafe as it sounds.


That's it for now!
------------------
I could naturally go listing other neat sites such as [microcorruption](https://microcorruption.com/),
[cryptopals](http://cryptopals.com/),
and (XSS game)(https://xss-game.appspot.com/),
but tackling those challenges without prior context can be like trying to walk through a brick wall.
Hopefully the above "list" is small enough that the idea of tackling it seems manageable, even inviting!

In the meantime, if you want to ask me about anything more specific,
or to lay some frank feedback onto me,
you can reach me on the usual channels as always. :)
