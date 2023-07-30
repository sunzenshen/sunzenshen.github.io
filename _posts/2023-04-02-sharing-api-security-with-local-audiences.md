---
layout: post
title: Tailoring API Security Talks For Local Audiences
categories: [training]
tags: [security, testing, api]
description: The challenges of trying to condense weeks worth of reference material into an hour or two for local audiences
---

Recently I have been exploring the topic of API security, in part due to the recent wave of interest that followed the release of the book ["Hacking APIs by Corey Ball"](https://nostarch.com/hacking-apis).
After recommending the book to colleagues, they encouraged me to give a brown bag style talk introducing the topic, during my workplace's quarterly learning days.
Admittedly, I still struggle with the idea that people would want to watch a local talk instead of diving into the original expert source material, but I took the recommendation as a concrete challenge to reinforce my learning.
If you are interested in the topic, I wholeheartedly recommend checking out the free [API Penetration Testing course](https://www.apisecuniversity.com/courses/api-penetration-testing) presented by the book's author at [API Sec University](https://www.apisecuniversity.com/).
If you complete the course, you even get a shareable certification link, just like [my version of the cert.](https://www.credly.com/badges/cd6548e2-ec90-4a8a-b587-dd8a6f206570)

I ended up delivering two versions of an intro to API security crash course between work and the [DC303 meetup](https://www.meetup.com/dc303denver/events/wgcpkqyfcfbgc/).
It was a bit of a challenge adapting the source material of the book to either venue, as there was a wide variety of backgrounds comprising both audiences:

* At my workplace, the audience and I had the benefit of being able to review and discuss examples of API security vulnerabilities and mitigations that happened in past work projects.  Naturally I had to cut out all of those references in the [talk slides tailored for the DC303 meetup](https://docs.google.com/presentation/d/18i8yEngeiT8tL4uuXI0wPdYlNiPoUfdEBr6tsanognI/edit?usp=sharing), and instead needed to rely on public news stories and intentionally vulnerable test applications like [crAPI](https://github.com/OWASP/crApi) as the source of examples. 
* When tailoring the talk for work, I decided to dedicate the first part of the talk on a high level overview of API security, and to then dedicate the latter part of the talk towards an engineering audience (with the assumption that anyone else could conveniently remember they had a conflicting meeting they needed to get to). 
* In order to focus the scope of the DC303 talk, I made the assumption that most of the audience would be interested from a penetration testing perspective. While there were some seasoned security testers in the DC303 audience, there were also a number of engineers and developers who attended due to a curiousity about the topic. With the latter audience members, we ended up discussing many of the same mitigations that the work-tailored talk touched on, just without specific examples.
* Because I only had an hour to give a talk at work, I recorded demos of API vulnerabilities in order to present them with controlled timing.
* At DC303, we had more time (2-3 hours), so I prepared VirtualBox snapshots of the vulnerable applications to work through testing examples live with the audience. Just in case, I recorded practice runs of the demos and [posted them on YouTube](https://www.youtube.com/playlist?list=PLQnQlEXScAsISjne6s7yAa2Gcr9SEPTvg) in case I ran into demo complications.

At both venues there was lively discussion amongst the audience, of API security related anecdotes from our own experiences.
In particular with the DC303, Mark Hoopes a.k.a. [xync](https://twitter.com/mapkxync) was generous in sharing stories (in broad, anonymized strokes) of some of the API vulnerabilities he has seen in production applications during security testing jobs. The audience engagement was a pleasant surprise, and I recommend giving similar talks to help spread what you've recently learned.

In reflection, here are some reasons why you should consider sharing what you know with your local community, even if you are not the preeminent expert of the topic you would like to share:

* While my initial belief was that learners would be better off diving into the original source material published by experts, people still want to gather as a group to discuss topics they want to learn together. Somehow, I had forgotten that there is lasting appeal to groups like book clubs for this purpose.
* As long as you are transparent about the source of your primary reference material, local venues won't mind that you are not the primary source expert. This is especially true if your event is free to attend, or if you're helping your local meetup organizer fill open slots in the year's meeting schedule.
* With recent interactions, I've realized that oftentimes in-person locals like you or me are more approachable for questions and discussion than strangers known industry-wide. This is even true if your local community organizers are already in direct contact with said experts, because the latter experts may have scheduling/priority conflicts that make it unlikely that they can engage with your community in the short term. And oftentimes people want to ask for a recommendation of learning sources from someone they can ask follow up questions from, before investing hours and weeks of time with the source material.

The common thread is that you can't discount how helpful it is to have a present person to ask questions of.  Even if there's a plethora of highly produced and always-available learning content available on the internet, it's still valuable to meet and discuss with other learners.  That is why it's possible to have a positive impact in your local community, just by sharing what you've learned.
