---
layout: post
title: Log4J Retrospective Discussion with the DC303
categories: [presentations]
tags: [security]
description: Slides from my ice breaker presentation for the January 2022 DC303 round table discussion on Log4J
---

To kick off the new year and fill a gap in the [DC303](https://dc303.org/) talks schedule, I volunteered to present an interactive [vulnerability retrospective talk](https://www.meetup.com/DC303Denver/events/281979560/) on the [Log4J RCE vulnerabilities](https://www.cisa.gov/uscert/apache-log4j-vulnerability-guidance).

The slides for the icebreaker presentation can be found [here](https://docs.google.com/presentation/d/1BROhgS3ZCeujD_HqIeioWeiJx-ULl2e1uZk5iixDqXg/edit?usp=sharing).

As the Log4J vulnerabilities have been covered to a great extent in video and textual form, I wanted to tailor this presentation to the live audience of the DC303 meetup.
We have visitors who are new to software security, come from a non-security technological background, or are just curious walk-ins, so I started the presentation with a summary and demo of the vulnerability.
Meanwhile, the group's core audience consists of a CTF team and study group, so the follow up topics focused on how future CTFs might incorporate the old Log4J vulnerability.

Much like how the OpenSSL [HeartBleed](https://heartbleed.com/) vulnerability [appears as a CTF target](https://ctftime.org/task/3370) years after it has been mitigated, it is inevitable that elements of this vulnerability will be used as inspiration for future CTF targets.
This is also why I added a section discussing how the JNDI lookup vulnerability was similar to other types of defects.  The idea was that while Log4J's vulnerabilities have already been mitigated, the fundamental concepts of untrusted lookups and coding marshaling/serialization will apply to other contexts.

Mark Hoopes a.k.a. [xync](https://twitter.com/mapkxync) also wanted to share his experiments with using [msfvenom's Java jsp_shell_reverse_tcp payload](https://www.infosecmatter.com/metasploit-module-library/?mm=payload/java/jsp_shell_reverse_tcp) to create a Java deserialization gadget, [inspired by this writeup](https://github.com/twseptian/Spring-Boot-Log4j-CVE-2021-44228-Docker-Lab), as he had just presented on the subject earlier in the week. We handled this collaboration by inserting the section "Mitigations that didn't work - Upgrade Java" (p21) into my slide deck, over which Mark discussed the background of his demo.  While Mark's part of the presentation is not expanded in my slides, as we developed our material independently, the background behind Java deserialization gadgets [has been covered by others in detail](https://medium.com/swlh/hacking-java-deserialization-7625c8450334).  One takeaway I found interesting from Mark's section of the presentation was that the core libraries of Java have been hardened against insecure Java deserialization, yet there are third party libraries that are still vulnerable to [custom gadget chains](https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-developing-a-custom-gadget-chain-for-java-deserialization).  His demo showed how this was also the case for Log4J at the time of controversy, despite remote class loading being disabled for both RMI (since Java 8u121) and LDAP (since Java 8u191).  Mark also happened to use [Rogue JNDI](https://github.com/veracode-research/rogue-jndi) as his LDAP server in contrast to my using [marshalsec](https://github.com/mbechler/marshalsec) for my demo.

The after talk discussion ranged across various topics such as:
* Additional discussion on Java insecure deserialization, and speculation on where else this may appear.
* The likelihood of other JNDI vulnerabilities not related to Log4J, in light of mitigations both recent (in response to Log4J) and historical (such as with Java 8u121 and 8u191).
* How this vulnerability could have extended life affecting embedded/[IoT](https://en.wikipedia.org/wiki/Internet_of_Things)) devices that are inconsistently patched.
* Brainstorming ideas for how this vulnerability may be customized as a challenge in a CTF.

The consensus amongst the group was that while this exact flavor of the Log4J JNDI vulnerability has already been mitigated, a lot of attention will be focused on the constituent ingredients of this topic, which will provide sporadic surprises to react to for the forseeable future.