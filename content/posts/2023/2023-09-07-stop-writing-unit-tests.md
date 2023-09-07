---
title: "For crying in the beer, stop writing unit tests!"
categories: [ "technical" ]
tags: [ "testing", "software", "test-strategy", "unit-tests", "contract-tests" ]
date: 2023-09-07T11:30:00
draft: false
---

Stop writing unit tests! It's wrong on many levels, so don't do it. Actually remove the ones you have.

I'm a huge fan of automated tests, and I use Test-Driven Development a lot, so no, I'm not advocating against testing in general. And don't think the solution is to write a lot of end-to-end tests either, as that's even worse.

So what's wrong with unit tests? And what should we do instead? Let's have a look...

## How most developers approach testing

Assuming they write tests at all, people tend to write unit, integration, and end-to-end tests.

Leaving aside the names for a second, as there's no consensus on these, the idea is that there are units, like lego blocks, and these units interact to deliver functionality as part of a service. Services, in turn, interact as part of a system.

With this in mind, the usual test strategy involves the following test types.

### Unit tests

Unit tests focus on your units. In particular, a unit test covers a unit in isolation from other units. What's a unit? Well, a unit is a function or type e.g. a class.

You construct the unit, isolate your test by replacing its dependencies with mocks or stubs you can control, then excite the unit, and check the outputs and the internal state.

Examples:

- You have a car with 4 wheels, you remove 1 wheel, and you check that the car now has 3 wheels.
- You create a car of a make and colour, and you check that its colour and make match the ones you passed as inputs.
- You have a 1m-high table, and you check its height property is equal to 1m.

I can see some of you screaming, but this is a popular approach. I'm aware that this is not what Kent Beck meant, more on this towards the end of the post.

### Integration tests

Integration tests, as the name suggests, focus on testing the integration logic. So what are we integrating and testing? Well, we're integrating various units together, and we're also integrating with databases, etc.

Now that we have tested the lego blocks, we cover their integration with other blocks or downstream dependencies.

How does this work? You spin up your service, create some preconditions inside your downstream dependencies e.g. databases or queues, you excite your service using its API e.g. through an HTTP client, and check the outputs and the internal state in the DB or queue after the changes. If something is misconfigured at service level, integration tests have good chances of catching it.

These tests catch more issues than unit tests, but are slower. Also, expectations are harder to set up at database or queue level, so many conditions are harder to simulate at this level (e.g. delays, dependencies not being available or misbehaving). So we don't just rely on these, but also on unit tests.

### End-to-end tests

End-to-end tests cover the interaction between different services and systems. They go from one end to the opposite end, are driven by the input closest to the user e.g. a UI or a top-level API, and they drive all sorts of upstream and downstream systems, including load balancers, databases, Cloud providers, and even SaaS vendors.

These are slow, cumbersome, often unstable, poorly isolated, and require a full environment to run, but hopefully we don't need as many, once we have unit and integration tests in place.

## Doesn't this work?

So what's the problem with this approach? It sounds sensible after all. In order to understand the problem, we need to think about what great looks like.

### What great looks like

A great automated test suite is surprisingly intuitive: it provides you with quick and accurate confidence that your changes are good to go.

The feedback must be quick. Speed really matters here. Delay the feedback, and you get all sorts of problems, including people switching to other tasks while waiting, increasing work in progress, rework, etc.

The feedback must also be accurate. This means you should be able to pinpoint the problem whenever there are test failures.

What does confidence mean here though? Everybody immediately recognises that confidence means that when things are wrong, your tests should indeed tell you that things are wrong. So false positives are bad.

Is this enough though? Well, no, it isn't. You also need confidence that when things are working, your test suite should tell you that things are okay. False negatives are a real bummer as well.

### The problem

There are so many problems with the unit, integration, and end-to-end test strategy, and they all fundamentally stem from a misconception of how systems work.

Like Ackoff used to say, "A system is never the sum of its parts; it’s the product of their interaction" and "The performance of a system doesn't depend on how the parts perform taken separately, it depends on how they perform together – how they interact, not on how they act, taken separately".

The thinking behind this popular test strategy is that your software system is the sum of its parts, or units. So if the units are working correctly, then the system is also going to work well.

I can hear you thinking "uh, not so, because we have integration and end-to-end tests, so we care about the interactions as well". True, but there's nuance to this.

