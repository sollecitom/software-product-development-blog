---
title: "It's time to put REST to rest"
categories: [ "technical" ]
tags: [ "http", "rest" ]
date: 2023-09-22T07:00:00
draft: false
---

REST is still going strong these days, with many companies structuring their HTTP API based on its principles. And yet, I think that REST is a fundamental mistake, that it caused a lot of damage and pain, and that people should just stop creating RESTful HTTP APIs.

A bold statement, isn't it? Let's dig a little bit deeper to understand the problem, and an alternative.

# What is REST: a recap

I won't explain REST in details, but a brief and incomplete summary is that, in a RESTful HTTP API:

1. Users manipulate resources.
2. Resources have a representation in various data formats e.g. JSON, but even XML or others.
3. A resource is associated to a specific request path.
4. Resources can be nested to model relationships.
5. Some HTTP methods assume a specific meaning, representing particular actions a user can do on a resource:
    - ``GET`` retrieves a resource e.g. ``GET /schools/{school-ID}/students/{student-ID}`` would retrieve a student with given ID of the school with given ID. The response body might look like ``{ "id": "123", "firstname": "Bruce", "lastname": "Wayne"}``
    - ``POST`` creates a new resource e.g. ``POST /schools/{school-ID}/students { "firstname": "Peter", "lastname": "Parker" }``
    - ``DELETE`` removes a resource e.g. ``DELETE /schools/{school-ID}/students/123``
    - ``PUT`` replaces a resource in its entirety e.g. ``PUT /schools/{school-ID}/students/234 { "firstname": "Clark", "lastname": "Kent" }``
    - ``PATCH`` replaces a field in a resource with a new value ``PATCH /schools/{school-ID}/students/234 { "lastname": "Luthor" }``

## The "benefits" REST is supposed to introduce

Some folks claim that REST introduces the following benefits:

1. It's simple, and easy to understand. You can perform the same actions on all resources, so you don't need to learn the details of a specific API to use it.
2. The API is usable via a browser.

# The problem with REST?

So what's the problem with REST anyway?

## I don't lack experience with it

First of all, a brief recap of my experience here. I started my back-end development career in a company that was using SOAP as its API style. I quickly graduated to REST, and then went on to use it for 12 years. My job has primarily been developing and evolving software products that use HTTP APIs extensively.

I was a big REST enthusiast, and I even used HATEOAS principles when building HTTP APIs. I came to question the whole REST idea only recently.

This doesn't mean you need to take my word for it, I'm just saying that this is not about me being unfamiliar with REST.

## Its benefits are bollocks

First of all, I want to spend a few words about the benefits that REST is supposed to introduce.

1. About being able to use any API without understanding it first: you cannot perform the same actions on all resources, because those actions have business meaning. This is the central argument against REST, so more on this below, but you cannot use any RESTful API immediately just because it's RESTful.
2. About being able to use a RESTful API directly from a browser: browsers only use the ``GET`` and ``POST`` HTTP methods, among the ones REST associates meaning to. You cannot use a RESTful API from the browser, because the ``PUT``, ``PATCH``, and ``DELETE`` methods are not used by the browser, and even the ``POST`` method cannot be used without a UI. Also, even if you could, APIs are for machines, not humans. The user experience would be dreadful if you had to use a RESTful API directly from a browser, without a specific UI for it.

## The fundamental issue

The fundamental issue with REST is that it defines operations that manipulate data structures. It's about structure and structural changes, not behaviour. It's imperative, rather than declarative.

Sounds like a pile of philosophical nonsense to you? Well, it's about to get a lot more concrete.

The problem with this approach is that software products aren't about arbitrary JSON (or XML or whatever) data structures being manipulated. Unless your product stores arbitrary digital records, that is.

So if your business deals with schools and students, it's going to have business-specific operations that have their own meaning.

You don't create a new student under a school, you enlist them. And if a student decides to leave your school, they don't get deleted, a record remains. Replacing a student with another makes no sense whatsoever.

See what's happening here? **REST replaces business-specific operations with generic changes to the structure of some resources**.

## The implications

Is it really that bad though? I mean, sure, it's a bit clunky, but does it really matter? As a matter of fact, it does.

By stripping away the meaning of the business operation, REST guarantees that a RESTful HTTP API will be hard to understand, to use, and to maintain.

