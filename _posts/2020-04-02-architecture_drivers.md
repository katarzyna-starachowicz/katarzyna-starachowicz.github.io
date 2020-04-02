---
layout: post
title: My first architecture driver
date: 2020-04-02 21:32
summary: Architecture Decision Records in Architecture Decision Log
categories: software architecture drivers
---
In Poland – where I live and work – we have a pension system. My grandma doesn't have to work now to survive and she makes a living from her pension. But my situation won't be the same. Right now polish pension found receives about 50.000.000 PLN from government to pay all pensions. When I retire, the found will need 3 times more (according to the found itself). Right now there are two working people for one pensioner. When I retire there will be 0.8 working person for one pensioner. I'm going to receive the pension in the amount of 20-30% of my current salary.

Yep... So it's time to run a budget, including my own pension budgeting. And I definitely need an application for that. And here the chain of decisions finds its beginning. Software architecture decisions are determined by __architecture drivers__ which we can be divided into five categories:
1. High-Level Functional Requirements
2. Quality Attributes
3. Architectural Concerns
4. Conventions
5. Design Purpose

You should keep trying discovering your drivers because:
1. it saves time and money (you know exactly what are you building),
2. it helps to decide which technology are you going to use (there is infinite amount of them!),
3. you will get to know the real needs / purpose of the project.

The source of requirements, architecture drivers, are __stakeholders__. In this specific situation one stakeholder – just me.

It's good to write your architecture decisions down, because they are changing in time and can be various for specific parts of your system. For that I will use __Architecture Decision Records__. ADRs are just text documents, where you describe your decision. There is no one schema, how to do it[^1]. The list of your ADRs is called __Architecture Decision Log__.

I will keep my ADL inside `my_budgeting` project [repository](https://github.com/katarzyna-starachowicz/my_budgeting/blob/master/doc/adl). Let's start with `0001_record_architecture_decisions.md`.

# 1. Record Architecture Decision

## Status

Accepted

## Context

I start a public project for which architecture decisions can be seen as weird.

## Decision

I will record architecture decisions as documents in `doc/adl` folders – `documentation / architecture decision log`

## Consequences

The motivation behind previous decisions is visible for everyone, present and future. Nobody is left scratching their heads to understand, "What were they thinking?" and the time to change old decisions will be clear from changes in the project's context.
See more [here](http://thinkrelevance.com/blog/2011/11/15/documenting-architecture-decisions)


---

[^1]: Some examples you can find [here](https://github.com/joelparkerhenderson/architecture_decision_record)
