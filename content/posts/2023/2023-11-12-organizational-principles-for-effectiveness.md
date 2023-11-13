---
title: "Organizational principles for effective software product development"
categories: [ "management" ]
tags: [ "system-thinking", "management", "effectiveness", "startups", "organization-design" ]
date: 2023-11-12T05:00:00
draft: true
---

I often discuss what's wrong with an approach, practice, or system. Today, for a change, I want to clarify some principles that an effective software product development company should adopt.

Why principles? Wouldn't a detailed description of how things should work be more useful?

It'd be almost impossible to write, as it's a colossal task. Perhaps it'd be good for a book, but definitely not for a blog post.

Also, reality is multifaceted and nuanced. Everything depends on everything. Prescriptive approaches cope poorly with dynamic situations. Principles, on the other hand, allow you to deal with uncertainty, and guide your decision-making by cutting out the noise.

# How to use these principles

You can use these principles to design how a whole company operates. When choosing tradeoffs, approaches, and practices, check whether the element you're designing violates one of the principles. If it does, design an alternative approach that doesn't.

The principles work in synergy, so the value they bring when implemented together is more than the sum of the parts, but they're individually useful. That means you can apply them to designing not only whole organizations, but also departments, areas, and teams.

At the very least, they provide a framework to evaluate how effective a company or a team is.

# Applicability

Like any model, these principles have specific applicability boundaries. They're only useful when:

1. There's a willingness to strive for excellence. If a company is content with doing okay, some of these will sound extreme or dangerous.
2. The results are placed before what's better for some people. The non-goals include keeping people in their comfort zone, supporting control structures, and feeding people's ego.

# Principles

## Outside-in organization

Employees work across different levels. Activities range from being closest to the customers, to the innermost level. The time horizons tend to widen as the levels get further from the customers.

The inner levels support the outer levels. It's about coordination, not command or management. The outer levels can pull help from the inner levels, but the decision-making stays with the people working as close as possible with the customers.

The opposite of this is the traditional top-down organization, where each level controls and manages the level below.

## The team as the unit of work allocation

Work is carried over by teams, rather than by individuals. This means that nothing is allocated to a specific one person.

A team is a group of people working together towards the same goal. Sharing a goal is not enough, people need to collaborate synchronously towards achieving it. Ensemble programming is a great example of a practice that embodies this principle.

## Small equivalent teams

Teams should be as small as possible, while still qualifying as a team. A team must abstract who's doing what, be capable of doing any work, and be resilient to absences.

To do so, teams should be cross-functional and staff people with different backgrounds and strengths.

About backgrounds, you want a mix of old and young, senior and more junior, academic and self-taught, genders, etc. In terms of personalities, you need shapers, fixers, and explorers. When it comes to skills, you should at least cover web development, user experience, distributed systems, codebase structure, Cloud infrastructure, databases, product discovery, scripting, observability, and code maintainability.

I believe teams of four or five people can achieve the requirements above, without splitting into more than one team. People are not interchangeable, and the same person will complement a team and not fit in others. Hire for the specific skills/strengths/personality/background you need in a specific team.

## Work-in-progress limits

Each team should be working on only one initiative at a time. So the number of teams you have is the degree of parallelism you get. Not everything counts as an item though, only high-level product or technical initiatives do. So a team is always improving various things, but only working on a significant piece of work at a time.

## Pull-based just-in-time work

The teams should pull work when they become available. As a team finishes working on an initiative, they should pull the next initiative and start working on it. This means that teams cannot get overwhelmed by work pushed on them. Information about upcoming work shouldn't reach a team until that team has finished the current initiative. 

## Pull-based information

Information should also be pull-based, made available when and if a team or a person needs it. Documentation, expertise, advice, support, etc. should all be accessible when needed by anybody.

## Leaderless teams

A team should be a group of equals who are great at different things. Nobody should be the designated leader of the team. Seniority shouldn't formally matter. The team can self-organize in terms of representation when dealing with stakeholders, but nobody should be allowed to represent indefinitely.

## Company-wide initiative queues

TODO

##### TODO

- Evolutionary approach (set-based approach and different ways, over standardization and efficiency)
- Salaries and incentives
- Executives
- Releases happen every day (Fridays included)
- Learning on the job
- Continuous collaboration
- Working hours (5 hours a day of collaborative work, plus learning activities; unlimited holidays, minimum 30 a year + national holidays)
- Titles and promotions
- Exactly one environment (production, with internal tenants and users)
- Continuous delivery (integration, delivery, and deployment)
- Experts are available as advisors (the team calls experts to help them; the teams keep the decision-making) (architecture, product discovery, product observability, etc.)
- Initiative queues
- Nobody manages people (for holidays, etc.)
- People align vertically (within the value stream, rather than within their function)
- Products, not projects
  - No budgets (allocate money when and if needed, never freeze it)
  - No estimates (build first and sell second, never tell customers when things will get done)
- Teams own the way they work (hiring, firing, onboarding, practices)
- Collective code ownership
- Collective product ownership
- Initiative DRIs (direct responsible individuals)
- Cross-function training (for developers: finance, marketing, product management, design, sales, business, domain expertise; for others: similar including programming)