If you understand trading, you might look for a way to place a limit order on an asset, or a market order. The action that resonates with you is "place", not "post".

There might be multiple operations that result in the creation or deletion of the same data, and REST doesn't support this very well (or at all, really).

By expressing business operations as data manipulations, REST makes validation a pain. When a user clicks a button, there's a clear business operation that they're performing. Then the client strips away its meaning, by converting it to a RESTful API call. On the receiving side, the server needs to reconstruct the meaning of the original business operation, to process it correctly. Because let's face it, no company (I hope!) blindly applies data manipulations to a record in a database.

So when the server receives a ``PATCH /schools/{school-ID}/students/234 { "lastname": "Luthor" }`` request, it needs to understand that a student has requested for their lastname to be changed, and it then needs to decide what to do about it. What if some fields cannot be changed? What if the value of some fields is constrained by the value of some other fields? By allowing an arbitrary ``PATCH`` operation, these concepts are hard to model and validate requests against.

No company will allow to replace a resource with another, because it makes little sense from a business perspective.

Also, a RESTful API is forced to represent the same business concepts with the same structure across all its operations. This can be quite inconvenient.

And if you rename your business concepts, you need to version your API.

What about the way REST advocates to use HTTP status codes? So when a student with given ID doesn't exist, a RESTful API returns the ``404`` HTTP status code.

This also sucks, because HTTP status codes are about the HTTP protocol, not your business semantics. The ``404 Not Found`` status code indicates that a path doesn't exist. If you use it to say that a student doesn't exist, these two get mixed up. If a client invokes the wrong path by mistake, there's no telling whether it's due to a protocol error or to a nonexistent student.

# The alternative

So what can we do instead? Should we go back to SOAP, with its verbosity? Well, not really. And I'm not talking about ``gRPC`` either.

The idea is to model business-specific operations, and to allow users to invoke these, instead of generic structure-related data manipulations.

The resulting HTTP API tends to always look the same:

``POST`` on ``/commands/{command-type}/version/{command-version}`` and, if you prefer to keep them semantically separated, ``POST`` on ``/queries/{query-type}/version/{query-version}``.

The request body defines the data, using a structure that's specific to the command/query type and version. Basically each command/query is its own API, meaning that if you rename your business concepts, all you need to do is introduce additional commands/queries and deprecate the old ones, without having to version your whole API e.g. the request paths.

Going back to our school example above, you might end up with the following operations:

1. ``POST`` on ``/commands/enlist-student/version/1 { "firstname": "Bruce", "lastname": "Wayne", "joining-date": "2023-09-22" }`` to enlist a student. Want to operate across multiple students or schools? Just accept multiple fields as part of a dedicated command.
2. ``POST`` on ``/queries/enlisted-students-on-joining-date/version/1 { "date": "2023-09-22" }`` to retrieve all students that joined on a given date.
3. ``POST`` on ``/commands/report-student-lastname-change/version/1 { "student-id": "123", "new-lastname": "Kent" }`` to report a lastname change for a student.

See what's happening here? The API is way easier to understand, document, use, and maintain. The server can route and process based on command/query type and version. You can bind a response description for a path in your OpenAPI specification easily. OpenAPI doesn't allow if statements, so an arbitrary REST-style ``PATCH`` is hard to document.

And you get batching capabilities for free:

``POST`` on ``/commands { "commands": [ { "type": "enlist-student", "version": 1, "data": { "firstname": "Bruce", "lastname": "Wayne", "joining-date": "2023-09-22" } }, { "type": "report-student-lastname-change", "version": 1, "data": { "student-id": "123", "new-lastname": "Kent" } } ] }``.

Batching commands and/or queries can have tremendous throughput implications, when applicable.

Last, your semantics can better differentiate between HTTP protocol errors and application level results.

When a requested student is nonexistent, your API can return ``200 OK`` HTTP status code with a ``{ "user": null, "message": "No user exists with the specified ID" }`` response body.

# Parting words

That's it really: **REST replaces business-specific operations with generic changes to the structure of some resources, and that is evil**.

I hope I was able to clearly explain why this is a terrible idea, and what you could and should do instead. I don't hate ``gRPC`` by the way, but I don't think it's a good approach for client to server communications.

So next time you need to design an HTTP API, why don't you stick to business-specific operations and make your users' life and your own life simpler?