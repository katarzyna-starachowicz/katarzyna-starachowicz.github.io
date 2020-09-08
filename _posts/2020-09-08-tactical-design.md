---
layout: post
title: Tactical design – value object, entity, aggregate
date: 2020-09-03 07:34
summary: Explore system structure further
categories: value object, entity, aggregate
---

Every step in our business analysis journey brings you closer to coding. It's time to look for value objects, entities and aggregates.
Value object
`Value object` is something (object) to describe (value) something. In DDD we want to use meaningful objects instead of primitives. On code level – it's often a class keeping few attributes. For example: `30 EUR`, `vat rate` (0 can here have 3 meanings and we have to distinguish between them), `id`, `ActiveSupport::TimeZone`.
In My Budgeting project, we definitely need the `money` value object which describes amount and currency. Something like:
{% highlight ruby lineanchors %}
money = Money.new(300, EUR)
{% endhighlight %}
I would need to have also an `account`, defined as type of account, number, and the bank where it is, as well as currency.

If we want to describe value objects, we would need to think about:
Value object has no identity – 30 EUR can be used in many contexts and not be the same 30 EUR.
Values are comparable, so we can compare 30 EUR and 50 EUR, or 10 EUR and 10 DOL.
Value object is immutable – you cannot change the value object, you should replace it if needed.
Value object can compound attributes[^1]:
{% highlight ruby lineanchors %}
currency = Money.new(1000, "USD").currency
currency.iso_code #=> "USD"
currency.name     #=> "United States Dollar”
{% endhighlight %}

Entity
It's mostly what you have in `ActiveRecord::Base`, a domain object with a unique identity. Usually it has mutable state (it changes in time). For example, in My Budgeting core domain, we have: `user`, `budget categories group`, `budget category`, `payment`.

Aggregate
An aggregate is a bunch (a tree) of few entities, but can be represented by only one entity as well. The interface of aggregate elements is `aggregate root`. For example, we could have the whole budget aggregate. If we want to change only value of one category, we would need to do it through budget aggregate, where a category is one of the aggregate "leafs".
One transaction should change only one aggregate. We load the whole structure from a database, operate on that in memory (updates, removing/adding elements), and save the whole structure in the database. The role of aggregate is to protect certain business rules we always want to have true.
Vaughn Vernon suggest four basic rules of aggregate design:
>
1. Protect business invariants inside Aggregate boundaries.
2. Design small Aggregates.
3. Reference other Aggregates by identity only.
4. Update other Aggregates using eventual consistency[^2].

How to find the right sizing for aggregate is a topic for the whole book. I will try to touch this topic another time.

It's really hard to find aggregates without code, but for now I would say that in core domain my aggregates are:  `budgets account`, `budget category group`, `budget category`, `budget goal` and `payment`. Let's see how the implementation will change this approach.


---

[^1]: Example excerpt from: Robert Pankowecki & Arkency Team, “Domain-Driven Rails”, Leanpub 2016-2020.
[^2]: Vaughn Vernon, Domain-Driven Design Distilled, Boston 2016, p. 81.
