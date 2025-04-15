---
layout: post
title: "Thoughts on button push driven development"
date: 2019-02-24 09:19
comments: true
sharing: true
categories: Software Alexa
---

I was in a conversation the other day when someone mentioned

_"We may only be a couple Moore's Law iterations away from all software built by pushing buttons and WYSIWYG editors."_ 

This made me think of the software that we write today and the direction software is going. It also made me think of why I got into software and am still in this profession.

Lately, I have been very curious about voice as a computing platform and what that will do for applications we use in future. Thankfully, as software engineers, we don't have to hypothesize. We can build it.

Digging into Alexa skills development has been interesting. While the technical documentation and development for Alexa is quite good, I felt a fair amount of internal resistance during the project. The potential of this new computing platform and the possibilities it will bring kept me going.

![Yes Code](/images/yes_code.jpg "Yes Code")

The building blocks of working with Alexa are intents, utterances and lambda functions. After a series of thirty or so steps of wiring up buttons, copying and moving templates around, setting up attributes gives you a working voice enabled app, upload zip files, deploy it and submit for app review in the Alexa app store. 

Why did I feel the resistance? Any new tool or language will bring an initial set of frustration before we achieve a minimal level of proficiency. But Alexa development felt like using a software program rather than programming. It felt challenging the way gruntwork feels challenging and as opposed to intellectually stimulating. It also felt opposite to when I have felt the most joy during programming. When I had a strong grasp of the vocabulary of the language and the meta-language (libraries, development environment,runtime, etc), leaving room for higher level product/architectural decisions where most things are a tradeoff. This meant I had to do _very minimal context switching_. When writing an app for Alexa, it feels driven by context switching.

<!-- more -->

Continuous context switching has real penalties. In [Deep Work](https://www.amazon.com/Deep-Work-Focused-Success-Distracted/dp/1455586692), Cal Newport points out that the more time we spend effortlessly focusing on a difficult task, the happier we are. The ability to do deep work is one of the greatest joys of programming. So while using WISYWIG or code as configuration can lower barrier to entry for software development, they do take away the mindful aspects of programming.

That left me with the following thoughts.

1. Democratizing building of software applications is the direction in which software should go. _Just like literacy, tools of creativity should not be limited to those who have the time to learn or funding to hire people to do it._ If information hoarding is one's only advantage, one is asking for disruption.
2. _If solving problems is what gets you excited about programming, in the next decade you will want to think about focusing on areas more resistant to this change_. Infrastructure and tools development are more resistant to this change than application development, but there is less of it to be built compared to applications.
3. _Programming is still a difficult thing to do. Building quality, lasting software is expensive for a business._ For a business, the ability to reduce this cost by using WISYWIG tools or code as configuration will always be appealing.
4. WISYWIGs encourages dependence on higher level tools which reduces the need to learn about the fundamentals and increases the risk when the tools themselves break.

I hope this is a blogpost I get to laugh it in five years due to how much things have changed. But I do think this trend in software development has consequences as far as who will be interested in programming in the future and the intention people have when they get into programming.
