---
layout: post
title: Crash Course Into The API Security Top Ten (2023) At Denver OWASP
categories: [training]
tags: [security, testing, api, owasp]
description: Thoughts on speedrunning the OWASP API Security Top Ten in less than an hour
---

I recently had the opportunity to fill in for the [July Denver OWASP Meetup](https://www.meetup.com/denver-owasp/events/294482375), as there was interest in reviewing the updated [2023 version of the OWASP API Security Top 10](https://owasp.org/www-project-api-security/).
If you're looking to learn more about the API Security Top 10, my recommendation is to learn from the best with APISec University's [OWASP API Security Top 10 and Beyond course](https://www.apisecuniversity.com/courses/owasp-api-security-top-10-and-beyond).  That said, [here are my slides from the event](https://docs.google.com/presentation/d/1Yw2DX3_jpNJNzW4s1Dx7oYtgk1yXMNglF02jQSeicwQ/edit?usp=sharing), and I'll cover some of the thought process behind developing a talk for this venue.

The amount of available time to cover the topic was the biggest difference between my talk and the online course I recommended, as the average allocated talk times for [Denver OWASP](https://www.meetup.com/denver-owasp/) range in the 30-50 minute range (while the APISec University course is advertised as 3-hours). That meant that I had much less time to cover each of the Top 10 items, and needed to be focused on what my goals were for audience takeaways.

In order to fit within the recommended 50 minute time budget, I decided to come up with 4 generalized summary points that reordered the Top 10 items into thematic groupings:

Allowing unreasonable access:
* API4:2023 - Unrestricted Resource Consumption
* API6:2023 - Unrestricted Access to Sensitive Business Flows

Forgetting to validate authorization:
* API3:2023 - Broken Object Property Level Authorization
* API1:2023 - Broken Object Level Authorization
* API5:2023 - Broken Function Level Authorization

Boundaries being bypassed:
* API2:2023 - Broken Authentication
* API7:2023 - Server Side Request Forgery
* API10:2023 - Unsafe Consumption of APIs

Lack of visibility or awareness:
* API9:2023 - Improper Inventory Management
* API8:2023 - Security Misconfiguration 


My thought process on reordering the top ten items was along these lines:

* The talk starts off with the impact of unrestricted API access on broadly relatable experiences such as trouble accessing overloaded websites and difficulty with acquiring frequently-scalped electronics like video game consoles.
* Authorization issues were the main focus of the talk and ordered earlier on, such that I could borrow more time from later sections if I ran long.  Also, these 3 categories related to the same theme of forgetting to validate authorization, where I went in order of increasing "size" of scope (the imperfect analogy is that object properties are aspects of a single user, objects relate to a full context of user's data, and functions could affect multiple objects/users).  I did run into an unexpected hiccup where there was some confusion regarding the idea of an "object".  In future versions of this talk, I plan to come up with an Object-Oriented Programming analogy to clarify this point.
* The items under "boundaries being bypassed" all related to the theme of vulnerabilities that happen due to some breach of the protective perimeter (firewalls, proxies, allow-lists), such that internal APIs are exposed to attacks. I agreed with the relative ordering of the 2023 list, as I finished this group with Unsafe Consumption of APIs as a general catch-all.
* And finally, I conflated issues with inventory management and security misconfiguration as lack of visibility or awareness. I introduced configuration as a subset of inventory to be managed, hence the switch in order.  I then closed the talk with a discussion of how automation and safe security defaults is becoming a general trend in advice, as manual interventions are subject to human error and difficulty to scale.


The idea of these groups was to highlight some of the shared themes of the individual Top 10 items, as well as to provide fewer more condensed takeaways that are hopefully even easier to remember.


The difference in venue from the talk I gave at [DC303](https://sunzenshen.github.io/training/2023/04/02/sharing-api-security-with-local-audiences.html) also influenced the summarized high level overview style of this version of the talk. The Denver OWASP meetup attracts a broader audience, including  leadership level roles in addtion to the technical contributors I usually target my talks at. The sponsors of Denver OWASP also provide an open bar for guests, which encourages a more relaxed social atmosphere than the study group tone of DC303. 

With those factors in mind, I felt that it would be easier to follow for everyone if I focused more on the shared thematic themes of the Top 10 items, rather than drilling down to the technical details like last time.  Admittedly, another reason was that my last talk at DC303 lasted 2 hours, primarily due to the interactive demos, so I knew I had to trim a lot of fat from how I organized my last talk in order to have any hope of fitting in the recommended talk time.

Reception to this presentation style was reportedly positive, according to friends and coworkers who attended in a show of support. Even though I still struggle with impostor syndrome for being the one to deliver this talk locally, as one attendee said: It's not like Corey Ball is going to present in Colorado soon.  (But we would all be extremely happy if the preeminent expert could come visit!)  And regardless of whether I feel like people are just being nice with positive feedback, I suppose I didn't do *that* badly, as I am discussing with [Boulder OWASP](https://www.meetup.com/OWASP-Boulder/) and work to schedule refined versions of this talk in future months. As usual, if you have any questions about the presentation content, feel free to reach out!