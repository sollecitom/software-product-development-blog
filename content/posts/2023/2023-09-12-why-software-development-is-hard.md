---
title: "Why software development is hard"
categories: [ "systems-thinking" ]
tags: [ "complexity", "software-development" ]
date: 2023-09-12T11:00:00
draft: false
---

We always hear that software development is hard, and that a very high percentage of all software projects fail. But have you ever wondered why software development is so hard?

I'm not considering software product development as a whole here, merely its software development aspects. Product development adds many other dimensions of complexity to software development, and I don't want to mix the two.

# Causes of complexity

Let's look at some causes for this complexity.

## (Mis)information abundance

Software development should be well understood by now. After all, we've been struggling with it for 50+ years at least, and there's a wealth of information about it.

You can read books, listen to podcasts, or watch videos, and there are classes and courses. You can often access all of this for free, or without breaking the bank in the worst case.

And if it's hired help you're looking for, you'd hardly struggle to find it: consultancies, contractors, advisors, coaches, and experts are at easy reach for the executive in need.

And yet, both doing the right thing and doing the thing right remain elusive. Despite all this information available, it's hard to know what to do, what not to do, and how to do things.

Books, courses, and other mechanisms to access information provide an analysis of the subject they concern themselves with. They break down the subject into its parts, and then analyze the parts, yielding knowledge of how the subject they treat works. Analysis never yields understanding ("why something works the way it works"), or wisdom ("what to do or not to do about something").

## A fast moving industry

The software development industry moves fast. Trends, frameworks, languages, open-source projects, security vulnerabilities, databases, build tools, packaging, distribution, Cloud services: they all come, change, and go fast.

It's not about keeping up with the latest fad. Technologies change all the time, but principles tend to remain the same. Sometimes, though, new technologies dramatically simplify or enhance something, leading to a paradigm shift.

When this happens, companies that don't adapt quickly find themselves at serious disadvantage compared to those that do. And just keeping track of what's new and what changed is a huge effort.

## Increasing expectations

Open-source technologies and Cloud providers have enabled software developers to achieve things that 30 years ago were impossible. And yet, this has raised the bar in terms of expectations on the software itself.

Distributed systems, virtualization, containers, orchestration, zero-downtime deployments, security vulnerability scanning, dependency management, runtime agents, upgrades, auditability, service mesh, responsive and accessible UIs, push notifications, horizontal and vertical scaling, idempotency, data residency regulations, multi-region availability, vendor-lock in, multi-Cloud, eventual consistency, encryption, GDPR, etc.

Layers over layers of requirements, expectations, integrations, and accidental complexity. This complexity, while accidental because not intrinsic to the business operations implemented by the software, is often unavoidable, because customer expectations and regulations are requirements the software must meet.

## Invisible quality and demand

The whole manufacturing industry is about demand and quality. You predict the variety of demand by looking at historical data, and you gear yourself up to meet this demand. Quality can be defined by how little you deviate from expectations. So if something is supposed to weight 50g, 49g and 51g are equally bad.

Service organizations can still look at historical data to predict demand, but they struggle with defining quality. A barber could record the frequency of hair types, requested cuts, and so on, but they'd struggle to measure the quality of their work. This is because, for service providers, quality is in the eye of the beholder. You cannot measure the quality of a barber, of a lawyer, or of a city planner.

For software development companies, unfortunately, even demand is an elusive concept. It might work for software development agencies that work on short contracts. These behave in a pretty similar way to a barber. But most companies aren't about short engagements. For most companies, at any given time, it's impossible to know what demand they'll experience, what quality they provide to their customers, or even what quality they have internally.

## Collaborative knowledge work

Software development is collaborative knowledge work. You have people with different strengths, experience, knowledge, roles, desires, agendas, and personalities. And they need to work together in a team, while often competing with each other over limited resources e.g. money, status, promotions, or attention.

People are systems, and their performance is hugely influenced by their state of mind, including focus, mood, psychological safety, and by how their needs are met by their job, team, company, industry, city, and personal life.

Teams are also systems, meaning that their performance is never the sum of the parts, but the product of the interactions between the team members, which are never interchangeable.

Companies are systems as well, and evolve continuously in terms of their employees, their position in the market, the level of resources they command, and their underlying view of the world, culture, and operating principles.

## Continuously evolving the same piece

Software development is not manufacturing. The teams don't build or produce anything. That's what the build pipelines are for. Teams develop software. Like developing a vaccine, a recipe, or an invention.

You continuously work on your software system, evolving it to meet changing and expanding requirements. And it's not a linear process either:

- Inputs come as requirements.
- The system evolves to meet these additional requirements, while also meeting all the previous ones.
- The new capabilities developed inform the future inputs, with expanding scope or rework.

# To sum it up

Overall, I believe the reason why software development is so hard is that it's about teams of people developing and continuously evolving software systems, to provide a service to their organization.

From this you get:

- Inability to quantify most things.
- All the complexities of systems: balancing and reinforcing loops, power laws, potential instability, higher order causes, change-resistant behavior.
- The complexities of social systems: the differences between people, the need to cooperate, the effect of incentives, the internal competition, the changes in management, hierarchy, market position, employees, worldview, culture, etc.
- The complexities of distributed software systems: technologies, requirements, integrations, vendors, regulations, trends, and threats: all ever-changing and moving fast.
- The interactions between social systems and software systems: Conway's Law, the effects that the quality of the codebase has on the people working on it, etc.
- The complexities of long-term horizons, and having to deal with the consequences of your decisions for a long time, with compounding effects.

# Parting words

Before ending this post, a few final considerations:

- In a complex scenario, best practices don't make sense. You never face the same situation, across either projects or companies. You probe, sense, and act. That's why there's so much information out there, and why it's mostly so useless.
- The internal quality of a software system determines the complexity and the effort involved in changing the system itself. The complexity and effort involved in an activity, in turn, determine the likelihood that a team might perform this activity. So bad systems are hard to change, require more work to be operated, and tend to get worse over time, as people pile up shortcuts over shortcuts.
- Software development is a continuous fight against entropy. Quality is the only way to achieve speed. Anything that destroys the pride a craftsman takes in their work is a major danger to any software project.
- The wrong incentives will favor internal competition and defensiveness, while destroying cooperation. This will also manifest itself in the processes and in the software systems of a company. 