By thinking of a system as the sum of its parts, we can't let go of the need for tests that focus on the parts in isolation: our unit tests. After all, if a part is not working well, how could its containing system ever work well, right? And what's the issue with unit tests anyway?

When unit tests are defined as above, focusing on classes or functions in isolation, they cannot test behaviour, because behaviour is a property of a system, never of its parts. A class doesn't do anything in isolation; behaviour comes from the interactions.

So if they cannot test behaviour, what do unit tests test? Structure. Let's revisit the examples above:

- You have a car with 4 wheels, you remove 1 wheel, and you check the car now has 3 wheels.
- You create a car of a make and colour, and you check that its colour and make match the ones you passed as inputs.
- You have a 1m-high table, and you check its height property is 1m.

None of these tests is about behaviour. They test structure, e.g. state or properties. That there's a table, and that its height is 1m. That a car has 4 wheels.

The problem here is that you care about the correct behaviour of your system, not about its structure.

You might counter with the argument that, at worst, unit tests are not that useful, but I believe they're actually destructive. Something to avoid at all costs.

How can I sustain this? Well, the problem with unit tests is that, by focusing on structure rather than on behaviour, they intrinsically cause your test suite to yield false negatives. So your system works, but your tests fail or don't even compile.

What's the purpose of a table in your kitchen? For you to eat? With how many people? At what time? While watching TV? Can you meet these behavioural needs in a way that employs a different table or table position, or that doesn't require a table at all? Well, if you can, your unit tests will fail. If the height of the table is different, your tests will fail. And if you remove the concept of a table altogether, your tests won't even compile.

So if you change the structure of your code, and you're forced to change your tests, are those tests giving you any confidence at all? How do you know things are still working fine, if you had to change the tests?

Ultimately, unit tests are bad because they prevent you from getting quick and accurate confidence that your changes are good to go, and they increase the amount of work you need to change things.

You might counter with "that's kid of okay, no? You structure your service well, and then add coverage to prevent regressions". This is the same as nailing your kitchen table to your kitchen floor, so it stays perfectly still and aligned. But worse, because software is *ALL* about changing things. It's never a linear activity, where you build, A, then B, then C, and so on. It's about iterating over and over on the same system, continuously evolving it to react to changing needs.

### A perverse alternative

Quite a few people and companies have come to realise that unit tests, as described above, are a liability, but the alternative they choose is equally destructive.

They mostly write end-to-end tests, and end up with crazy long test suite runs. Given that end-to-end tests require an environment with the whole system in it, this is typically a shared environment, and things can easily fail because of random IO conditions, or because changes are made to the systems while the tests are still running e.g. when another team deploys a new version of a service.

This solution doesn't yield false positives, but still has false negatives due to its instability, while destroying both the speed and the accuracy of the feedback. If anything, it's worse than the approach that adopts unit tests.

## What to do instead

So approaches that use unit tests or that mostly focus on end-to-end tests are both bad. What are we left with? What can we do instead?

The problems I described derive from a misinterpretation of the concept of unit tests. Yes, they focus on units in isolation, but a "unit" originally meant a unit of behaviour.

So your unit is not a class or function, but a self-contained module capable of providing value on its own. Not a part of a system, but a sub-system. And these units don't add up linearly, but compose together to form systems of increasingly higher order. Units containing other units, if you will.

What does this mean? It means that an effective test strategy still employs unit, integration, and end-to-end tests, but their responsibilities are separate, and their meaning is different.

### End-to-end tests

End-to-end tests are a type of unit tests, where the unit is your whole system.

You want to distinguish between tests that tell you whether your system is currently working, and tests that tell you whether your system works.

1. Your system might work, in the sense that it's implemented correctly and handles outages or adverse conditions well.
2. But it might not currently work, in the sense that a necessary downstream or upstream external system might not be currently working. Or maybe it doesn't have any running instance.

It's important that your tests distinguish between these 2, because what you do when your tests fail is different in each case.

1. If your system doesn't work correctly, you should change it until it does. This means your pipeline should stop, and you should fix things before releasing the change.
2. If your system is currently not working, you should look into it operationally, as you might want to get in touch with the companies or teams responsible for your external dependencies. In any case, your build pipelines should not stop, as there's nothing your system is doing wrong.

It's useful to adopt different names, and I propose we use "smoke tests" for tests that tell you whether your system is currently working, and "system tests" for tests that tell you whether your system works.

