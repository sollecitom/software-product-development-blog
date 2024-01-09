---
title: "Interdependencies in your system of work"
categories: [ "system-thinking" ]
tags: [ "system-thinking", "Agile", "effectiveness", "software-development", "technical-processes" ]
date: 2024-01-08T05:00:00
draft: true
---

I keep hearing people claiming their team tried Trunk-Based Development, and decided they didn't find it beneficial after a couple of months. Now, I love TBD, but today I'm not going to war about it.

The problem with this kind of statement is that Trunk-Based Development is a part of a system of work. And the performance of a system is never the sum of its parts, but the product of its interactions.

So you cannot look at Trunk-Based Development, a practice, and assess its performance in isolation from its containing system. This makes no sense whatsoever.

Experiencing something without a containing system is also impossible. So when people say they tried Trunk-Based Development, what did they actually do? They probably attempted to work directly on the main branch, as the only change to the way they were working before.

Even assuming they understood what TBD is and how it works, ideally with an instructor, what are the chances that "improving" a part of a system improves the performance of that system? Pretty much zero. Things almost always get worse.

When you introduce any practice, Trunk-Based Development is just an example, to the way you work, you're implicitly creating a new system of work. And that's what you experience in terms of performance. Not the merits of TBD, but the merits of your overall new work system.

It's as nonsensical as replacing a small airplane's thrusters with a helicopter's rotor, witnessing the poor thing crash, and concluding that rotors are a bad idea. As it goes for the airplane, what are the chances that swapping a part of a system with a part of another system significantly improves things: zero.

## The system of work



[//]: # (TODO index)

- Ensemble programming, TDD, TBD, CD, DDD, etc. can be useful, but they're not goals on their own.
- The goals are:
    - Effectiveness: doing the right thing, meeting the needs of the customers and of the company, delivering value earlier.
    - Safety: not breaking things in production, security, compliance, etc.
    - Sustainability: no heroics, no sprints, no borrowing from the future, no increasing the effort required, etc.
    - Resilience: coping with temporary absences, late changes in requirements, etc.
    - Efficiency: avoiding non-value activities.
- It's a sociotechnical system made of people, processes, and technology systems.

- System:
    - A cross-functional leaderless team of four product developers:
        - Backend, web, infra, mobile
        - Settler, explorer, town planner
        - Creativity, execution
        - Starters, finishers
    - The team members work with ensemble programming, synchronously together on the same task.
    - They structure their distributed system using an event-driven architecture (service choreography, CQRS, event-sourcing, event-store).
    - They use explicit Bounded Contexts and Context Maps to plan the architecture, from Domain-Driven Design.
    - They use hexagonal architecture for each software component (driving and driven adapters, application, domain).
    - They adopt a programming language with a sophisticated type system.
    - They use Aggregate Roots, Entities, and Value Objects to model the domain of each Bounded Context, from Domain-Driven-Design, aligning the language used with how the business calls things.
    - They maintain shared libraries with implemented patterns, utilities, and a thin Shared Domain.
    - There's a company-wide registry of contracts e.g., OpenAPI, Avro, Kafka/Pulsar topics, etc.
    - They pull work from a company-wide queue of initiatives, and operate with a work-in-progress limit of 1.
    - They use outside-in Test-Driven Development to develop their internal modules, with clear contracts and example tests at module boundary's level.
    - They adopt a build system able to only rebuild and retest the modules that actually changed (using hashing).
    - They have a series of service-level tests and checks they can run locally:
        - Application tests: application against stubbed driven adapters.
        - Integration tests: driving adapters against their inbound contract e.g., OpenApi or Avro and against a stubbed application. Driven adapters against their target technology running in Docker through TestContainers.
        - In-process service tests: the whole service going from driving adapter to driven adapters and back, against technologies in Docker.
        - Container-based service tests: the whole service running in Docker, using TestContainers, from driving adapter to driven adapters and back, against technologies in Docker.
        - Compliance checks for data contracts e.g., OpenAPI, JSON, and Avro, against company-wide rules e.g., paths are dash-separated.
        - Performance micro-benchmarks.
        - Mutation testing.
        - Security static code analysis, cyclomatic complexity, dependencies and Docker image vulnerability scanning, etc.
    - They work on the main branch directly, pushing a commit every time a new test passes, and after every small refactoring or tidying.
    - Every commit pushed to the upstream main branch is built, tested, and packaged. It's also either released directly, with automatic rollbacks based on error-rate monitoring, or deemed releasable manually at any moment.
    - There's only one environment: production. Test tenants and users are used to test things internally to the company, but in production.
    - New behavior is feature-flagged, so that it's only visible to internal tenants, until explicitly enabled for external tenants.
    - Ephemeral environments that are identical to production can be brought up on demand, in minutes. These are used to test large-scale changes that cannot be gradually rolled-out.
    - Smoke tests run continuously in production, on internal tenants and users, covering each of the company's business workflows. Alerts are triggered if they fail.

- Aspects:
    - This heavily limits what's possible, through types, tests, checks, many more smaller steps, working together, pre-defined component-level architecture, data contracts, CQRS, event-driven workflows.
    - This dramatically reduces the probability that something goes wrong, and the effort required to fix it when it happens. This increases super-linearly with the number of possibilities.
    - Shift left, the goal is to get quick feedback locally before pushing upstream. The tests and checks should run under three minutes. The careful modules and the smart build system hugely help.
    - Feedback happens early and often.
    - The tests and checks determine whether something is releasable. If something passes the tests and checks, and then breaks something, those tests and checks are evolved to prevent that in the future.
    - Every person works on the entire system, on rotation. Nobody works alone. There are always eight pairs of eyes on any character written. Problems are identified quicker. Quality is improved.
    - Knowledge spreads. If somebody is off, a team can function anyway.
    - Each team can work on anything needed. The company can flexibly schedule its work and concentrate its efforts.
    - A ton of waste is avoided: ceremonies, planning, fire-fighting, release management, branch management, merge conflicts, code reviews

[//]: # (TODO change the title;)