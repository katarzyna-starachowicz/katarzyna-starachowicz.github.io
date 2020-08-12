---
layout: post
title: What the domain?!
date: 2020-08-12 07:49
summary: Find the domain, define the bounded context
categories: domain, domain model, bounded context
---
We're trying to figure out what is Domain Driven Design. We already learnt that we should write down and use "the dictionary" of ubiquitous language, that there are strategic and tactical patterns to discover domain model and that event storming can help to explore the domain and create the domain model. But what exactly is the domain and what's the difference between `domain` and `domain model` or `domain` and `bounded context`?

> [Just a reminder:] According to the principles of Domain Driven Design, efficient software design requires knowledge of the business domain and the ability to model its problem domain. Discovery and modelling of domain knowledge is a strategic design.

According to [Cambridge Dictionary](https://dictionary.cambridge.org/dictionary/english/domain) domain is `an area of interest or an area over which a person has control`. I would say not only a person, but also a company. To keep it simple, a domain is that in which the company deals, which gives the company money.

### Core domain and subdomains
Mostly there is one core domain and several subdomains in our projects. __Core domain__ is a business differentiator – defines the business. It's an answer to the question, why the system (application) is built, why it's not just bought. For the My Budgeting company `budgeting` is the core domain. The goal is to make money on allowing users to manage their money. And the application for budgeting is built from scratch, because there is no other satisfying solution on the market right now. The My Budgeting company managers know the secrets of the best budgeting way and that's the ground of their business. In this area, developers (as well as managers) should spend the most of their time and it should be their main focus.
__Subdomain__ can be supportive or generic. __Supportive subdomain__ supports (what a coincidence!) the core domain. It cannot exists without a core domain and makes no sense without core domain. Finally, there is no existing product providing the same functionalities. For budgeting supportive domain is `reporting`. Of course, there are existing tools on the market for reports, but reporting in My Budgeting company is super intelligent, reports not only already budgeted and spent money, but also predicts the future plans and expenditures. What' more – explores the financial personality of the user which allows to reshape users financial habits and in result conquer the world (when it's not about money, it's always about power).
__Generic subdomain__ on the other hand provides ono-unique solutions, mostly already existing on the market. Here we have `accounting`, `payments` and even `subscription`.

Domains can evolve. Right now budgeting is our core domain, but similar solutions proliferate in the market and someday the "the reporting" can become the differentiator of our business. Our application will provide recipients how to change financial personality and habits to achieve defined by the user financial goals. What's more, maybe we start development with budgeting as a supportive subdomain (we can even use already existing tools) and focus on budgeting topic. And we are going to expand the meaning of budgeting in the future – then a supportive domain would undergo a metamorphosis into the core domain!

Discovering (sub)domains helps to understand how the business works. It divides the problem into sub-problems – it is always better to face smaller problems. Furthermore, from a technical point of view, we can use other tools to different kind of subdomain.

### Subdomains discovering heuristics
If you are not sure how to find subdomains, you could use one of the heuristics:
#### 1. Take a look at your organization structure.
The boundaries of departments are equal to boundaries of subdomains (for sure it's tricky to do in startup like My Budgeting :) )
#### 2. Take a look at domain experts
There are people responsible for the idea of budgeting, for the proper structure of the invoice sent to clients, and another one – for technical problem of online money transfer.
#### 3. Listen to the language of domain experts
A money transfer means something different for a person responsible for the integration of a gateway and person responsible for the concept of budgeting.
#### 4. Ask question – what gives a big business value
Real money transfer – provide real money for the company, money transfer as the part of budgeting concept – attract new clients.
#### 5. Take a look at business processing steps

And always remember – the domain model is permanently changing.

### Domain model
>  The model is a set of concepts built up in the heads of people on the project, with terms and relationships that reflect domain insight[^1].

The domain model is a solution of domain problem. A set of concepts creating a common understanding. The model can be presented in many ways – for example as a code, as an implementation.
The model does not solve the problem. It's like a map – it shows how to find a way to the goal. It does not present the real one to one, it shows only some aspects of reality abstractly.

### Subdomain vs bounded context
The domain model is embedded in the bounded context. Bounded context is a solution. After we found the subdomain – we are able to define the bounded context.


---

[^1]: Eric Evans, Domain-Driven Design. Tackling Complexity in the Heart of Software, New Jersey 2003.
