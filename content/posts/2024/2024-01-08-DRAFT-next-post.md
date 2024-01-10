---
title: "Interdependencies in your system of work"
categories: [ "system-thinking" ]
tags: [ "system-thinking", "Agile", "effectiveness", "software-development", "technical-processes" ]
date: 2024-01-10T05:00:00
draft: true
---

I hear of people saying their team tried Trunk-Based Development, and decided they didn't find it beneficial after a couple of months. I'm not going to war about the benefits of Trunk-Based Development today, even if I do love this practice.

Instead, I want to discuss the fact that this kind of statement is problematic. You see, Trunk-Based Development is a practice, and therefore it's part of a system of work. The performance of a system depends on how the parts interact, not on how the parts perform separately.

So you cannot look at Trunk-Based Development, a practice, and assess its performance in isolation from its containing system. It makes no sense whatsoever.

Also, experiencing something without a containing system is impossible. So when people say they tried Trunk-Based Development, they probably attempted to work directly on the main branch, and this was the only change in how they were working before.

What are the chances that "improving" a part of a system improves the performance of that system? Pretty much zero. Things actually almost always get worse.

When you introduce any practice, Trunk-Based Development is just an example, to the way you work, you're implicitly creating a new system of work. And that's what you experience in terms of performance. Not the merits of the practice itself, but the merits of your overall new work system.

It's as nonsensical as replacing the thrusters of an airplane with a helicopter's rotor, witnessing the crippled thing crash, and concluding that rotors are a bad idea. You might even be tempted to swap the rotor on the helicopter with some thrusters.

Once again, what are the chances that swapping a part of a system with a part of another system significantly improves the performance? Zero, and not just for aircraft.

## Comparing end-to-end alternative systems

The way people work to develop a software system is their system of work. This is a subsystem of the product development system, which in turn is a subsystem of the company, which is contained in the industry, and the economy, and so on ad infinitum. For the sake of this discussion, though, let's stop at the way people develop a software system.

The system of work is a sociotechnical system, involving people, teams, processes, practices, and the software system itself. All these aspects, like in any system, are interdependent: you cannot divide a system into independent subsystems.

So the practices, even when considered all together, don't have an independent effect on the system of work. You cannot take Test-Driven Development, Continuous Delivery, and Trunk-Based Development, and separate them from how the code is written, and from how the teams work.

People must experience end-to-end alternative systems of work to meaningfully evaluate the merits of different approaches. It's about comparing an airplane with a helicopter, not an airplane with the same airplane with its thrusters replaced by a rotor.

The effectiveness obviously depends on the context and the task at hand. You wouldn't use an airplane where helicopters excel, nor the other way around. There are some circumstances, though, in which either will do, and these tend to be leisure cruises with no stakes or associated risks. In software development it's the same: if what you're doing is trivial, or if you don't care about the outcomes, work in any way you want. No point in thinking about it, do whatever, and you'll get whatever.

If you happen to care, though, the difference in performance between two alternative systems can be tremendous. In particular, a system designed holistically and intentionally will usually dramatically outperform a system that's a patchwork of practises put together like if their effect added up linearly.

## Desired properties for our system of work

The first thing to do when attempting to design a system is to be explicit about its desired properties. After all, how can you design anything if you don't know what you want?

Since adopting specific practices is not a goal, what properties should our system of work have? If we're talking about developing software systems, I'd go with:

1. Effectiveness: doing the right thing, meeting the needs of the customers and of the company, delivering value earlier.
2. Safety: not breaking things for customers, not losing data, meeting security, privacy, compliance, and legal needs.
3. Sustainability: no heroics, no sprints, no borrowing from the future, and not ending up increasing the required costs or efforts over time.
4. Resilience: tolerating temporary absences, dealing with late changes in requirements, and working flexibly on anything needed.
5. Efficiency: minimizing no-value activities. An activity is deemed no-value if it doesn't directly add value for customers and users. Some useful activities, like discussing approaches, training employees, etc. are still no-value activities in this sense, because if you were able to provide the same value to your users without doing them, it'd be better.