#### Smoke tests

You don't typically need many of these, because their function is not to provide confidence that your system works. If any of your upstream or downstream systems isn't currently working, you tend to notice.

They should be deep, to cover your business workflows. An example might involve a new user singing up, then signing in, accessing the value you provide, then logging out, then quitting your product. Another one might excite the whole account recovery workflow. And so on.

You don't even need accuracy here. If anything fails, you can smell smoke, hence the term, and given that your build passed all tests, it's typically a misbehaving upstream or downstream system. You go and investigate. Occasionally you might find that it's not due to an external system, and your tests were not covering something important, so you go and evolve those tests.

Smoke tests are not run as part of your build or even release pipelines, but they run periodically in your production environment. So while you typically don't need many, there's no harm in having more than just a few, as these don't slow down your feedback when you build.

#### System tests

System tests are end-to-end, similarly to smoke tests, but the similarities end here. These tests tell you whether your system works, so you remove all factors you cannot control, including all upstream or downstream systems that are outside your company.

These are run as part of your build pipeline, in an environment with multiple services in it, and they're slow and cumbersome.

As such, there should be as few of these as possible. The ideal number here is zero. Yeah, you heard that right. If your release pipeline includes error-rate monitoring and canary rollouts with automatic rollbacks, any misconfiguration across services will be caught at that time anyway. But you could still have some, just never rely on these to provide confidence. Use them as an expensive and inconvenient safety net, and get rid of it as soon as you're confident with your test suite.

### Integration tests

Integration tests are also a type of unit tests, where the unit is a service, as opposed to your whole system made of multiple services.

If you organize your service to adopt a Hexagonal Architecture - and you should - you can think about your service as some glue, plus a collection of subsystems:

1. Driving adapters, which drive your service e.g. HTTP endpoints or Kafka consumers.
2. Your application, the facade the driving adapters interact with.
3. Driven adapters, which your application drives e.g. databases, queues, and external APIs.

With this in mind, integration tests can be split into "adapter tests" and "service tests".

#### Adapter tests

A port is an external system that either calls your application or is called by it. A driving port or a driven port. An HTTP API or a SQL database.

Your service has an adapter for each of these ports, like an HTTP endpoint, or the JDBC or JPA implementation of a repository.

Adapter tests check that your adapter can adapt your application with their target port. They do not check the correctness of your application.

##### For driving adapters

Imagine your application was exposed through an HTTP API, then the set of your HTTP endpoints is your driving adapter for your HTTP API port, or your driving HTTP adapter.

The way you test it is by mocking or stubbing your application to behave in a fixed way, by producing a query or command using a real HTTP client and request, and by then checking that both the request and the response comply with your stated HTTP API e.g. your OpenAPI specification, and that the return data matches what you expected, given the behaviour you fixed in the application and the command or query.

An example might include:

1. You want to test your handling of commands to register new users, when a user hasn't already registered with that email address.
2. You instruct your application layer to return a result stating that the user registration command was accepted successfully (as opposed to another result indicating it was rejected because an already registered user existed).
3. You then create an HTTP request you can fire with your chosen HTTP client.
4. You check that your request complies with your OpenAPI specification. Paths, headers, request body schema, etc.
5. You start your endpoint, injecting your stubbed application in it, and get the port it's running on.
6. You send the HTTP request to your endpoint, using the HTTP client pointing at the port the endpoint is running on.
7. You receive an HTTP response, and check it complies with your OpenAPI specification as a response for the given request. Paths, headers, status code, response body schema, etc.
8. You check that the data in the response matches in content what you expect, based on the use case e.g. that it indicates that things were accepted just fine. This involves the expected status code e.g. 202, and might also involve the headers and response body.

These tests still run locally and are quite fast (~1 second), and you typically have 1 suite per adapter, requiring to start each driving adapter e.g. the HTTP server only once.

##### For driven adapters

Imagine your application wrote to a SQL database or appended an event to an event bus. The database or event bus is your port, and your driven adapter is the logic that transforms a call in the domain language your application speaks into a call to this external service.

The way you test it is by creating preconditions in your downstream system, by driving an invocation using your domain-level facade e.g. a repository interface, and by then checking the result returned by your domain-level facade and then internal state of your downstream dependency.

An example might include:

