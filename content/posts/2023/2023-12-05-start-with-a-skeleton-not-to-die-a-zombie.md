---
title: "Start with a skeleton not to die a zombie"
categories: [ "software-development" ]
tags: [ "system-thinking", "architecture", "walking-skeleton", "effectiveness", "startups" ]
date: 2023-12-04T05:00:00
draft: true
---

Most companies die a zombie. They start lean and nimble, ship feature after feature, and delight their customers. Then, after eighteen to twenty-four months, the bubble pops, and suddenly they cannot do anything. They limp around painfully until they bite the bullet and re-write their systems, or kick the bucket.

So what happens? What's this hidden killer that shows itself only after a year and a half or two? The problem is that most companies never plan their systems. They start with some functionality, get it out, check what the customers want, and keep doing this.

And it's absolutely the right thing to do. With a big but, though. As a company, you can survive without a well-planned system in place for a while, but you're living on borrowed time. The cost of changing your system steadily increases in this case, until after a year and a half or two, you guessed it, changing anything has a prohibitive cost.

When I say cost, by the way, I mean risk. So you could have a lot of money, but it wouldn't help much. Adding people makes things significantly worse very quickly, as they come up with workaround after workaround.

So what options do you have? Well, it depends on how many resources you have in the beginning.

Most companies won't have almost anything at the start, so make assumptions, validate them, and build prototypes until you identify your product market fit. At some point, you'll have to build a new system from scratch, and migrate your customers to it. Don't make the mistake of avoiding this step.

In other circumstances, you might start as a new large program or company within a parent company with a large amount of resources. In this case you know you'll end up building some product, even if you don't exactly know what, but you're not overly concerned of running out of money. Have two separate systems, one that's a throwaway prototype for quick experimentation, and another one that's well-planned and extensible.

In any case, you cannot build a complex well-functioning system part after part, and you cannot retrofit a large system that's not effective into one that works well. You'll want to start from a bare-bone system that does very little, but does it well: a walking skeleton.

A walking skeleton it's like a Minimum Viable Product, but for your software systems. Its purpose is to prove that your choices and trade-offs achieve the desired system-wide properties you have in mind.

There are a few differences across B2B and B2C, but it's the technical ambitions that determine the scope of a walking skeleton. That's its beauty: it has very little to do with your actual product, or even industry. So you could start building one in a way that's orthogonal to your product discovery efforts.

It's called "walking" because the software is runnable, and it exemplifies the fundamental architectural patterns, approaches, technologies, and moving parts. And it's called "skeleton" because it's a robust system that works, but it does nothing significant: you'll add your product-specific behavior to it after it's ready.

Starting your software system from a walking skeleton offers several benefits:

1. Designing the various parts and aspects together improves the quality of the overall system. This is because the parts are inter-dependent, so you cannot design one aspect without keeping in mind all the others. Simply keeping in mind all the aspects will force you to design things differently.
2. It yields a software system that works end-to-end, so you can iterate on it, and move from a complete system that works to a different complete system that works. This is much safer and faster, de-risking your progress.
3. You can put automated tests in place, to prevent any new functionality from breaking your desired system-wide properties.

