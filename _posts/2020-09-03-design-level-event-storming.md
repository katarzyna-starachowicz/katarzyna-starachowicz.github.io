---
layout: post
title: Design Level Event Storming
date: 2020-09-03 07:34
summary: Explore system structure
categories: command, actor, policy
---
Big picture event storming – as the name suggests – supports exploration of business domain horizontally, allows to create a big picture of the domain. Here we cluster events in [bounded context](https://katarzyna-starachowicz.github.io/bounded-context) as well. Events in big picture event storming forces us to think about system behaviour, not system structure.

After small [introduction](https://katarzyna-starachowicz.github.io/event-storming) and conducted [Big Picture Event Storming](https://katarzyna-starachowicz.github.io/events-everywhere) (unstructured exploration, setting timeline order and review process) – it's time for the next steps.

In `Design level event storming` we explore one bounded context. It means we can invite less people to the meeting: experts of only one subdomain, developers responsible for the implementation of a part of the system. We explore here design elements which will build a domain model. There are no strict rules about notation here, but still we can follow some [common usage of sticky notes colours](https://github.com/mariuszgil/awesome-eventstorming).

### Commands and actors
When you have the event flow defined, you can start looking for the triggers of the events. There are many types of them. The most obvious are `commands` therefore we are going to focus on them for now. Commands in Pig Picture Event Storming are described in imperative on blue sticky notes and represent intention. The commands are called by `actors` symbolised by light yellow sticky notes. In My Budgeting core domain, the actor is mostly the user.
![core domain events flow triggered by user](assets/2020-09-03-design-level-event-storming/core-domain-events-flow-triggered-by-user.png)

Not all events are triggered by user commands. Some of them are `scheduled`. For events of this type, we draw a calendar on event sticky note (see next event flow picture).

### Reaction and policy, external systems
> A `reaction` is something that needs to happen after something else happens. Reactions are best captured in the following statement,
“**This** happens **whenever that** happens”.
`This` is the reaction. `That` is the event. `Whenever` is the word that associates an event to a reaction to create a `policy`.
If you find yourself using the term `whenever` to describe a sequence of events, you’re speaking in terms of a event-driven system. The order of these statements is less important than the contents of the statement[^1].

After a My Budgeting app user sign up – the free trial expiration is scheduled. Whenever free trial expired the access must be paid. Payment is triggered in an `external system` (pink sticky note). We have two policies – depending on the payment result. If payment is successful access invoice is issued and sent to the user. If payment fails information about failed payment is sent to the user and access to the My Budgeting is blocked.

![scheduled payment event with policy](assets/2020-09-03-design-level-event-storming/scheduled-event-with-policy.png)

### Why we need Design Level Event Storming?
During the design level event storming session, we explore domain language further and business policies. We keep common knowledge visualisation. Last but not least, it's just the easiest and cheapest (sticky notes on the wall!) way of exploring different models, move commands, business rules, adding or removing policies.

---

[^1]: Kevin Webber, [Modelling Reactive Systems with Event Storming and Domain-Driven Design](https://blog.redelastic.com/corporate-arts-crafts-modelling-reactive-systems-with-event-storming-73c6236f5dd7).
