---
layout: post
title: Events, events everywhere
date: 2020-04-06 19:22
summary: Big Picture Event Storming as domain exploration technics
categories: ddd, event storming
---
It's time to establish what `my_budgeting` application should do through event storming sessions. However there are a few obstacles, with which I have to face.

The workshop should be conducted with domain experts, to who I don't have access. That's why I decided for __domain safari__[^1] – technic of learning domain by visiting places on the Internet where domain experts write or speak with each other and learning this way the domain (language). So, last year I read a lot of blog posts and articles about budgeting and now I know more or less how budgeting works[^2].

Because I'm writing this post during the COVID-19 pandemic, I decided to stay with online sticky notes on [Miro](https://miro.com/) board.

Today we are going to take care of domain events only. I hope today defined events will be in the future translated directly into the code. What are domain events?

> Domain events are structures describing what happened in your app. They are a gateway drug to enable lots of other techniques. Used correctly, they can be beneficial and valuable on their own for debugging (what the heck happened in my app, why did it behave like that…) and audit logging (who the hell changed this to that and caused all those problems that we have right now)[^3].

### Unstructured Exploration
Domain events are going to be represented by orange sticky notes. You write there in the past sentence what happened in your domain. Firstly I will create w bunch of them, just write down what first comes to your mind. In Miro application I can use `bulk mode` for that.

![Miro bulk mode](assets/2020-04-06-events-events-everywhere/bulk_mode.png)

After some time we have just a bunch of events:

![Bunch of events](assets/2020-04-06-events-events-everywhere/bunch_of_events.png)

### Timelines
Now it's time to sort the events in proper timeline order. By the way, if you already see some groups of events, why not group the sticky notes?

_![Events in order](assets/2020-04-06-events-events-everywhere/events_in_order.png)_

It's the simplest path for user interaction with the application. The new user registers, sets up timezone, budget concurrency and a virtual account. Then the application creates default budget schema (categories and group of categories) for the current (or feature ?) month. After that user budgets some categories, e.g. set 50 euro for the `cinema` category in the `entertainment` categories group. If the user buys tickets to the cinema for 30 euro, he records the payment. And that means, we have to adjust the category budget (50 - 30 = 20 euro).

I already know, there will be something more complex with setting budget goals, that's why I extracted the group of sticky notes for that topic, as well for... user payments for access to the application.

![Events in order](assets/2020-04-06-events-events-everywhere/goal_setting.png)

![Events in order](assets/2020-04-06-events-events-everywhere/access_payment.png)

As you can see, we use the word `payment` in two different contexts and they mean – from domain point of view – something different... We will go back to that when we will define `bounded contexts`.

### The review process
After you set all events in proper order – try to revisit events from the end to the start, form the right to the left. It changes your everyday routine of thinking about the business events flow consequently helps to validate the logic of a flow.

---

[^1]: The name of technic was borrowed by Andrzej Krzywda from salespeople who use sales safari. I learned about it on the Arkency course [Rails Architect MasterClass 3.0](https://arkency.com/masterclass/).

[^2]: I read mostly polish blogs, e.g. written by [Marcin Iwuć](https://marciniwuc.com/) or [Michał Szafrański](https://jakoszczedzacpieniadze.pl/). I learned English budgeting language mostly on the site of [YNAB](https://www.youneedabudget.com/).

[^3]: Robert Pankowecki & Arkency Team, “Domain-Driven Rails”, Leanpub 2016-2020.
