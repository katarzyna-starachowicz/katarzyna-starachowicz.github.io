---
layout: post
title: Event storming solves all your problems
date: 2020-03-23 19:22
summary: Event storming as domain exploration and domain model creating technics
categories: ddd, event storming
---
There are two patterns to build domain models – tactical and strategical. __Tactical patterns__ focus on on building blocks of domains model (value object, entity, aggregate, domain event, design patterns like repository, factory, strategy). __Strategic patterns__ focus on concepts, communication, definition of ubiquitous language (bounded context, context map, core and sub-domains).

And there are many ways to explore domain and build domain models. It's not easy to gather that knowledge in one place. In my current company my team is responsible for extracting part of existing application into separate service. The problem we encountered was that the majority of the team didn't know the selected bounded context. Our first approach was that everyone singly was responsible for digging into some small part of the code and explaining it to the rest of the team. But after that we still had fragmented knowledge, no idea how to put it together into one simple system (the idea was not only to extract but also to refactor the code).
Finally we decided to conduct event storming. In few hours of meetings we all not only know what's going on from business point of view, but we also were able to translate domain process into code architecture (more or less..., you know, it's still in progress).

I fell in love with __event storming__ because it's visual and comparatively easy to understand. It's not technical (domain), but easy way to the code structure. It builds common understanding of domain (ubiquitous language) by engaging everyone in discussion.

How does it work? We invite domain experts ("business people") and developers[^1] into one room where they gather their knowledge about domain in sticky notes on a wide wall by asking questions and answering for them. Everybody is involved into the process overcoming obstacles of "too expert" or "too technical" language. The business process is "stormed out" as a series of domain events which are denoted as orange stickies[^2]. It's chaotic process, so it's good to have somebody with facilitator role – the person responsible for making this chaos working.

![big picture session](https://github.com/mariuszgil/awesome-eventstorming/blob/master/assets/timelapses/timelapse-1.gif?raw=true)

Mostly we start with __Big Picture Event Storming__ to see the project domain from above. Next we run into __Design Level Event Storming__ when developers translate domain knowledge into code structure.


---

[^1]: I'm focusing here on creating / refactoring software applications. But event storming can be used in all other context.

[^2]: See more on [page dedicated to event storming](https://github.com/mariuszgil/awesome-eventstorming)