Wait a minute though, what about [YAGNI](https://en.wikipedia.org/wiki/You_aren%27t_gonna_need_it)? Are we not wasting time trying to imagine a future that will never happen? Should we not face these challenges when and if they manifest? YAGNI has to do with the scope of your product, not the quality of your system.

What happens if a company doesn't do this? Well, the problem is that the company will still need to design and build the aspects a walking skeleton covers. This is much harder once you have customers using your products, and while you're building new features. You can still overdo a walking skeleton though, so it's certainly a balance.

But you shouldn't just ignore an aspect with the idea that you'll think about it later. This is because the cost of doing something changes dramatically during the lifecycle of a system. Designing is about trade-offs, and these decisions can be hard to reverse.

So if you design your messaging infrastructure one way, ignore tenant isolation, and later on try to design for tenant isolation, you'll find that the way your messaging infrastructure works will also have to change. And I'm talking about fundamental changes. These are only two aspects, but you're actually looking at twenty or more, so when you change your messaging infrastructure, your monitoring, logging, and scaling will also have to change. When any of them changes, other aspects will have to change in turn, and so on. You can't even do this in small steps, as the new parts don't fit with the rest of the existing system.

How long does building a walking skeleton take? Well, there's no standard answer to this. For tiny simple projects, it might only take a week or two. For large initiatives, it'll typically take a competent cross-functional team of senior people four to six months to build a walking skeleton. Projects requiring multi-Cloud, multi-region, or dynamic provisioning will require a longer time for this. I'd say that each of these factors multiplies the time it takes to build a walking skeleton by a factor of 1.5.

Building a walking skeleton is not something you can parallelize much, because of the interdependencies involved in designing an end-to-end system. So, while raising the quality and expertise of the team involved will produce better results, increasing the number of people involved beyond ten or so will actually be counter-productive.

Mind that the goal of a walking skeleton is to dig out the unknown unknowns, and to design a system that can cope with them. It does not require that you build everything. You need to balance You Ain't Going to Need It (YAGNI) with You Ain't Going to Survive It (YAGSI). So you need to cover at least two very different languages for internationalization. But you shouldn't go and build translation packs for every language known to humanity, just in case somebody might need it at some point.

# What should the scope be for a walking skeleton?

Let's have a look at what a walking skeleton should cover. All these aspects should be addressed in a way that they all work together. So it doesn't make sense to build one aspect and then move to the next one. Instead, build them in circles: plan them together, build a prototype, checks if things fit well, adjust, expand, etc.

I'll try to group these aspects by category, but they're all interdependent, so there's no way to lay them out in dependency order. You should read through, understand how things could work together, and then decide whether you'd like the overall resulting system.

I'll sometimes advise for specific approaches: take this with a pinch of salt, or feel free to ignore it, but changing one aspect will likely change how the overall system behaves, and what's achievable. The important thing is that you consider all the aspects, make decisions, understand the trade-offs, and end up with a system that works well end-to-end.

# Tenant and access management

## Authentication

- Standard user journeys for onboarding, invitation, email verification, [Multi-Factor Authentication](https://en.wikipedia.org/wiki/Multi-factor_authentication) (MFA), login, and password reset.
- Single Sign-On (SSO) options, including access via Google, etc. and external [Identify Provider](https://en.wikipedia.org/wiki/Identity_provider) (IDP) federation for B2B.
- Choose between delegated or mapped identity for IDP federation cases. With delegated identity, the external IDP tells your IDP the identity of the user, and you take it at face value. With mapped identity, you map the identity from the external IDP in your own IDP. My advice here is to always map. In any case, you should ensure that when an identity is removed from an external IDP, it also gets removed from your IDP.
- You'll likely need to support both [OpenID Connect](https://openid.net/developers/how-connect-works/) (OIDC) and [Security Assertion Markup Language 2.0](https://en.wikipedia.org/wiki/SAML_2.0) (SAML 2.0), for IDP federation.
- Tenants should be able to federate their IDP with yours programmatically, without you having to enable this manually for them.
- Events for every time a user logs in for the first time, logs in, and logs out.
- Whether to accept email aliases e.g., `bruce.wayne+batman@gmail.com`.
- A login challenge e.g., matching a password hash, something based on signing some bytes on both sides, etc.
- Support for Personal Access Tokens for user accounts, and API keys for service accounts. Because orchestrated authentication workflows don't play well with scripting.
- Password storage implementation (Argon2 or similar to hash, salting, peppering, etc.).
- You should allow users to view their active and historical sessions, including IP address, device type, location, and start and end dates. The user should also be able to invalidate all or specific sessions.
- My strong advice is to stick to a battle-tested open-source solution, like [Keycloak](https://www.keycloak.org/), or to go with a managed service like Okta. Out of the two, I'd go with hosting Keycloak, in general.

## Token management

- Server-side sessions should be avoided.
- Issuing, rotating, and verifying tokens, as part of your authentication workflows.
- Certificate management is a prerequisite for this. You'll need to support tenant-specific certificates, associated with tenant-specific subdomains e.g., `<tenant>.<your-domain>.com`.
- You should include a unique client-side session ID in your tokens, along with the start and end timestamps for the token's validity.
- The authorization roles and containing scopes should also be included in the token.
- The duration of a token should be a maximum of 30m to 1 hour.
- You also need to choose a digital signature scheme. [EdDSA](https://en.wikipedia.org/wiki/EdDSA), ideally, rather than RSA or ECDSA, as it's faster, requires shorter keys, and it's considered more secure.
- In terms of token structure, [JWT](https://en.wikipedia.org/wiki/JSON_Web_Token) is a safe bet.

## Tenant isolation

- Tenants should be isolated from each other in terms of workflows.
- The data for a tenant should be stored and encrypted separately from the data of other tenants.
- Each tenant should be able to set up Single Sign-On with their own IDP, and to enable [Mutual Transport Layer Security](https://www.cloudflare.com/learning/access-management/what-is-mutual-tls/) (mTLS) and IP address range restrictions.
- As mentioned above, you'll need tenant-specific subdomains e.g., `<tenant-name>.<your-root-domain>.com` for this. This needs to happen automatically when you onboard a new tenant.
- If you offer environments, you'll likely need infrastructure isolation to prevent the activity from one tenant to affect the workflows of another tenant.
- Different tenants might require different encryption keys, physically segregated storage, and different locations for their data.
- Data residency regulations require that data for customers in a Country is also going to be kept in that country (some Countries require "only" instead of "also", but very few).
- You'll need to implement at least two tenants for each tenant type, as part of your walking skeleton.

## Tenancy model

- Your users will belong to different tenants, but a tenant will likely be too big to map to a single namespace.
- You should allow your tenants to define more granular groups of users. You could choose to model these groups as projects, spaces, teams, or organizations.
- My advice is to avoid choosing one model, and allow arbitrarily nestable containers, similar to folders. This way, a tenant can model their own organizational structures within your product, and allocate users and resources according to where they live in their own company.
- The property of belonging to a container should cascade down the hierarchy. So if a tenant creates a "Global" folder, "US" and "EU" folders underneath it, and a "France" folder underneath "EU", anything within "France" will also need to be within the "EU" and the "Global" folders.
- These nestable containers can be used as containing scopes for authorization. So if a user has the "Project-Accessor" role within the "France" scope, they'll see projects in France, but a different user with the same role in a different scope won't.
- These groupings are also useful for billing insights, so that billing contributions can be tagged with the containing scope they were produced in, allowing to roll them up hierarchically, according to the tenant's own organizational structure.
- As part of your walking skeleton, model at least two branches of the organizational hierarchy for each tenant, and do that for at least two separate tenants.

## Authorization

- My advice is to model resources (the things your product allows to interact with), actions (what you can do with a resource), and container scopes (nestable groupings of resources).
- I also advise defining policies as sets of action-resource permissions, and creating roles that are associated with bundles of policies. A user then has multiple roles, each associated with a containing scope. So when a user is in a given context, it has certain roles active in that context, and inherits some permissions through the policies associated with those roles, as a result.
- Authorization should be checked and enforced once per invocation. If the grants for a user change, in-flight invocations should complete with the grants they had at the beginning of their processing.
- You also need a way to query this, both on the front-end (to hide or gray out things the user cannot perform) and on the back-end (to enforce authorization rules).
- On the front-end, you should retrieve the roles and the containing scopes from the user's token, then look up the policies and permissions granted by those roles, from a dedicated endpoint.
- You'll need some standard available roles, plus the ability for your customers to define their own. To do this, you should describe what actions and policies each resource offers.
- You should support mapping groups in your tenant's Identity Provider to roles and scopes in your domain. So that if a customer's employee is in the "UK" and the "developers" group, they might be associated with the "Standard User" role in the "UK" "Production" scope, and with the "Admin" role in the "UK" "Test" scope.
- I recommend using a standard way of defining and querying authorization permissions and policies. [Open Policy Agent](https://www.openpolicyagent.org/) (OPA) is an excellent choice.

# High-level architecture

## Main architectural patterns

- You'll need to choose whether to use orchestration (the logic is centralized in a controller, which dispatches calls to other services) or choreography (the logic is distributed, with each service reacting to what the other services are doing). [A longer explanation of these two approaches](https://temporal.io/blog/to-choreograph-or-orchestrate-your-saga-that-is-the-question).
- The choice between orchestration and choreography is for each workflow and subsystem. My advice is to adopt service choreography for every workflow and subsystem.
- Choose whether to have as your source of truth the snapshot of the current state, or the history of the state changes. [A longer explanation of these two approaches](https://www.eventstore.com/blog/what-is-event-sourcing). [Another explanation](https://developer.confluent.io/courses/event-sourcing/event-driven-vs-state-based/).
- This is also a local choice, so that each subsystem could choose a different approach. My advice is to record the history of state changes and use that as your source of truth, for all the subsystems.
- I also recommend [Command Query Responsibility Segregation](https://en.wikipedia.org/wiki/Command_Query_Responsibility_Segregation) (CQRS). This means that commands (invocations that mutate the state without retrieving it) are processed by subsystems that are separate from the ones that process queries (invocations that retrieve the state without mutating it).

## Event-driven workflows

- Event-driven architectures work well with a partitioned distributed ledger as the backbone of event propagation.
- [Apache Pulsar](https://pulsar.apache.org/) and [Apache Kafka](https://kafka.apache.org/) are both open-source and very popular. My recommendation is to go with Apache Pulsar, which I find superior to Kafka in every possible way. You should probably host your own Pulsar cluster, as it's much easier than hosting Kafka, and much cheaper than a as-a-service commercial solution.
- You should consider whether storing the events indefinitely within your distributed ledger (with tier storage backed by object storage, like S3 and Glacier), or whether using your ledger for propagation and a separate technology for events.
- My advice is to have a store for events, like [EventStore](https://www.eventstore.com/eventstoredb) or even [Postgres](https://www.postgresql.org/).
- You'll need a mechanism to handle [Personal Identifiable Information](https://en.wikipedia.org/wiki/Personal_data) (PII) with regard to GDPR's Right To Be Forgotten. Storing PII as part of the events with field-level encryption using per end-user symmetric keys is a good approach. When the user needs to be forgotten, you can unlink the key, without losing data integrity.
- Whenever you need to enforce domain rules that depend on the current state, you'll have to choose between the [outbox pattern](https://en.wikipedia.org/wiki/Inbox_and_outbox_pattern) (write to a DB, then derive publishing an event), or [the saga patter](https://en.wikipedia.org/wiki/Compensating_transaction) (read from an eventually consistent view, decide in memory, publish an event, eventually update the view, rollback the changes and refund if there are conflicts). My advice here is to use sagas, as the outbox pattern is tricky and constitutes a severe limitation in throughput.
- As your system is fully asynchronous, message-based, and reactive, you can use the [async request-reply pattern](https://medium.com/@mahernaija/messaging-patterns-cf4bc5b164cf) to respond to queries synchronously.
- My advice is to use [NATS](https://en.wikipedia.org/wiki/NATS_Messaging) for this. You generate a unique response NATS topic, subscribe to it, emit an event tagged with the response topic, await for a downstream service to publish the outcome of your workflow to NATS, and finally respond to the open socket. MQTT works well for this too, but it's quite a heavy technology to deploy.

## API style

- In terms of API style, you'll have to pick one and stick to it for your whole API surface. Examples of API styles include [REST](https://en.wikipedia.org/wiki/REST), [GraphQL](https://en.wikipedia.org/wiki/GraphQL), and [RPC](https://en.wikipedia.org/wiki/Remote_procedure_call).
- My advice is to adopt an RPC style. GraphQL and REST both operate at data manipulation level, but what you want is domain-specific actions. I'm not talking about [gRPC](https://grpc.io/) by the way, as it brings its own protocol tweaks and doesn't work well with many existing tools. Go over standard HTTP 2, and use either [JSON](https://en.wikipedia.org/wiki/JSON) or [Avro](https://en.wikipedia.org/wiki/Avro) as data format. I'd recommend Avro, but JavaScript in the browser supports it poorly, so even JSON works fine.
- So use the POST HTTP method, with the type of the invocation as part of the path, and choose whether to differentiate commands and queries. Examples include `POST /commands/tranfer-account-ownership`, `POST /queries/retrieve-available-balance`, and `POST /invocations/tranfer-account-ownership`.
- You can specify caching instructions for POST responses, but my advice is to avoid caching responses as much as possible. If you really need that performance, subscribe to changes on the client side.
- This approach enables bulk invocations endpoints e.g. `POST /commands`, `POST /queries` and `POST /invocations`, so a client can send multiple invocations in one exchange with the server.
- This way, it's easy to record all the invocations that happened, whether commands or queries, to provide full auditability.

## Server-push data

- Your back-end will need to sometimes push data to your client applications. This means the server will initiate a communication with the client, rather than the other way around.
- You should either host a solution, like an [MQTT](https://mqtt.org/) cluster, like [EMQX](https://www.emqx.io/), or going for a commercial solution, like [Ably](https://ably.com/).
- My advice is to avoid websockets, as they introduce connection stickiness (you need to know which socket to use to send a message to a user), and they're too low level.
- A user shouldn't be able to subscribe to information they shouldn't see (data belonging to other tenants or users), so you'll need authentication and authorization.
- You'll need to structure your topics carefully, balancing authorization needs and the effort involved in pushing an update. So a topic per user makes authorization trivial, but pushing updates a nightmare. A single topic is the opposite. You'll need a balance.
- My advice is to use a hosted open-source solution when you plan on sending server-pushed information often, as the cost builds up with commercial solutions.

## Gateway and services

- Choose whether to leverage an API gateway, or to go without one. My advice would be to use one, so you can centralize token signature verification, authorization enforcement, parsing of tracing information, [CORS](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing) handling, [TLS termination](https://en.wikipedia.org/wiki/TLS_termination_proxy), and other similar aspects. I also recommend hosting an open-source or a commercial solution, rather than buying a service.
- You'll want to create templates for the various types of services that appear in your topology. Command endpoints (receive and emit commands), query endpoints (serve queries), event processors (receive and emit events), event sinks (receive and consume events, typically integrating with third-party technologies, or updating materialized views).

# Correlation

## Invocation context

- Every invocation should be contextualised with metadata about the invocation itself.
- This context should be part of your software models, not something implicit and accessed outside the normal call stack. You should be able to base your behavior on this information, to log it, and to include it in the events you publish.
- The context should contain information about the access, the trace, and the toggles associated with the invocation.
- The toggles associated to an invocation are a set of key-value pairs, where the key is a feature toggle ID, and the value is the type-safe value for that feature. This can be used for A/B testing, to bump the logging level for an invocation, and for many other use cases. Mind that these toggles are per-invocation, so they shouldn't contain things like product tiers, etc.
- The access should include authorization information, provenance information (client IP address, parsed user agent, etc.). It should also indicate whether the invocation was unauthenticated (for operations exposed outside of login) or authenticated. For authenticated accesses, information about the actor should also be included. This should indicate the account ID, whether it's a user or a service account, the tenant the actor belongs to, the locale of the user, and the authentication mechanism (including client-side session ID or the hash of the API key used). The actor model should also support impersonation and acting on behalf of other accounts.
- The trace should allow correlating invocations that are logically related. A good way of achieving this is to generate some initial unique IDs (e.g., [ULID](https://github.com/ulid/spec)s) on the client side: 1 for the action itself e.g., a button press, plus 1 for each invocation to the back-end this action results in (typically one). After that, the gateway should generate an originating trace ID, and these 3 pieces of information should be immutable throughout the chain of invocations. Each service that processes the invocation should receive a parent invocation ID, generate an invocation ID, and send this last ID as parent invocation ID for downstream calls.
- This way humans and systems can easily identify retries and invocation that are logical duplicates of previous invocations.
- The information in the invocation context allows determining an idempotency key: this one is typically the external invocation ID, within a namespace composed of the tenant ID and the actor ID (so that different actors and tenants cannot interfere with each other in terms of idempotency).
- An application should receive the full invocation context from the gateway (typically encoded as JSON and to Base64 in a header), fork it (generate a unique invocation ID, and move the received invocation ID as new parent invocation ID), add it to the log stack, pass it as an argument (or as a context parameter) to all functions, include this information in every event, and send this as a header as part of any downstream HTTP request.
- Every event and message should also have their own context information, which is the ID of the originating and the parent events and messages. So each event has an event context, which includes the invocation context, and event correlation information. Each message (the event might be in the payload), will also contain message correlation information.

## Idempotency

- The invocation context gives you an idempotency ID.
- You can use this ID to ensure that logically duplicated calls do not cause duplicated side effects, including state changes and calls to external systems.
- For SQL databases, you can use a transaction that inserts this ID into a dedicated table of previously seen invocations, with a unique constraint. As part of this transaction, you can do whatever that invocation needs to do from a business perspective. If the transaction fails because of the idempotency constraint, you should consider the operation successful, and proceed with anything else you would normally do if it completed regularly.
- For external APIs, some will allow you to specify an idempotency key. In this case, you simply pass your external invocation ID, and the 3rd-party system will take care of idempotency on its end. This works the same for your system, since your clients can choose to repeat the external invocation ID, if they want to retry an invocation in a safe way.
- Some 3rd-party APIs e.g., email senders, won't allow you to specify an idempotency ID. In this case, you can use a SQL database to filter out duplicates, as per above except for skipping the call to the external system in case of a uniqueness constraint failure with the idempotency ID. This approach does not guarantee idempotency, because if you cannot transactionally invoke the 3rd-party API and your database, so if you crash in between, you can end up with duplicate invocations.

# User-facing applications

## Internationalization

- All strings should be represented using the UTF-16 or UTF-8 charsets. UTF-8 can represent any character, but it's optimized for text that is mostly ASCII. So it depends on the intensity of this requirement. In any case, stick to UTF-8 at a minimum, even if you don't currently have any internationalization requirements.
- The frontend applications should externalize all text content, so that a different value can be used based on the browser's locale. When the locale changes in the browser, this should also be changed.
- The backend should return these internationalization keys, rather than text in English, for everything.
- The actual values should be packaged in the app itself, falling back to a [Content Delivery Network](https://en.wikipedia.org/wiki/Content_delivery_network) (CDN) lookup. This allows trading off chattiness and app size, and changing text without having to release.
- All communications e.g., emails and in-app notifications should respect the locale of the user, falling back to a default locale, if the user's locale is not currently supported.
- If you plan to support Arab countries, or Asian countries like China and Japan, you should also change the page layout based on the user locale, as some of these languages are laid out differently.

## In-app notifications of changes

- You should model new features, marketing communications, etc. as code, and notify your users about them both in-app and through emails. The notifications should link to a browsable changelog of all historical changes to your products.
- This changelog should be an append-only log of changes, so that a user can browse and search them. Each item in this list should take the user to a page with more details about that specific change.

## In-app audit log

- Users should be able to browse, filter, and inspect a changelog with all the actions they ever performed.
- If a user has the specific permission, they should be able to also see in the changelog the actions performed by other users.
- Each item in the audit log should contain the full context of the invocation represented by that item, with dates, access, etc.

## Displaying and reporting errors

- You should display meaningful error messages when something goes wrong, in the user's locale (with fallback, if not supported). These shouldn't be protocol-level error messages e.g., 403 Forbidden, but properly crafted messages, explaining what went wrong, and what the user should do about it.
- Some types of errors should offer the user the option to retry, automatically using the same external invocation ID for idempotency.
- All unexpected errors should ask the user to report the error, automatically adding correlation information about the invocation. Reporting an error should create an entry within an in-app error investigations section, and retry the invocation with bumped up logging level (using a toggle) and same external invocation ID (for idempotency).
- This should alert your back-office. Once the error is fixed, a back-office user can provide information about what happened and what was done about it. The open investigation should be updated, and the user should receive an in-app and an email notification.

## Accessibility

- If you have any accessibility requirements, and probably even if you don't, you should ensure your client applications are accessible.
- You should create automated tests to prevent regressions (using tools like [Wave](https://wave.webaim.org/), [Axe](https://www.deque.com/axe/), and [Pa11y](https://pa11y.org/), https://opensource.com/article/23/2/automated-accessibility-testing), so that what's accessible doesn't lose this property at some point in the future.

## In-app and off-app learning

- You'll need to walk your users through your product.
- This can be a mix of in-app resources e.g., a guided walkthrough and your product's documentation, and off-app resources e.g., videos on YouTube.
- In any case, you should list these resources in-app, and guide the users through their journey.
- My advice is to use an existing product tour tool, rather than trying to roll your own. [Here's a selection of some options for this](https://www.storylane.io/blog/11-best-product-tour-software-for-saas).

## History of changes for each entity

- Your product will expose specific entities, allowing users to manipulate these entities to achieve their goals.
- You should ensure that your users can browse and search the history of all changes that happened on any one of such entities.
- An example might be that, if your product allows users to create projects, any user with permissions should be able to see the whole history of changes on a specific project: who created it and when, the original data, the log of changes, each including who did what, when, and how.

## Multiplatform strategy

- If you ever need more than platform e.g., iOS, Android, and web, you'll need to decide between leveraging a multiplatform approach (like [React](https://react.dev/)/[React Native](https://reactnative.dev/), [Kotlin Multiplatform](https://kotlinlang.org/docs/multiplatform.html), etc.), and adopting separate codebases and technologies for each channel.
- In B2B, it almost always makes sense to go with a multiplatform approach. In B2C, your users will tend to be mobile-first, so going native might sometimes be preferable.
- However, this is not a rule, so make an explicit decision, keeping in mind the number of specialists you'll need, and how exacting are your platform-specific requirements.

## UI components

- You'll want to curate a set of UI components to avoid duplication and achieve a consistent user experience, throughout your applications.
- You should be able to compose these into higher-order components and workflows.
- You should be able to test each component in isolation.
- These components should be versioned and maintained as a library.

## Modules, features, and billing

- Your products will contain various modules and features.
- You'll need to model these explicitly in your code, so that a new module can be released without having to release the front-end applications.
- You should be able to bill based on a combination of a base tier, plus a consumption-based contribution. In any case, you should be able to clearly explain your bills, with hierarchical roll-ups based on nested containing scopes.
- Whenever a tenant would have exceeded their maximum quota of operations, you should be able to automatically disable further actions from that tenant, until they expand their subscription or a new billing cycle starts.

## Instrumentation and attribution

- You should instrument your products, so that you can learn what your users are clicking, doing, etc.
- These events should be captured within the client applications, and sent to the server or to a 3rd-party service.
- Instrumentation should include both low-level actions e.g., clicks, typed text, etc. and high-level intentions e.g., logged in, created a project, changed the permissions of another user, viewed the list of projects, etc.
- You should also be able to attribute events to user-specific toggles, to gauge the impact your tweaks had on the KPIs they hoped to improve.
- My advice is to use an external tool for both instrumentation and attribution. Examples could be [Amplitude](https://amplitude.com/) for both, or [Pendo](https://www.pendo.io/) for instrumentation and [Split](https://www.split.io/) for attribution.

## Requirements and entitlements

- Some features, modules, or products will come with additional requirements.
- Even just accessing your platform will likely have some basic requirements e.g., a valid email address.
- You should model what requirements each feature, module, product, or platform needs, before a user can access it, within your code.
- Each requirement could be satisfied by various alternative entitlements. You should model which entitlements satisfy a requirement. This can vary based on the country, etc.
- An example might be that a valid email address requirement could be satisfied by a passed email verification check, or by receiving a corporate email address from a federated identity provider.
- Users should be associated with the set of entitlements they already have. A product with requirements that already satisfied by the entitlements a user has shouldn't ask the user to do anything else.
- You should be capable of disabling functionality the user hasn't qualified to use yet, of explaining which requirements aren't met yet, of showing the available ways of qualifying for each requirement, of running the verification step for the entitlement chosen by the user, and finally of unlocking the feature when all the requirements are met.
- Requirements and entitlements should be dynamic, sent by the server to the client as data. Your client applications shouldn't know which requirements a product or feature needs. The same product might have different requirements across different countries. And a requirement might be met by different entitlements, in different countries.
- This works very well with components. So a requirement might be "having accepted the terms and conditions with ID 123", an entitlement might be "digitally signed a document showing the terms and conditions with ID 123", and you could have a component for this entitlement, so that any time a product or feature needs terms and conditions signed, you can re-use the component as part of that workflow.

## Documents and reports

- You'll likely need to develop the ability to produce PDFs for terms and conditions, and for reports.
- Legal documents should be stored in an immutable way, rather than being produced again in the future.
- So if you're a bank and a user produces a statement of their transactions, you should store that statement, so that the user is guaranteed to access the same statement in the future, even if you change your business logic.

## SDKs

- You should abstract all communications to and from the back-end with client-side SDKs.
- Each SDK should be built, tested, versioned, and released as a stand-alone library.
- Each SDK should have a contract-only module, and various implementations e.g., HTTP-based + MQTT for server-pushed communications, or an in-memory implementation for local testing.
- You should test your client applications against an in-memory version of the SDK, not against an environment hosting your back-end.
- You should use reactive-streams e.g., [RxJS](https://rxjs.dev/) or [MobX](https://mobx.js.org/README.html) to allow the client to subscribe to server-pushed data.
- You should use the SDK to write tests that don't test the UI e.g., smoke tests you can run periodically in production.
- You should have test extensions for your SDKs, allowing you to easily create preconditions that wouldn't make sense as normal operations.
- You might want to give your client-facing SDKs to your customers. You shouldn't give your customers the test extensions.

# Infrastructure

## Only one long-lived environment

- You should have only one long-lived environment: production. So no test, UAT, or staging environments.
- If you support dynamic environments, every such environment should be production for you. If your customers want a test environment, this should still be a production environment for you. To understand this better, think about how Cloud providers work.
- Learn how to test locally, and leverage internal tenants to test and demo your changes before releasing them to external tenants.
- Use ephemeral short-lived environments to perform intense tests e.g., stress performance tests, or to test large-scale infrastructure changes.
- These ephemeral environments should be exact copies of the production environment, with masked sensitive tenant data, and you should be able to spin them up and down programmatically.

## Infrastructure as code

- You should describe your entire infrastructure and tenant configuration in a declarative way, as code.
- Changes in the code should trigger changes in your infrastructure.
- You can use various approaches for this, including [Pulumi](https://www.pulumi.com/) and [Terraform/OpenTofu](https://opentofu.org/).
- My advice is to use Pulumi, as it allows you to dynamically declare resources based on runtime data. You can also create your own types and functions, and it's easier to compose.
- You should monitor your infrastructure, checking for divergences between the declared and the actual state. A configuration drift management tool can help you spot these inconsistency, raise alerts, and even roll-back any undeclared changes.
- Structure a mechanism for requesting and granting temporary and audited access (read or write) to resources. These requests need to be approved and recorded. Nobody should have direct access to any database, network, console, or anything.
- In terms of provisioning, a fully scripted approach works well, except when infrastructure needs to be provisioned as part of some users' actions. In this case, you'll need dynamic provisioning, and Terraform and Pulumi can leave you with an inconsistent state in case of failure. [Kubernetes Operators](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/) are a better approach in this case.
- My advice would be to use Pulumi to set up [Kubernetes](https://kubernetes.io/) and install a bootstrap Operator, and then use [Kubernetes Operators](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/) for everything else, even when you don't have dynamic infrastructure provisioning requirements.

## Configuration management

- Your applications will need configuration variables, secret keys, certificates, passwords, etc.
- These might depend on the specific tenant the invocation belongs to. Two tenants might use separate databases, each with their own credentials.
- Whenever you can, avoid injecting these variables into your applications at all. Instead, use side-cars that proxy the connections or do the work that requires the secrets.
- When not feasible, use a standard way of injecting configuration, like [Kubernetes ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/), or file-based configuration exposed to the apps through ephemeral volumes.
- In terms of storing secrets, you'll want something audited, segregated, and secure, like [Hashicorp Vault](https://www.hashicorp.com/products/vault). You don't want each application to interact with Vault directly, though. So either expose the secrets in Vault through [Kubernetes Secrets](https://kubernetes.io/docs/concepts/configuration/secret/), or pass them to your applications inside files on ephemeral volumes.
- You should ensure that whenever a configuration value changes, your applications can pick up the change. I recommend rebooting the containers in this case, as it's usually not a big deal.
- All credentials should be service-specific, never shared by multiple applications.

## Certificate management

- Your products will use certificates, and those certificates will need rotation, etc.
- In multi-tenant contexts, each tenant will likely end up with its own subdomain and its own certificates.
- Figure out how to manage dynamic certificates: either by issuing them through a root certificate, or by rolling your own [Certificate Authority](https://en.wikipedia.org/wiki/Certificate_authority).
- Whenever a tenant or an infrastructure zone requires its own certificate, you should be able to issue it programmatically.

## Internet Edge Solution

- An internet edge solution, like [Fastly](https://www.fastly.com/) or [CloudFlare](https://www.cloudflare.com/) is almost always a great idea.
- You get protection from DDoS attacks, and against other malicious attempts.
- Also, you can allow your tenants to enable mTLS and IP address range restrictions programmatically, by calling the internet edge solution's API as part of handling such a command on your back-end.
- My advice is to use [Fastly](https://www.fastly.com/), as it's usually powerful and easy to integrate with.

## Cloud providers

- You'll need to decide whether having single Cloud provider availability and business continuity is enough.
- If so, then my advice is to stick with [Google Cloud Platform](https://cloud.google.com/) (GCP). It's cheaper than the others, and offers great essential products e.g., the managed Kubernetes service.
- If you need a multi-Cloud approach, you'll need to figure out whether active-passive-cold is enough, or whether you need active-passive-hot or active-active.
- In any case, the way this should work is that, when your active Cloud provider has an issue, you should be able to switch to another Cloud provider with 1 click.
- You should aim at being able to switch without losing any data, and with zero downtime (that's where active-passive-hot and active-active come into play).
- Active-passive-hot and active-active multi-Cloud workflows are rare and hard, but they can be achieved in a similar way active-active multi-region workflows work.
- You could deploy a messaging cluster on each Cloud provider, and then replicate each command across all clusters, ensuring that each replicated command ends up having the same offset across different clusters. Apache Pulsar can help with this, with its geo-replication features. Once you have this, you can enable/disable the side effects in your passive Cloud provider, but it'll be ready and eventually consistent with the active one.
- If you need a multi-Cloud approach, you should use at least three Cloud providers as part of your walking skeleton. This is because you'll need quorum to recover from a temporary failure, so you'll need three Cloud providers at a minimum, if one is not enough.

## Regions and Availability Zones

- Depending on your availability and disaster recovery requirements, you'll need your services across multiple Availability Zones, or even across multiple Regions. [More information about Regions and Zones](https://cloud.google.com/compute/docs/regions-zones).
- Active-active and active-passive-hot multi-region workflows are hard, just like it's hard to get these working well across multiple Cloud providers.
- The difference is that multiple Cloud providers introduce higher management complexity, while multiple Regions introduce higher latency involved in your replication.
- If you have multi-region requirements, you should test in at least 3 regions as part of your walking skeleton. This is because you usually need quorum to recover from a temporary failure, so the minimum regions you'll need is 3, when 1 is not enough.

## Service registry

- You should have a service registry, listing all your existing services.
- Each service should have an identity in the form of a unique identifier e.g., a [ULID](https://github.com/ulid/spec).
- Each service should show which infrastructure resources they depend on, along with the libraries and versions they use.
- You should be able to see all services that use a dependency version affected by a vulnerability.
- Every service should also link to its codebase on version control.

## Messaging

- Your messaging infrastructure will need authorization, auto-scaling, replication, partitioning, etc.
- You should have a service registry in place, and a way of authenticating services. mTLS is a good way of doing this, if you issue per-service certificates, with rotation, using sidecars to proxy the communications.
- In terms of authorization, [ACLs](https://docs.streamnative.io/docs/access-control) work well, but a custom [Authorization Provider](https://pulsar.apache.org/docs/next/security-extending/) using [Open Policy Agent](https://www.openpolicyagent.org/) (OPA) is better. Both Pulsar and Kafka support this. The way it works is that you can declare a custom Authorization Provider as a plugin extension, and your broker will ask it whether a service is allowed to publish or subscribe to a topic, caching the result afterward.
- Partitioning and [cluster auto-scaling](https://docs.datastax.com/en/streaming/kaap-operator/0.1.0/) are much easier with Pulsar than they are with Kafka, because Apache Pulsar's brokers are stateless. You'll need to template both aspects as part of your walking skeleton.
- You should also have a company-wide registry of topics and schemata (typically in [Apache Avro](https://avro.apache.org/)). So that each developer should know what topics exist, what are they for, and what schema is published to that topic.
- Your cluster should be configured to reject messages whose payload is backward or forward incompatible with the schema set for the topic. [An overview of how this works in Pulsar](https://pulsar.apache.org/docs/3.1.x/schema-understand#schema-evolution).

## Service-to-service communications

- Ideally no two services should ever know of each other's existence, exclusively publishing and receiving events instead.
- If you must have peer-to-peer communications, service mesh will help manage this.
- By using peer-to-peer communications you lose a lot, in terms of backpressure, security, extensibility, etc. so think really carefully whether you really have to.
- For external services, you'll need peer-to-peer communications anyway. My advice is to structure proxy services for 3rd-party dependencies, so that your applications are not concerned with certificate management, credentials, etc.

## Outbound invocations

- If your applications initiate outbound invocations to a tenant's infrastructure, you'll need to somehow prove these are genuine and originated from the right environment.
- For webhooks, you should consider [HTTP Message Signatures](https://httpwg.org/http-extensions/draft-ietf-httpbis-message-signatures.html).
- Each tenant-specific area of your infrastructure should generate a key pair (with rotation) used to sign outbound requests.
- The receiver should retrieve the public key from a well-known endpoint exposed under the tenant-specific subdomain (so protected by mTLS, IP address range restrictions, etc.), and use the key to verify the signature.
- Like for calls to external services, my advice is to use proxy services to produce and attach HTTP Message Signatures to outbound invocations, so that your applications are not concerned with certificate management, credentials, etc.

## Autoscaling for services

- You'll want CPU-based auto-scaling groups, for command and query endpoints, as their driven by push-based unpredictable external traffic.
- For event processors and event sinks, CPU-based autoscaling makes no sense, as these process messages out of a queue. Instead, you'll want to scale their consumer groups based on the derivative of their queue size: if they're falling behind the producers, ramp up, and if they're catching up fast, ramp down.

## Monitoring

- You should have dashboards and alerts for both product and infrastructure-related aspects.
- In terms of infrastructure, things like CPU, memory, number of inbound and outbound connections, error rate, available disk space, etc.
- About product aspects, stuck workflows that are not progressing through the steps after a given time (using sagas for this), brute-force login attempts, suspicious patterns, etc.
- You should also have health checks and readiness checks for each service, along with an external availability check service e.g., [Pingdom](https://www.pingdom.com/), to check whether your platform is available to the outside world.
- Any error-level log entry should trigger an alert to be investigated.
- My advice is to use open-source tools for monitoring and for dashboards e.g., [Prometheus](https://prometheus.io/) and [Grafana](https://grafana.com/), as opposed to commercial solutions like [Datadog](https://www.datadoghq.com/), as these can get very expensive fast.

## Releases and deployments

- You'll need automatic canary deployments, gradually incrementing the amount of traffic directed to the upcoming version, based on comparing the error rate with the baseline for the old version.
- Each invocation that failed on the new version should be retried on the old version, to ensure there's no downtime (remember: you should have idempotency throughout).
- A failed release (error rate increased beyond the acceptable) should be rolled back automatically, with alerts, so the development team can investigate.
- For back-end applications, you'll likely want a continuous deployment model, where each successfully built change is released to production and enters into effect immediately.
- For web and mobile applications, you'll want a similar deployment model, but the changes should be deployed with feature flags that make them inactive, to be activated at a later stage based on marketing campaigns, etc. For mobile, you should batch your changes, so that a new version is published to the app stores only once a week or so.
- Data migrations should be performed as part of the release, by [Init Containers](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/). You should be able to control when your migrations run, so that some run before the new instances come up, some during the release, and some only after all the old instances have been brought down.

## Logs

- Each service should be able to log in plain statements, or in JSON, based on a configuration variable passed at runtime. The default should be JSON, overridden locally to be plain instead.
- Each log entry should comply with a company-wide JSON schema. Services should be tested to check whether the log lines they produce comply with this schema, as part of the build pipelines.
- The `Invocation Context` should also have its own schema, included as an optional field in the log entry schema.
- Logging long strings is incredibly slow in general, so the default minimum log level should be kept to `DEBUG`, and `INFO` should never be used as part of normal workflows.
- An invocation should be able to specify a toggle to bump the produced logged level from `DEBUG` to `INFO`.
- Does this mean that most workflows won't produce any logs? No, because an event sink can map each produced event into a log line, asynchronously, without slowing down the processing itself.
- So why do we need to occasionally bump the log level to `INFO`? Or why log directly from the apps completely? That's because, sometimes, weird things happen, and an application ends up not being able to publish events. Or you might be interested in how the inside of an app is working.
- The events are already recorded forever, so no point in mapping them as logs that are also kept forever. You can keep the direct application logs for a while (1 month, or something similar), and merge these on demand with the event logs, when an employee wants to investigate something.
- Imagine you're having a live incident, you can ask your logging system to give you all the logs for a given invocation ID. Your system will merge the direct logs from the application containing that ID, and re-consume all events with that invocation ID, to produce a search space for you. Your system should show the whole tree of correlated logs and events.
- If you create wrapping types for Personal Identifiable Information (PII) and secrets, you can easily avoid these being leaked in the direct application logs, and you can mask them when bringing them into the search space.
- My advice is to use open-source tools for logs collection and searching, like [Kibana](https://www.elastic.co/kibana), as commercial solutions can quickly get expensive.

# Application development

## Codebase

- You should choose whether you want a mono-repo or different repositories for your services.
- Even when you use multiple programming languages (hopefully always), mono-repos make local development a lot easier, so this is something to consider.
- If you use multiple languages and adopt a mono-repo, consider grouping your projects under language-specific folders. This is going to make your life easier when working with IDEs.

## Frameworks and libraries

- You'll need to figure out how to cover a range of table stakes, including configuration parsing, etc. You don't want to implement these low-level concerns yourself.
- Choose libraries and frameworks that make your life easier, without becoming too attached to them, and avoiding the ones that are too opinionated or that significantly slow down application startup.
- You should be able to check for new versions of every library a service uses, and to update them, with one command.
- Each service should have a scheduled job to update all dependency versions (libraries, build tools, plugins, programming languages, frameworks, etc.), run the tests for that service, open a PR to update those dependencies if the tests pass, and automatically merge it. If the tests fail, the job should alert the development team.

## Event-driven optimizations

- For event-processors, you'll want to process an event on only one thread.
- Ideally your processing should happen in-memory. Your service processes the inbound event, and update its in-memory state.
- A separate process aggregates your outbound events into a state snapshot, using the partition as key, and including the offset the snapshot is valid at.
- When your processor starts, it gets assigned a set of partitions, loads the state snapshot for each of them, and then compares the offset of the snapshot with the offset of the inbound message.
- If the snapshot is behind, the processor simply reprocesses the events between the offset of the inbound message and the offset of the snapshot. The service applies the state changes to the in-memory state, and it's back, ready to correctly process the inbound message it received when starting up.
- For event sinks, you should adopt batched processing if the service is not on the critical path. As an example, a sink that updates a materialized view could batch every 5000 events or every 1 second, whichever happens first, and do 1 database batch insert instead of 5000 inserts and round-trips.
- Perhaps unsurprisingly, in-memory processing hugely reduces latency while achieving great throughput, while batched processing enormously improves throughput.

## Shared libraries

- Some people swear by shared libraries, and some other folks swear when they see them. In any case, you should make an explicit decision about this.
- Shared libraries are only available to programming languages compatible with the language they're written in. So mixing multiple programming languages in the same area e.g., web apps, or back-end apps can be a pain.
- Avoid home-made frameworks at all costs. Home-made libraries are okay. The difference between frameworks and libraries is that frameworks are heavily opinionated and require full buy-in, while libraries are modular and can be easily replaced.
- If you decide to use shared libraries, each should be developed, versioned, built, tested, released, and documented like an external library.
- Shared libraries can be powerful to offer well-thought plug-and-play behavior that would be expensive and error-prone to implement in each new service.
- My advice is to write a set of shared libraries for each programming language you use.
- In any case, never ever mandate any library or framework. Each team should decide what to use for each service, without being obligated to use a company-wide approach.
- Enforcing consistency kills continuous improvement, because it increases the cost of choosing a different approach. Experiments become less appealing, and anything promising requires changing everybody's opinion and updating all code. Don't do this. Always assume you have two or more stable alternative approaches, and a few ongoing experiments. Every new initiative should involve an experiment.

## Service-level architecture

- Adopt a standard service-level architecture, to organize the code that makes up each service for ease of readability and testability.
- Organize your code so that what's used together stays and changes together. So "winter clothes" and "summer clothes" are good groupings, while "trousers" and "tops" are bad.
- My advice is to adopt the [Hexagonal Architecture](https://alistair.cockburn.us/hexagonal-architecture/), also called Ports and Adapters Architecture. It's a great way of structuring your code for effective changing and testing.

## ID generation

- You should choose the type of unique IDs you generate. Different types work best in different contexts.
- My advice is to use [Universally Unique Lexicographically Sortable Identifier](https://github.com/ulid/spec)s (ULIDs) or [K-Sortable Unique Identifier](https://github.com/segmentio/ksuid)s (KSUIDs) for domain IDs, and [Time-Sorted Unique Identifier](https://github.com/f4b6a3/tsid-creator)s (TSIDs) as primary keys in SQL databases. Here's [why TSIDs make great SQL database primary keys](https://vladmihalcea.com/uuid-database-primary-key/).
- You should also figure out whether to rely on sortable unique identifiers to infer the order of the events, in which case you should generate IDs from an event-processor, with partitioning, to ensure in-order processing.

## Resilience

- Circuit breakers and retries are important whenever you perform requests to downstream services.
- In an event-driven architecture, most services process messages from a queue, making both of these less important. For command and query endpoints, though, you still need them.
- For blocking IO operations, you'll want thread pools and bulkheads. An example might involve a separate thread pool and connection pool for each tenant, to interact with a SQL database. This way a tenant cannot easily influence other tenants with their activity.
- Each service should also expose a set of management endpoints, for health checks, etc. It's important that these are exposed on a separate port, rather than on the main application port, so that Kubernetes can access these without exposing them at all to other services or over public internet.
- Another good practice is a separate thread pool for the management endpoints, for otherwise high activity will make your application not responsive to management queries and commands.

## Data optimizations

- You should use compression for client-to-server, server-to-client, and service-to-service communications.
- Large attachments e.g., images and videos should be uploaded to object storage instead (e.g., [Google Cloud Storage](https://cloud.google.com/storage) or [AWS S3](https://aws.amazon.com/pm/serv-s3/)), and a pre-signed download URL should be sent instead, as a mechanism to obtain the attachment if needed.
- For images and videos, you also want to leverage CDNs, to dynamically adjust their size based on the screen dimensions of the user, and to choose their quality based on the user's internet connection speed.
- Whenever a user needs to upload an attachment (image, video, etc.), your back-end should generate a pre-signed upload URL to an object storage location, so that the traffic doesn't flow through your systems.
- You should adopt a quarantine bucket, so that every upload triggers a malware inspection process, which copies the file to the actual bucket if it deems the attachment secure.
- About PII, you should either encrypt the whole document with an end-user-specific key so, after the user has invoked the Right To Be Forgotten the documents will be unusable.
- Alternatively, you should store a template for the document and keep the data separate, so that after the user has opted out, you would still be able to produce a document, but with some of the information redacted.

## Dealing with money

- You should model money so that invalid amounts e.g., $15.732 cannot be represented.
- To avoid representation precision issues with decimals, you should model currency amounts using the fundamental units of a given currency. So instead of representing $7.52 dollars with a decimal, you should represent it with the number of dollar cents, 752.
- Tenants and users based in different countries might get billed in different currencies. Keep this in mind if you have this requirement, and think about currency conversion.

## Encryption

- Choose a battle-tested library for your encryption primitives. Never ever roll your own implementation of anything encryption related (unless you're an encryption company). [BouncyCastle](https://www.bouncycastle.org/) is a great choice.
- Figure out if you need compliance with the [Federal Information Processing Standards](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards) (FIPS). Unless your work closely with the US government, you should probably stick to non-FIPS implementations, as they are better supported and arguably more secure. Here's [an explanation of why Microsoft stopped recommending FIPS-compliant implementations](https://techcommunity.microsoft.com/t5/microsoft-security-baselines/why-we-re-not-recommending-fips-mode-anymore/ba-p/701037).
- Consider whether you would benefit more from runtime selection of algorithms and parameters, or from type-safe and abstracted encryption primitives. Personally I never found the first useful, and hate using BouncyCastle's API directly.
- Stick to well-known and battle-tested algorithms, like [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) for symmetric encryption, and [SHA](https://en.wikipedia.org/wiki/Secure_Hash_Algorithms) or [Argon2](https://en.wikipedia.org/wiki/Argon2) for hashing (SHA and Argon2 are best for different use cases).
- If your application relies on asymmetric encryption at application level e.g., a distributed ledger, you might want to consider post-Quantum algorithms like [Crystals Kyber](https://pq-crystals.org/kyber/) (as key encapsulation mechanism or KEM) and [Crystals Dilithium](https://pq-crystals.org/dilithium/) (as a digital signature scheme).

# Building and testing

## Packaging

- Each service should be packaged, as part of its build. You should choose between [OCI images](https://github.com/opencontainers/image-spec) e.g., [Docker](https://www.docker.com/), or native images e.g., [Graal](https://www.graalvm.org/).
- You should also tweak the runtime properties for your executable bundles. For JVM-based applications, this means chosen garbage collector, memory settings, GC flags, additional JVM options, etc.
- Structure your OCI images with [multi-stage builds](https://docs.docker.com/build/building/multi-stage/), so that each stage can be cached if it didn't change.
- Ensure you separate runtime requirements from build-time requirements, so unnecessary things don't end up in your image.
- Your [OCI images should be reproducible](https://medium.com/nttlabs/bit-for-bit-reproducible-builds-with-dockerfile-7cc2b9faed9f), meaning that the same code version should produce identical bytes. This requires some configuration tuning, but also for the contained artifacts e.g., JARs to also be reproducible. Here's [how to enable reproducible archives in Gradle](https://docs.gradle.org/current/userguide/working_with_files.html#sec:reproducible_archives).

## Builds

- Choose a smart build tool, so that only modules whose hash has changed get rebuilt and re-tested. This can save a ton of time from the duration of your builds. [Gradle](https://gradle.org/) does this well.
- Write scripts to build each service locally, without having to know the details of the build tool used by that service.
- Embed the build tool within the codebase of the service, rather than expecting for this to be installed on the machine running the build. An example is the [Gradle Wrapper](https://docs.gradle.org/current/userguide/gradle_wrapper.html).
- Your build pipeline should be the only criteria to decide whether your service is releasable. No human inspections should be needed. Manual regression testing is a crime. Manual exploratory testing is great, but not as part of the build and release pipeline.
- You should be able to build all your systems locally, relying only on localhost, and expecting nothing to be installed on the machine.
- As an example, if Java is not installed but is needed to build a service, the build script should install Java. An alternative approach to achieve this is to use a Docker container to run the build itself.
- Decide whether you prefer [GitHub Actions](https://github.com/features/actions), or a traditional build server e.g., [TeamCity](https://www.jetbrains.com/teamcity/). Build servers make it easy to rebuild dependent services, etc. and are generally much faster.
- If you prefer GitHub Actions, seriously consider running the agent on your own Kubernetes cluster, so that each build runs in its own throwaway Docker container on Kubernetes. It'll be much faster and cheaper.
- Ensure you upload build and test reports, and that you alert the development team of any failed builds, and of any build that was previously failing and just succeeded.
- Each service should specify its own build script, producing a Docker image, and uploading it to an image repository.
- Tag each image with the full hash of the code from version control, and pass this as an argument to the image, so that the service will be able to return its version from a management endpoint.
- On the remote build pipeline, sign each image with a key-pair, tag the image with the signature and the key ID, and verify the signature against the relevant public key before allowing Kubernetes to spin up those images. This prevents people from uploading imagines not produced by your build pipelines, whether unintentionally or maliciously.

## Functional tests as part of the build

- Each service should declare its input and output contract, using [OpenAPI](https://www.openapis.org/) specifications, Avro schemata, JSON schemata, etc.
- Test each service against its input and output contracts, to see whether it stays compatible with other services.
- Test each declared input and output contract for compliance with a set of company-wide rules. Examples include path style for OpenApi, or kebab-case instead of camelCase for Avro and JSON. This guarantees you get consistency of API standards, and is especially important for customer-facing contracts.
- Test each internal module against its code contract (the externally visible types and functions). Do this wrong, and your tests will be tied to the internal structure of your code, meaning they'll break when you change the structure, even if the behavior still works.
- Test each driving and driven adapter against the technology they integrate with. These integration tests should run using only localhost. Use a library like [Testcontainers](https://testcontainers.com/) to orchestrate Docker containers as part of your tests.
- After each driving and driven adapter is tested in isolation, and your business logic is covered by the contract tests for the application and domain modules, have one or two service tests. These start the whole service locally, and go from a driving adapter to a driven adapter, testing the correct configuration and wiring of the service.
- Run your service tests against your service running in-memory, and against the same service running as a Docker image. This way, you can identify issues with the packaging part.
- Use [mutation testing](https://pitest.org/) to check whether your tests are actually protecting you against undesired code changes. Aim for zero survived mutants. Don't bother with measuring test code coverage.
- Avoid any dependencies among tests, whether it's shared data or expected order of execution.
- The whole build, including all tests and checks should run in under 3 to 5 minutes, and you should be able to run all tests and checks locally. Having a smart build tool like Gradle helps with this.

## Checks as part of the build

- Perform static code quality checks.
- Automatically apply reformatting and linting.
- Inspect the code to prevent accidental leakage of secrets.
- Perform static code security analysis.
- Check dependency versions against known vulnerabilities.
- The whole build, including all tests and checks should run in under 3 minutes, and you should be able to run all tests and checks locally. Having a smart build tool like Gradle helps with this.

## Performance tests as part of the build

- For parts of your codebase where performance is critical, create micro-benchmarks e.g., with [JMH](https://github.com/openjdk/jmh) if you're using a JVM-based language.
- Establish a baseline, and run these as part of each build.
- For event-driven workflows, you can use flow analysis to determine the performance of the whole system from the performance of the parts. This is an extremely nice property. Given an event processor, you should test the throughput it can process, and the latency each event experience.
- The whole build, including all tests and checks should run in under 3 minutes, and you should be able to run all tests and checks locally. Having a smart build tool like Gradle helps with this.

## Smoke tests in production

- You should have a minimal set of smoke tests, running periodically in production.
- These should not duplicate the tests you run as part of each build, and you're not aiming for coverage here.
- The only purpose of smoke tests is to catch unexpected problems in your production environment. Misconfigured network rules, etc.
- Having one test for each main workflow works well, and these tests should exercise your whole system, in depth.
- An example of a smoke test might involve creating a test user for a test tenant, attempting to log in with the wrong password, resetting the password using a test email server, logging in successfully, logging out, and checking a login-protected page is now not available.
- If a smoke test fails, something is seriously wrong.
- You'll need test tenants, test users, test email servers.
- Normally you should use your actual third-party dependencies. Sometimes this is not possible, at which point you should use their test versions or some stubs, configured to only be used for these test users.
- These smoke tests should run in production and nowhere else, because the problems these tests catch are almost always environment-specific, so running them in another environment would be completely useless.
- Ideally these should run in ten to twenty minutes, and you should run them every thirty minutes or so.

## Resilience tests in production

- You should perform resilience tests in your production environment.
- Chaos testing tools are a good approach to achieve this.
- You should resist the temptation to run these in a separate environment, as they'd prove very little.

## Runtime monitoring in production

- Each event-driven workflow should produce an alert if a step doesn't complete within a time limit, or if the whole workflow exceeds a time limit.
- You should have a runtime security agent checking for abnormal behavior happening in production. [Wiz](https://go.wiz.io/) and [Aquasec](https://www.aquasec.com/) can help with this.

## Performance tests

- Exploratory performance tests should be run in ephemeral copies of your production environment.
- You should be careful with these, as the amount of data you have will likely influence your performance, so either makes the two environments identical or be careful about how you structure your tests.
- Examples of these tests include stress tests, soak tests, etc.

# Data and analytics

## Data lake

- Every application event should specify all the relevant and available information known at the time, without leaving anything out because it's not currently used by the downstream event processors.
- Never run OLAP queries on a database used by a service. Instead, an event sink can map the domain events published to a data lake for OLAP queries.
- Ensure you mask all sensitive data before inserting it into the data lake.

## Materialized aggregations

- Other event sinks can update some materialized view, for analytics that are aggregated as soon as the event that changed them is processed. An example would be the total number of users, updated as a count every time an event indicates that a new user has joined.

## Data operations and custom dashboards

- Use a set of connectors to produce events about various aspects.
- These should not include application events, as those are already produced.
- Anything of interest that happens off-platform should be produced. Financial reports, etc.
- Adopt tools that allow every employee to create their own custom dashboards and metrics. An example of these tools is Metabase.

# Backoffice

- You'll need a back-office web application for your employees.
- This should be built with the same care of your main web applications.
- Every operation should be event-driven, with full auditability.
- You might want to support different roles and admin reviews and approvals for some operations.
- This web application shouldn't be accessible from public internet, but only through VPN.

## Tenant management

- You'll need to list your tenants, and manage their configuration.
- You should be able to see which features and modules they have enabled, the weights and limits they have, and to change these settings.
- You need to be able to onboard a tenant from here, unless they can onboard from the app itself, in which case you need notifications.
- You should be able to review any applications, and either approve them or reject them for a specific reason. This should cause notifications for the tenant.

## User management

- You'll need to list and manage your users.
- You should be able to browse a user's activity.
- Sensitive information (including names, phone numbers, email addresses, transaction details, etc.) should be shown encrypted. The decision to decrypt should stay as a record for audit purposes.

## Issue management

- You'll need to list and manage your issues.
- You should be notified whenever a user submits an issue from the main app.
- The app should group issues by time, category, similarity, user, etc.
- From a list view, you should be able to focus on an issue, check the user, see the actions involved in the issue, find all events and logs related to the invocation ID, and make this available to some developers for further investigation.
- You should also be able to perform specific actions to compensate the user, or to fix their state. These should be normal commands, captured as events, showing up in the user's history, etc.
- When done, you should be capable of notifying the user that the issue is resolved, and to explain what the cause was. This needs to be reflected on the issue itself.
- Whenever things are more involved, you should be able to contact the user that's having the issue through the in-app chat.
- You should be able to template a resolution, and then apply it to a group of related issues.

## Product management

- You'll need to be able to manage your products from this app.
- TODO dashboards, features, modules, products, subscription tiers (with their limits, descriptions, etc.), in-app marketing messages, etc.
- Plan the release of a feature, with scheduling, marketing message, incremental rollout, etc.
- A/B test features, by enabling a toggle for a percentage of invocations for a target users sample (based on characteristics, etc.)
- Browse product activity, with trends, patterns, etc.
- Define and list dashboards and derived metrics.

## Infrastructure management

- You'll need to be able to manage your infrastructure from this app.
- List infrastructure deployments, along with which tenants they host.
- Show topics, event schemata, messaging queues, and services, in a topology.
- Visualize your information flows, in terms of which services produce and consume which topics, laid out like a graph.
- Visualize service information (by embedding or linking to your service registry).
- Propose a scripted database operation, opening a case for somebody to review and approve, so that the infrastructure can then pick it up, execute it, and give you the result back.
- Query logs and events, in an auditable and controlled way.