---
layout: post
title: How much bounded should be the context?
date: 2020-05-11 23:03
summary: What is bounded context and how to validate it
categories: ddd, event storming, bounded context
---

> DDD is primarily about modeling a Ubiquitous Language in an explicitly Bounded Conetxt[^1].


In our last pig picture event storming we already found some elements of budgeting ubiquitous language, like `budgeting`, `payment recording`, `budget goal setting`, `budget category`, `budget categories group` etc. We found also, that there are words used in different contexts which means something different – `payment` for example.

When we say that `user records payment` – it's no the same payment, when we say that `proof of payment is sent via e-mail`. The first one is in `budgeting` bounded context and means that the user spent some of the budgeted money: event `payment recorded` changes the user's budget. The second one stays in `accounting` bounded context and means that some money (let's hope, also budgeted by user) came to my company account and now my company must issue an invoice and send it to the user.

By the way – from the outside perspective it can be "the same" money! So, user budgets 10$ for our app fee (budgeting context, because it changes budget state), pays the fee (accounting context, because it triggers some accounting processes), and records the payment (budgeting context again, as it changes budget state).

> The Bounded Context is a central pattern in Domain-Driven Design. It is the focus of DDD’s strategic design section which is all about dealing with large models and teams. DDD deals with large models by dividing them into different Bounded Contexts and being explicit about their interrelationships.
As you try to model a larger domain, it gets progressively harder to build a single unified model. Different groups of people will use subtly different vocabularies in different parts of a large organization. The precision of modeling suffers, often leading to a lot of confusion. Typically this confusion focuses on the central concepts of the domain[^2].


__Bounded context__ is a sub-system of our system. It has clear boundaries (`bounded` context) which are linguistic boundaries. Concepts are clear inside these boundaries (bounded `context`), every one context has its own ubiquitous language, has its own specific language for solving its problem, has its own domain model.

When the company is big we can often map organisation department to one bounded context. If My Budgeting company would be huge – we would definitely have many people responsible for product maintenance and evolution, and they would be grouped into department responsible for:

1. `accounting`: integration with payment gateways, issuing and sending invoices;
2. `budgeting`: handling (create, update) the budget;
3. `reporting`: learning about money spending habits;
4. `subscription`: managing subscriptions (plans, access to the budget).

Thus these 4 would be my bounded contexts.

### Context boundaries validation
If we are not sure if our boundaries are defined correctly, it's good to validate context boundaries. There is a few hermeneutics we can use here.

#### 1. Context Autonomy
Bounded context should be able to make decisions autonomously, shouldn't ask for permission from another context.

#### 2. The number of contexts in business process
The more bounded contexts are involved in one business process, then worst it is.

#### 3. Look for information changed together
If there is information which should be always changed together, then we have probably one bounded context.

#### 4. Look for information used together
If we have information used together, we probably have one bounded context.

#### 5. Ask questions:
1. What is the responsibility of the context?
It should be described in on or few simple sentences. I already did it above.

2. How many integrations has the bounded context?
Outside integration makes autonomy weaker than inside integration (integration to some module/service developed inside the company). And what is the reason for integration?

3. Is there the one source of truth for some business concept?
If we miss the source of some business concept, it means we probably miss some bounded context.

4. Is there any schizophrenic context?
If any context must check the same rule (e.g. if the user is a private person or a company), then it means that the context does not know what it is. And we probably have two bounded contexts.

#### 6. Look for anti-requirements (breaking the boundaries)
If there is a requirement that does not have a sense – it's anti-requirement. If there is something like that, it means our boundaries are invalid.


After consideration I see (5.) `payment` as an additional autonomous bounded context.
* It is responsible for money transferring.
* It has its own data: only payment context must know user bank account or transfer title.
* The app will need to be integrated with the payment gateway. Application access to the payment is crucial for the business and thus we need a dedicated focus on that topic.


---

[^1]: Vaughn Vernon, Domain-Driven Design Distilled, Boston 2016, p. 11.

[^2]: Martin Fowler, http://martinfowler.com/bliki/BoundedContext.html.
