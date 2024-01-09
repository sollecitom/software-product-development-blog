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

## What's a system of work?

The way people work to develop a software system is their system of work. This is just a subsystem of the product development system, which in turn is a subsystem of the company, which is contained in the industry, and the economy, and so on ad infinitum. For the sake of this discussion, though, let's stop at the way people develop a software system.

The system of work is a sociotechnical system, involving people, teams, processes, practices, and the software system itself. All these aspects, like in any system, are interdependent, and you cannot divide the system into independent subsystems.

So the practices, even when consider all together, don't have an independent effect on the system of work. You cannot separate Test-Driven Development, Continuous Delivery, and Trunk-Based Development from how the code is written, and from how the teams work.

## Assessing end-to-end alternative systems

To meaningfully evaluating the merits of different approaches, people must experience end-to-end alternative systems of work.

It's the small airplane or the helicopter, not the small airplane or the small airplane with its thrusters replaced by a rotor.

This obviously depends on the context and the task at hand. You wouldn't use a small airplane where helicopters excel, nor the other way around. There are some circumstances in which either will do, and these tend to be leisure cruises with no stakes or associated risks.

In software development it's the same: if what you're doing is trivial, and if you don't care about the outcomes much, work in any way you want. No point in thinking deep about it, do whatever, and you'll get whatever.

If you happen to care, though, the difference in performance between two alternative systems can be significant. In particular, a holistically and intentionally designed system will usually run circles around a system that's a patchwork of practises put together like if their effect added up.

## Desired properties for our system of work

The first thing to do when attempting to design a system is to be intentional with its desired properties. After all, how can you design anything if you don't know what you want?

Since adopting specific practices is not a goal, what should the desired properties of our system of work be? If we're talking about developing software systems, I'd go with:

1. Effectiveness: doing the right thing, meeting the needs of the customers and of the company, delivering value earlier.
2. Safety: not breaking things in production, paying attention to security, compliance, and legal aspects.
3. Sustainability: no heroics, no sprints, no borrowing from the future, and not ending up increasing the required costs or efforts over time.
4. Resilience: coping with temporary absences, adjusting to late changes in requirements, and working flexibly on anything needed.
5. Efficiency: avoiding non-value activities.

If these are the desired properties we want in a system of work, we could evaluate alternative systems by assessing how well they manifest these properties.

I don't feel like criticizing the systems of work I don't believe in, at least not today. Instead, I'll outline how the system of work I do believe in operates, and reason around the properties it yields. I'll leave it to you to assess the system of work your company adopts.

## A possible system of work

Next, I'm going to describe a possible system of work. Keep in mind that the various practices and processes are interdependent, so resist the temptation to decide whether you like this or that aspect, and a holistic judgment at the end instead.

Also, a system of work is always the child of a belief system. So if any part evokes a strong negative reaction, stop for a minute and try to understand which of your fundamental believes is in conflict with the practice.

The proposed system would work according to the following principles:

1. A cross-functional leaderless team of five product developers. This includes a mix of:
    - Skills at web, infrastructure, back-end, and mobile.
    - Settlers, explorers, and town planners.
    - People with creativity, with a bias for action, and with long-term thinking.
    - Starters and finishers.
    - Skills at scripting, prototyping, and testing.