1. You want to test recording a newly registered user, either by inserting it in a Postgres database, or by appending an event to Kafka.
2. You start Postgres or Kafka in Docker using `TestContainers`, and use a raw JDBC client or Kafka producer to create preconditions in the form of preexisting data.
3. You create an instance of your `PostgresUserRepository` or `KafkaUserEventPublisher`, pointing at your running Postgres or Kafka container.
4. You use your `UserRepository` domain-level interface to record the fact that a user was registered.
5. You check that the value returned by the domain-level interface matches your expectations, given the preconditions.
6. You use your raw JDBC client or Kafka client to check the state of your Postgres or Kafka container after the invocation e.g. that the data is there, or that you can receive the event on the right topic.

These tests still run locally and are reasonably fast (~1-5 seconds), and you typically have 1 suite per adapter, requiring you to start each driven adapter e.g. Postgres or Kafka in Docker only once.

#### Service tests

Service tests test your service as a whole, mostly covering the glue code and your service-level configuration.

Typically, a service test:

1. Starts the driven ports e.g. your Postgres database or your Kafka cluster in Docker, using `TestContainers`.
2. Creates some preexisting data inside these ports using raw clients.
3. Starts the whole service, like it would be started externally, by passing args and environment variables to the main class or function.
4. Uses a raw client to drive the service e.g. an HTTP client.
5. Checks that the response has the right status and data.

These tests still run locally and are reasonably fast (~1-5 seconds), and you typically have 1 suite for a whole service. These don't duplicate the scenarios tested elsewhere, because their job is not to catch poorly implemented domain or integration logic, but to catch problems with the glue code or the configuration. This means there's usually 1-2 cases here, the main happy path and handling unavailable dependencies at service start time.

##### In-process and in-Docker

Ideally you want to run the service tests both in-process and in-Docker.

- The in-process tests start the service within the same process the test runs in e.g. by calling your main function if you use Kotlin or Java.
- The in-Docker tests start the service within a Docker container, as a separate process. This requires building the Docker image as part of your local build, and then using `TestContainers` to start the current version of your service within a Docker container.

Ideally you should use the same test specification for both, and the only difference should be how you start the service.

Also testing in-Docker allows you to catch problems related to how you build, configure, and run your Docker container. This is important, because services tend to run packaged these days, so you better catch packaging issues early.

### Unit tests

Unit tests focus on testing your application and domain logic. Instead of focusing on whether a given type works, a unit test covers a unit of behaviour, i.e. a subsystem or module within your application or domain layers.

This requires structuring your application into modules that are self-contained, each with their own contract. You should treat these modules like libraries.

Each module get its own tests, checking that the module behaves correctly against its contract. What contract am I talking about? Here there's no OpenAPI or Avro after all? I'm talking about its public API.

A module will have a contract or API, which is the set of all its publicly visible types and functions.

#### Contract tests

Contract tests are a type of tests that test a module against its contract, or public API. These are basically runnable specifications, documentation, and examples of how the module delivers its value through the interaction of its types and functions.

Every workflow or condition is represented in these tests, but only publicly visible types and functions can appear here.

These tests run locally, in-memory, and have no IO interactions, meaning they're really fast and reliable.

When you build a library, these example tests are also hugely useful for the users of your library.

#### Type-specific tests

Every publicly visible type might also get its type-specific test, to check that type behaves correctly. This is not as important in a service as it is in a library.

In a library, each publicly visible type gets its own test, because you don't know how what the users of the library will do. In a service, contract tests are typically enough, because if a type has an issue but the contract tests pass, it means that the issue is not impacting your expected behaviour.

## Final words

That's it, a long explanation of my go-to test strategy, and of why I believe it's a good idea compared to some popular approaches. I apologise to Kent Beck for using the word "unit tests" with a negative connotation, but sadly these days they tend to mean something far from their original meaning.

I leave you with some further advice you might find useful when structuring your test strategy:

1. Don't aim for coverage, but at getting quick and accurate confidence that your changes are good to go.
2. Ensure you can run most of your tests locally.
3. Ensure your tests can survive structural changes without false negatives or broken compilation.
4. Ensure each test type is specific, removing the need to cover possibilities in a cumbersome and slow way, when they could have been covered in a faster and more convenient way instead.
5. Write your tests first, and your application and integration logic second, in small steps, using Test-Driven Development.
6. Organize and package your services and systems for ease of testing things without resorting to end-to-end system tests. It will pay off big time.