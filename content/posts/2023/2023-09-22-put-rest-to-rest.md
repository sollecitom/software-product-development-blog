---
title: "It's time to put REST to rest"
categories: [ "technical" ]
tags: [ "http", "rest" ]
date: 2023-09-22T11:00:00
draft: true
---

# REST is a popular mistake

REST is still going strong these days, with many companies structuring their HTTP API based on its principles. I think that it's a fundamental mistake, and that people should just stop creating RESTful HTTP APIs.

Let's dig a little bit deeper to understand the problem, and some alternatives.

# What is REST: a recap

I won't explain REST in details, but a brief and incomplete summary is that a RESTful HTTP API:

1. Defines resources users can manipulate.
2. Resources have a representation in various data formats e.g. JSON, but even XML or others.
3. Resources are associated to request paths.
4. Resources are nested to model relationships.
5. Some HTTP methods have a specific meaning, representing particular actions a user can do on a resource.
    - `GET` retrieves a resource e.g. `GET /schools/{school-ID}/students/{student-ID}` would retrieve a student `{ "id": "123", "firstname": "Bruce", "lastname": "Wayne"}`
    - `POST` creates a new resource e.g. `POST /schools/{school-ID}/students { "firstname": "Peter", "lastname": "Parker" }`
    - `DELETE` removes a resource e.g. `DELETE /schools/{school-ID}/students/123`
    - `PUT` replaces a resource in its entirety e.g. `PUT /schools/{school-ID}/students/234 { "firstname": "Clark", "lastname": "Kent" }`
    - `PATCH` replaces a field in a resource with a new value `PATCH /schools/{school-ID}/students/234 { "lastname": "Luthor" }`

## The "benefits" REST is supposed to introduce

Some folks claim that REST introduces the following benefits:

1. It's simple, and easy to understand. You can perform the same actions on all resources, so you don't need to learn a given API to use it.
2. The API is usable via a browser.

# The problem with REST?

So what's the problem with REST anyway?

## I don't lack experience with it

First of all, a brief recap of my experience here. I started my back-end development career in a company that was using SOAP as its API style. I quickly switch to REST, and used that for some 12 years, my job being primarily about developing and evolving software products that use HTTP APIs extensively.

I was a big REST enthusiast, and even used HATEOAS principles when building HTTP APIs. Only recently I came to question the whole REST idea. This doesn't mean you need to take my word for it, I'm just saying it's not about me being unfamiliar with REST.

## Its "benefits" fail to materialise

First of all, I want to spend a few words about the benefits that REST is supposed to introduce.

1. You cannot perform the same actions on all resources, because those actions have a business meaning. This is the central argument against REST, so more on this below, but you cannot use any RESTful API immediately just because its RESTful.
2. Browsers only use the `GET` and `POST` HTTP methods, among the ones REST associates meaning to. You cannot use a RESTful API from the browser, because the `PUT`, `PATCH`, and `DELETE` methods are not used by the browser. Even if you could, APIs are for machines, not humans. The user experience would be dreadful if you had to use a RESTful API directly from a browser, without a specific UI for it.

## The fundamental issue

The fundamental issue with REST is that it defines operations that manipulate data structures. It's about structure and structural changes, not behaviour. It's imperative, rather than declarative.

Sounds like a pile of philosophical nonsense to you? Well, it's about to get a lot more concrete.

The problem with this approach is that software products aren't about arbitrary JSON (or XML or whatever) data structures being manipulated. Unless your product is a digital storage of arbitrary documents, that is.

So if your business deals with schools and students, it's going to have business-specific operations that have their own meaning.

You don't create a new student under a school, you enlist them. And if a student decides to leave your school, they don't get deleted, a record remains. Replacing a student with another makes no sense whatsoever.

See what's happening here? **REST replaces business-specific operations with generic changes to the structure of some resources.**

## The implications

Is it really that bad though? I mean, sure, it's a bit clunky, but does it really matter? As a matter of fact, it does.

By stripping away the meaning of the business operation, REST ensures that the HTTP API will be hard to understand and to use.

If you understand trading, you might look for a way to place a limit order on an asset, or a market order. The action that resonates with you is "place", not "post".

There might be multiple operations that result in the creation or deletion of the same data, and REST doesn't model this at all.

By allowing data manipulations, REST makes validation a pain. When the user clicks a button, there's a clear business operation they're performing. Then the UI strips away its meaning, by converting it to a RESTful API call. On the receiving side, the server needs to reconstruct the meaning of the business operation, to process it correctly. Because let's face it, no company (I hope!) will blindly apply data manipulations to a record in a database.

So when the server receives a `PATCH /schools/{school-ID}/students/234 { "lastname": "Luthor" }` request, it needs to understand that a student has their lastname changed, and it then needs to decide what to do about it. What if some fields cannot be changed? What if the value of some fields is constrained by the value of some other fields? By allowing an arbitrary `PATCH` operation, these concepts are hard to model and validate requests against.

No company will allow to replace a resource with another, because it makes little sense from a business perspective.

Also, a RESTful API is forced to represent the same business concepts with the same structure across all its operations. This can be quite inconvenient.

And if you rename your business concepts, you need to version your API.

# The alternative

So what can we do instead? Should we go back to SOAP, with its verbosity? Well, not really. And I'm not talking about `gRPC` either.

The idea is to model business-specific operations, and to allow users to invoke these, instead of generic structure-related data manipulations.

The resulting HTTP API tends to always look the same:

`POST` on `/commands/{command-type}/version/{command-version}` and, if you prefer to keep them semantically separated, `POST` on `/queries/{query-type}/version/{query-version}`.

The request body will define the data, using a structure that's specific to the command/query type and version. Basically each command/query is its own API, meaning that if you rename business concepts, all you need to do is introduce additional commands/queries and deprecate the old ones, without a need to version your whole API e.g. the request paths.

Going back to our school example above, you might end up with the following operations:

1. `POST` on `/commands/enlist-student/version/1 { "firstname": "Bruce", "lastname": "Wayne", "joining-date": "2023-09-22" }` to enlist a student. Want to operate across multiple students or schools? Just accept multiple fields as part of a dedicated command.
2. `POST` on `/queries/enlisted-students-with-joining-date/version/1 { "date": "2023-09-22" }` to retrieve all students that joined on a given date.
3. `POST` on `/commands/report-student-lastname-change/version/1 { "student-id": "123", "new-lastname": "Kent" }` to report a change of lastname for a student.

See what's happening here? The API is way easier to understand, document, use, and maintain. The server can route and process based on command/query type and version. You can bind a response description for a path in your OpenAPI specification easily. OpenAPI doesn't allow if statements, so documenting an arbitrary REST-style `PATCH` doesn't allow business-specific responses.

And you get batching capabilities for free:

`POST` on `/commands { "commands": [ { "type": "enlist-student", "version": 1, "data": { "firstname": "Bruce", "lastname": "Wayne", "joining-date": "2023-09-22" } }, { "type": "report-student-lastname-change", "version": 1, "data": { "student-id": "123", "new-lastname": "Kent" } } ] }`.

Batching commands and/or queries can have tremendous throughput implications, when applicable.

# Parting words

That's it really: **REST replaces business-specific operations with generic changes to the structure of some resources**, and that is evil.

I hope I was able to convey why this is a terrible idea, and what you could do instead. I don't hate `gRPC` by the way, but I don't think it's a good approach for client to server communications.

So next time you need to design an HTTP API, why not stick to business-specific operation and make your own life simpler?