If these are the desired properties we want in a system of work, we should compare alternative systems by assessing how well they do with regard to these properties.

I don't feel like criticizing various systems of work I don't believe in, at least not today. Instead, I'll outline how a system of work I like operates, and reason around the properties it yields. I'll leave it to you to assess the system of work your company employs.

## A particular system of work

Keep in mind that the various practices and processes are interdependent, so resist the temptation to decide whether you like this or that aspect, and form a holistic judgment at the end instead.

Also, a system of work is always the child of a belief system. So if any point evokes a strong negative reaction, stop for a minute and try to understand which of your fundamental believes is in conflict with that aspect. You don't need to agree, but understanding why you strongly disagree will benefit you.

The proposed system would work according to the following principles:

1. A cross-functional leaderless [team (not merely a group of coworkers)](https://sollecitom.github.io/software-product-development-blog/posts/2023/2023-12-31-so-you-think-you-work-in-a-team/) of five product developers, working as equals, without seniority roles or separate responsibilities. This includes a mix of:
    - Skills at web, infrastructure, back-end, and mobile.
    - Settlers, explorers, and town planners.
    - People with creativity, with a bias for action, and with long-term thinking.
    - Starters and finishers.
    - Skills at scripting, prototyping, and testing.
    - A mix of backgrounds and experiences, the more, the merrier.
2. The team members work in an ensemble e.g., with [Mob Programming](https://www.agilealliance.org/resources/experience-reports/mob-programming-agile2014/). This means they work synchronously together on the same task, rather than splitting the job and working in isolation.
3. The team members are either all office-based, sitting closely with each other, or all fully-remote, working on a team video call most of the day.
4. The distributed system employs an [Event-Driven Architecture](https://en.wikipedia.org/wiki/Event-driven_architecture). [Service choreography](https://camunda.com/blog/2023/02/orchestration-vs-choreography/), [CQRS](https://cqrs.files.wordpress.com/2010/11/cqrs_documents.pdf), and [Event Sourcing](https://www.eventstore.com/event-sourcing). Services are unaware of each other, share no dependencies, and only communicate using [Domain Event](https://medium.com/@chaojie.xiao/domain-driven-design-practice-domain-events-15b38f3c58fc)s with a company-wide schema registry.
5. The services are grouped using [Bounded Context](https://martinfowler.com/bliki/BoundedContext.html)s, and following how the business works. [Context Mapping](https://www.infoq.com/articles/ddd-contextmapping/) is used to visualize how the various contexts interact. ([Domain-Driven Design](https://learn.microsoft.com/en-us/archive/msdn-magazine/2009/february/best-practice-an-introduction-to-domain-driven-design)).
6. Each software service is structured according to [Hexagonal Architecture](https://www.arhohuttunen.com/hexagonal-architecture/). Driving and driven adapters, application, domain.
7. The team favors those programming languages with a sophisticated type system. Examples might be TypeScript for frontend applications, Kotlin/Scala for backend, Golang with [Pulumi](https://www.pulumi.com/b/) for infrastructure.
8. [Aggregate Roots](https://martinfowler.com/bliki/DDD_Aggregate.html), [Entities, and Value Objects](https://blog.jannikwempe.com/domain-driven-design-entities-value-objects) form a rich and type-safe domain model for each [Bounded Context](https://martinfowler.com/bliki/BoundedContext.html), [reflecting the language used by the business](https://martinfowler.com/bliki/UbiquitousLanguage.html). ([Domain-Driven Design](https://learn.microsoft.com/en-us/archive/msdn-magazine/2009/february/best-practice-an-introduction-to-domain-driven-design)).
9. Shared libraries provide implemented patters, utilities, and a few thin [Shared Kernel](https://deviq.com/domain-driven-design/shared-kernel)s.
10. There's a company-wide registry for Pulsar/Kafka topics and contracts e.g., [OpenAPI](https://www.openapis.org/), [Avro](https://avro.apache.org/), and [JSON Schema](https://json-schema.org/).
11. There's [Collective Code Ownership](https://en.wikipedia.org/wiki/Extreme_programming_practices#:~:text=Collective%20code%20ownership%20): no team or person owns any area of the codebase or any part of the product.
12. The team pulls initiatives from a company-wide queue, working on one thing at a time, end-to-end, till completion. The team is in continuous collaboration with stakeholders and external experts. Initiatives are carved to take between 1 week and 6 weeks each.
13. Initiatives are minimally specified, as a summary that captures the problem or opportunity. All conversations with stakeholders and experts happen synchronously (either face-to-face or on video call). All discussions include all the relevant people, and happen at the latest responsible moment, right at the beginning of the work.
14. The team remains responsible for most decisions. Experts provide advice on demand, stakeholders clarify the problem or opportunity space, but the team is in charge of the solution space, and of the implementation.
15. The team uses [Story Mapping](https://www.jpattonassociates.com/wp-content/uploads/2015/03/story_mapping.pdf) to design and document the solution, and [Event Storming](https://en.wikipedia.org/wiki/Event_storming) to design the implementation.
16. The code is written using [Outside-In Test-Driven Development](https://www.codecademy.com/article/tdd-outside-in), with clear contracts and example tests at module boundary's level.
17. Each invocation (commands and queries) is processed along with a bundle of information about the invocation itself. The [Invocation Context](https://sollecitom.github.io/software-product-development-blog/posts/2023/2023-12-10-start-with-a-skeleton-not-to-die-a-zombie/#:~:text=Correlation-,Invocation%20context,-Every%20invocation%20should) contains the user ID, the tenant ID, the ID of the token, etc. This information is logged, and it's part of each published [Domain Event](https://medium.com/@chaojie.xiao/domain-driven-design-practice-domain-events-15b38f3c58fc). It's also used to [implement](https://sollecitom.github.io/software-product-development-blog/posts/2023/2023-12-10-start-with-a-skeleton-not-to-die-a-zombie/#:~:text=message%20correlation%20information.-,Idempotency,-The%20invocation%20context) [idempotency](https://betterprogramming.pub/architecting-distributed-systems-the-importance-of-idempotence-138722a6b88e) for all operations.
18. The services use a build system capable of only rebuilding and retesting the modules that actually changed, using a deterministic non-cryptographic hash algorithm to determine whether a module has changed. An example for the [JVM](https://en.wikipedia.org/wiki/Java_virtual_machine) is how [Gradle](https://gradle.org/) uses the [Build Cache](https://www.baeldung.com/gradle-build-cache) to achieve this.
19. The code is made of well-defined modules with clear boundaries, responsibilities, and contracts. These can include [Gradle modules](https://docs.gradle.org/current/userguide/multi_project_builds.html), [React components](https://legacy.reactjs.org/docs/components-and-props.html), shared libraries, (micro)services, etc. Limiting how these modules interact and establishing rigorous contracts, with tests checking them, is also essential, because it allows knowing when to stop testing things because of a change. An [Event-Driven Architecture](https://en.wikipedia.org/wiki/Event-driven_architecture) with data contracts using [Avro](https://avro.apache.org/) really helps achieve this.
20. The build performs an array of tests and checks, including:
    - Application tests: they test the application layer against the stubbed driven adapters. These cover the application logic.
    - Integration tests: driving adapters against a stubbed application, checking their inbound contract e.g., OpenApi or Avro. Driven adapters against their target technology running in Docker through TestContainers.
    - In-process service tests: the whole service going from driving adapter to driven adapters and back, against the downstream technologies running in Docker through TestContainers.
    - Container-based service tests: the service itself running in Docker, using TestContainers, from driving adapter to driven adapters and back, against the downstream technologies in Docker, also through TestContainers.
    - Property-based tests: where inputs are randomized, and outputs are checked against properties in relation to inputs e.g., the inverse of a matrix multiplied by the original matrix should produce the identity matrix.
    - UI-driven tests: these tests check the correct rendering of UIs by exercising the UI against an in-memory implementation of the SDK that abstracts all communications between frontend and backend.
    - Compliance checks for data contracts e.g., OpenAPI, JSON, and Avro, against company-wide rules e.g., paths are dash-separated, no typos, no top-level array fields, etc.
    - Performance micro-benchmarks. These tests prevent regressions in performance-sensitive parts of a service, without taking a big amount of time to run.
    - Mutation tests. These tests inject mutations in the codebase before running the other tests, and count how many mutants go through the tests without failures. This is a way of assessing the effectiveness of your tests.
    - Static code analysis, with regard to security, cyclomatic complexity, code smells, and inefficiencies.
    - Dependency scanning to check dependencies and Docker images for security vulnerabilities.
21. Performing all the tests and checks that are part of every build takes less than 3 minutes overall. This is only possible with great attention to modularity, a smart build system, and tests that can confirm whether some changed module still honors its contracts.
22. The team works directly on the main branch, with [Trunk-Based Development](https://medium.com/@mattia.battiston/why-i-love-trunk-based-development-641fcf0b94a0), pushing a commit every time a new test passes, and after every small refactoring or tidying. This typically happens at least once every 10 minutes, for each team.
23. [Continuous Delivery](https://continuousdelivery.com/) is in place: every commit pushed upstream to the main branch is built, tested, and packaged, and each packaged new version of the code is either released directly, with automatic rollbacks based on error-rate monitoring, or deemed releasable at any moment, without any further checks needed.
24. Only one permanent environment exists: production. There are internal tenants and users to test things before rolling them out to customers, but this [testing happens in production](https://copyconstruct.medium.com/testing-in-production-the-safe-way-18ca102d0ef1).
25. New behavior is guarded by [Feature Flags](https://martinfowler.com/articles/feature-toggles.html), so that it's only visible to internal test tenants, until explicitly enabled for external tenants. This allows releasing features in a coordinated way with marketing and sales.
26. [Ephemeral environments](https://ephemeralenvironments.io/) that are identical to production can be brought up on demand, in minutes. These are used to test large-scale changes that cannot be gradually rolled-out.
27. [Smoke tests run continuously in production](https://newrelic.com/blog/how-to-relic/smoke-testing-with-synthetic-monitors), on internal test tenants and users, simulating the company's business workflows end-to-end. Alerts are triggered if these tests fail.
28. [Chaos engineering](https://www.lambdatest.com/learning-hub/chaos-testing) simulates the random loss of arbitrary infrastructure areas, in production.
29. An external monitor is used to check whether the APIs and web applications of the company are reachable from outside the company's infrastructure, and for [DNS monitoring](https://www.pagerduty.com/resources/learn/dns-monitoring/). Alerts are triggered if these checks fail.

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
10. The codebase is always working, at each commit, both locally and remotely. A team can pivot at any point without effort. Late changes in requirements are accommodated immediately with minimum disruption.
11. A ton of non-value activities are avoided: ceremonies, planning, fire-fighting, splitting work across teams or people, release management, branch management, merge conflicts, code reviews, manual regression testing, manual deployments, security reviews, etc.

## Final words

If you only take one thing from this post, let it be this: you cannot evaluate a practice in isolation. You should always evaluate alternative end-to-end systems of work, because the effectiveness depends on how the various parts work together.

So next time you encounter a practice you're curious about, don't try to introduce it in your existing way of working. Instead, try to understand what it enables, and to think at how you could build a different way of working, given this new possibility.