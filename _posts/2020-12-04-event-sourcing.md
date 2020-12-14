---
layout: post
title: Event sourcing as side effect of event-driven architecture
date: 2020-12-04 17:34
summary: Beyound CRUD world
categories: event sourcing
---

When you start your journey with programming, you learn about SQL and Object Relational Mapping systems (like Active Record in Rails environment). And next when you think about blog post, you see database record which can be created (inserted), read, updated or deleted (CRUD). You operate on one record, on its last/current/only one state.

On the other hand – we keep our projects in Git, or to be more precise – we keep changes of our project in Git. In git history you can see who added some line of code, when another line was deleted. It's more like your bank account history, with saved deposits and withdrawals. And that is closer to just another way of persisting – event sourcing.

`Event sourcing` is another way of storing data. You store all the changes, all domain events. If you need to change/take a decision on the base of the current state of some entity – you need to fetch all changes, build the current state from them (event sourcing model: replay all domain events from an aggregate stream in correct order), apply new changes and publish domain event about these changes (run some operation, apply changes which produce new domain events). Thanks to that approach we remove Active Record from the decision-making process. In result domain logic is Rails free.

But remember – you restore the current state of the entity for reaching decisions. If you need just read the current state to show it to the user – then you use read models (about that in next part of this post).

There is a few great advantages of event sourcing:
1. Better debugulity of the application – you see what exactly happened there. You can restore the state of your application at any point of time you only wish. So you have not only the current state, but also all the past states as well.
2. You have the whole system history and audit logs "for free".
3. If you store domain events, you store users intention. You lose that intention if you keep just current state.
4. You avoid Object–Relational Impedance Mismatch just because you use event sourcing models.
5. With some experience of using event sourcing – it can be felt even more "natural/default" way of persisting data (see: how you think about your bank account history, or the current state of food in your fridge).

When you come from CRUD world, event sourcing implementation can be challenging at first. What if some mistake happened – you can ask. Well, then you just create compensate events (like refund invoice). You do not "migrate" / "fix" data in another way. And what if we want to change an event sourcing model and we need some kind of "migration"? For that, we will need to implement versioning of the models and events. There are patterns how to do it. And we will learn about it more in the future.

Please remember, we don't need to have event sourcing everywhere. Maybe we should use it only in the core domain?

Event sourcing seems to be a natural side effect of event-driven architecture. When you try to change legacy code into event-driven – you implement publishing events and reactions on that events. When your code is covered more with such approach – you start to have two sources of code: deltas of changes (events) and your traditional (ActiveRecord) entities records in database. In the end you don't need Active Record persistence. For views you will use read models, and for taking decisions – you can receive the current status from events. Event sourcing looks like a natural side effect of event-driven architecture (and auditing tools, history of changes etc. for free!).