2. The team members work in an ensemble, like in mob programming. This means they synchronously work together on the same task, rather than splitting the job and working in isolation.
3. The distributed system adheres to an event-driven architecture. Service choreography, CQRS, event-sourcing, permanently stored events that can be replayed. Services are unaware of each other, and only communicate using domain events with a company-wide schema registry.
4. The services are grouped using Bounded Context (Domain-Driven Design) and following how the business works. Context Maps (Domain-Driven Design) are used to visualize how the various contexts interact.
5. Each software service uses hexagonal architecture. Driving and driven adapters, application, domain.
6. The team favors those programming languages with a sophisticated type system.
7. Aggregate Roots, Entities, and Value Objects forming a rich and type-safe domain model for each Bounded Context, following the language used by the business (Domain-Driven Design).
8. Shared libraries provide implemented patters, utilities, and a thin Shared Domain.
9. There's a company-wide registry for Pulsar/Kafka topics and contracts e.g., OpenAPI, Avro, and JSON.
10. No team owns any area of the codebase or any part of the product.
11. The team pulls initiatives from a company-wide queue, working on one thing at a time end-to-end, till completion, in continuous collaboration with stakeholders and external experts. Initiatives are carved to take between 1 week and 6 weeks each.
12. The team remains responsible for most decisions. Experts provide advice on demand, and stakeholders clarify the problem or opportunity space, but the team is in charge of the solution space, and of the implementation.
13. Code is written using outside-in Test-Driven Development, with clear contracts and example tests at module boundary's level.
14. Each invocation (commands and queries) is processed along with a bundle of information about the invocation itself. The user ID, the tenant ID, the ID of the token, etc. This information is logged, and it's part of each published domain event. It's also used to implement idempotency for all operations.
15. The services use a build system capable of only rebuilding and retesting the modules that actually changed, using a deterministic non-cryptographic hash algorithm to determine whether a module has changed.
16. The build includes an array of tests and checks that can all run locally in under 3m (courtesy of the smart build system and the in-process tests):
    - Application tests: they test the application layer against the stubbed driven adapters. These cover the application logic.
    - Integration tests: driving adapters against a stubbed application, checking their inbound contract e.g., OpenApi or Avro. Driven adapters against their target technology running in Docker through TestContainers.
    - In-process service tests: the whole service going from driving adapter to driven adapters and back, against the downstream technologies running in Docker through TestContainers.
    - Container-based service tests: the service itself running in Docker, using TestContainers, from driving adapter to driven adapters and back, against the downstream technologies in Docker, also through TestContainers.
    - Compliance checks for data contracts e.g., OpenAPI, JSON, and Avro, against company-wide rules e.g., paths are dash-separated, no typos, no top-level array fields, etc.
    - Performance micro-benchmarks. These tests prevent regressions in performance-sensitive parts of a service, without taking a big amount of time to run.
    - Mutation tests. These tests inject mutations in the codebase before running the other tests, and count how many mutants go through the tests without failures. This is a way of assessing the effectiveness of your tests.
    - Static code analysis, with regard to security, cyclomatic complexity, code smells, and inefficiencies.
    - Dependency scanning to check dependencies and Docker images for security vulnerabilities.
17. The team works directly on the main branch, pushing a commit every time a new test passes, and after every small refactoring or tidying. This typically happens maximum every 10 minutes.
18. Every commit pushed upstream to the main branch is built, tested, and packaged.
19. Each packaged new version of the code is either released directly, with automatic rollbacks based on error-rate monitoring, or deemed releasable at any moment, without any further checks needed.
20. Only one permanent environment exists: production. There are internal tenants and users to test things before rolling them out to customers, but this testing happens in production.
21. New behavior is feature-flagged, so that it's only visible to internal tenants, until explicitly enabled for external tenants. This allows releasing features in a coordinated way with marketing and sales.
22. Ephemeral environments that are identical to production can be brought up on demand, in minutes. These are used to test large-scale changes that cannot be gradually rolled-out.
23. Smoke tests run continuously in production, on internal tenants and users, simulating end-to-end the company's business workflows. Alerts are triggered if they fail.
24. An external ping is used to check whether the APIs of the company are reachable from outside the company's infrastructure. Alerts are triggered if this fails.

In terms of the properties this system of work yields, we have:

1. Feedback happens early and often. From continuously working with stakeholders and experts, from running tests and checks locally, and from releasing tens of times a day. This delivers value earlier and prevents large amounts of rework from misunderstood requirements.
2. Nobody works alone. Eight pairs of eyes review each character typed. This raises quality, prevents mistakes, and avoids rework a delayed inspection would introduce. Problems are identified earlier, when fixing them is much cheaper.
3. Types, tests, checks, ways of working, data contracts, CQRS, event-driven workflows, and a pre-defined component-level architecture heavily limit what's possible. Fewer possibilities mean fewer things to keep in mind, which means fewer mistakes.
4. Releases are very safe, because the team takes many more much smaller steps. The effort required to fix the occasional issue is low.
5. Everybody works on the entire system. There are no silos, permissions asked, or dependencies among teams. The work stays interesting. The teams have end-to-end ownership of an initiative, working directly with stakeholders, customers, and experts.
6. The amount of work-in-progress is under control. Teams don't work on more than they can chew. Nobody burns out. Things are finished before other things are started.
7. Code quality is very high, and the architecture is modular and extensible. The cost of modifying the software system doesn't continuously increase over time.
8. Knowledge spreads within a team (because of ensemble programming), and across teams (because there are no areas of the codebase owned by any team).
9. Each team can work on anything the company needs. Initiatives can be flexibly scheduled regardless of their domain area.
10. A ton of non-value activities are avoided: ceremonies, planning, fire-fighting, splitting work across teams or people, release management, branch management, merge conflicts, code reviews, manual regression testing, manual deployments, security reviews, etc.

## Final words

If you only take one thing from this post let it be this: you cannot evaluate a practice in isolation. You should always evaluate alternative end-to-end systems of work, because the effectiveness depends on how the various parts work together.

So next time you encounter a practice you're curious about, don't try to introduce it in your existing way of working. Instead, try to understand what it enables, and to think at how you could build a different way of working, given this new possibility.