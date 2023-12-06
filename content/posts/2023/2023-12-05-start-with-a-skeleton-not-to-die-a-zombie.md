---
title: "Start with a skeleton not to die a zombie"
categories: [ "software-development" ]
tags: [ "system-thinking", "architecture", "effectiveness", "startups", "platform-engineering" ]
date: 2023-12-04T05:00:00
draft: true
---

TODO change this; start with "Some companies die a zombie. After 12-18 months, the cost of change skyrockets, so they cannot do anything, limping around mindlessly, until they bite the bullet and re-write their systems, or kick the bucket".

A walking skeleton is a basic set of code that acts as a “starter pack” for the development team. It's a lightweight application framework without any product-specific functionality, but that is still runnable and can exemplify the fundamental architectural patterns.

In a nutshell, you create a well-planned system that works, but that does nothing relevant, and then you add your product-specific behavior to it. Starting your software system from a walking skeleton offers several benefits:

1. As the various parts and aspects are inter-dependent, designing them together improves the quality of the overall system. Trying to add system-wide aspects later on is always much harder.
2. It yields a software system that works end-to-end, so you can iterate on it, and move from a complete system to a different complete system. This is much safer and faster, de-risking your progress.
3. You can put automated tests in place, to avoid new functionality breaking desired system-wide properties e.g., idempotency. 

What happens if a company doesn't do this? Well, the problem is that the company will still need to design and build the aspects a walking skeleton covers. This is much harder once you have customers using your products, and as you build new features. Also, you wouldn't get the chance to design the system end-to-end, meaning you likely won't achieve the same levels of effectiveness.

Most companies experience a steady increase in the cost of changing their systems, until things start becoming unfeasible 12 to 18 months in. At that point, the cost of addressing these issues is incredibly high, so it's often either rebuilding from scratch or slow death. Rolling rewrites work very rarely, because the new subsystems don't fit with the old ones. 

What's the best time to build a walking skeleton? It depends on the company. If the company is cash rich, perhaps a new venture within an established and profitable business, you'll want to do that early on, while you carry over market research. On the other hand, if you're bootstrapped, you won't have the runway to complete a walking skeleton before you start building your product, so prioritize your product initiatives in this case. After finding Product-Market Fit, take the time to rebuild your systems, from a walking skeleton. Don't skip this phase! It's tempting, but it often leads to ruin.

Let's have a look at the scope of a walking skeleton. All these aspects should be addressed in a way where they all work together. So it doesn't make sense to build one aspect and then move to the next one. Instead, build them in circles.

With a competent team of senior people, you can build a walking skeleton in 4 to 6 months, for most projects. Small-scale projects won't likely require this at all, or you can focus only on some aspects.

I'll try to group these aspects by category, but they'll all inter-dependent. So you should read through, understand how things could work together, and then decide whether you'd like the overall system. I'll sometimes advise for things: feel free to ignore it, but changing one aspect will likely change how the overall system behaves, and what's achievable.

# Tenant and access management

## Authentication

- You'll likely need a Single-Sign On option, and Identity Provider federation if in B2B.
- For the non-SSO option, you'll need MFA, email verification, password storage (Argon2 hashing or similar, salting, peppering, etc.), and password reset.
- You need to know when a user logs in the first time, when they log out, etc.
- You should decide whether to accept email aliases e.g., somebody+something@gmail.com.
- You should pick between delegated or mapped identity for IDP federation cases. With delegated identity, the external IDP tells your IDP the identity of the user, and you take it at face value. With mapped identity, you map the identity in the external IDP in your own IDP. My advice here is to always map. In any case, you should ensure that when an identity is removed from an external IDP, it also gets removed from your IDP.
- You'll also want to support Personal Access Tokens (for user accounts) and API keys (for service accounts), because orchestrated authentication workflows don't work well with scripting. 
- You'll almost always want to either host an open-source solution like Keycloak, or to go with a managed service like Okta.

## Token management

- You'll need to issue, rotate, and verify tokens, as part of your authentication workflow.
- Certificate management (below) is a prerequisite for this. You could choose to have a single certificate (with rotation), or different certificates across different tenants (if B2B, based on subdomains) or geographies.
- You should include a unique client-side session ID in your tokens, along with the token's validity start and end timestamps.
- The authorization roles and containing scopes (below) should also be included in the token.
- The duration of a token should be a maximum of 30m to 1 hour.
- You also need to choose an algorithm, ideally EdDSA, rather than RSA or ECDSA, as it's faster, requires shorter keys, and it's considered more secure.
- In terms of token structure, JWTs are a safe bet.

## Tenant isolation

- This is mostly a B2B concern.
- Tenants should be isolated from each other in terms of workflows.
- The data for a tenant should be stored and encrypted separately from the data of other tenants.
- Each tenant should be able to set up SSO with their own IDP, and to enable IP address range restrictions if they want.
- To separate the entry-points (required for the above), you should consider creating a subdomain per tenant e.g., <tenant-name>.<your-root-domain>.com. This needs to happen automatically when you onboard a new tenant.
- If you offer environments, you'll likely need infrastructure isolation to prevent activity from a tenant to affect another tenant's workflows.
- You'll need to implement at least two tenants for each tenant type, as part of your walking skeleton.

## Authorization

- You need a way to model rules about authorization.
- You also need a way to query this, both on the front-end (to hide or gray out things the user cannot perform) and on the back-end (to enforce authorization rules).
- Authorization should be checked and enforced once per invocation. If the grants for a user change, in-flight invocations should complete with the grants they had at the beginning of their processing.
- My advice is to model resources (the things your product allows to interact with), actions (what you can do with a resource), and container scopes (nestable groupings of resources).
- I also advise defining policies as sets of action-resource permissions, and creating roles that are associated with bundles of policies. A user then has multiple roles, each associated with a containing scope (think about these as projects, spaces, or folders). So when a user is in a given context, it has certain roles active in that context, and inherits some permissions through the policies associated with those roles, as a result.
- On the front-end, you should retrieve the roles and the containing scopes from the user's token, then look up the policies and permissions granted by those roles, from a dedicated endpoint.
- I recommend using a standard way of defining and querying authorization permissions and policies, with Open Policy Agent (OPA) being an excellent choice.

## Tenancy model

- This is mostly a B2B concern.
- Your users will belong to different tenants. Also, a tenant will likely be too big to map to a single namespace.
- You should allow your tenants to define more granular groups of users.
- You could choose to model these groups as projects, spaces, teams, or organizations.
- My advice is to avoid choosing one model, and allow arbitrarily nestable containers, like folders. This way, a tenant can model their own organizational structures within your product, and put users and resources within these.
- It's important that belonging to a container cascade down their hierarchy. So if a tenant creates a Global folder, US and EU folders underneath it, and a France folder underneath EU, anything within France will also need to be within the EU and the Global folders. 
- These nestable containers will be used as containing scopes for authorization (see above). So if a user has the Project-Accessor role within the France scope, they'll see projects in France, but a different user with the same role in a different scope won't.
- These groupings will also be useful with billing insights, so that billing contributions can be tagged with the containing scope they were produced in, allowing to roll them up hierarchically, according to the tenant's own organizational structure.
- You'll need to model at least two branches of the organizational hierarchy for each tenant, and do that for at least two tenants, as part of your walking skeleton. 

# High-level architecture

## Main architectural patterns

- You'll need to choose whether to use orchestration (the logic is centralized in a controller, which dispatches calls to other services) or choreography (the logic is distributed, with each service reacting to what other services are doing).
- The choice between orchestration and choreography is for each workflow and subsystem. My advice is to adopt service choreography for every workflow and subsystem.
- You'll also need to decide whether to record the current state, or whether to store the history of state changes, use it as your source of truth, and derive the current state from this history.
- This is also theoretically a local choice, so that each subsystem could choose a different approach. My advice is to record the history of state changes and use that as your source of truth, for all the subsystems.
- An architecture that globally uses service choreography and records the history of state changes is called an event-driven architecture.
- At this point, I also recommend Command and Query Responsibility Segregation (CQRS). This means that commands (invocations that mutate the state without retrieving it) are processed by subsystems that are separate from the ones that process queries (invocations that retrieve the state without mutating it).

## Realization

- Event-driven architectures work well with a partitioned distributed ledger, like Apache Pulsar (or Apache Kafka), as message broker and the backbone of event propagation.
- You should consider whether storing the events indefinitely within Apache Pulsar (with tier storage backed by object storage, like S3 and Glacier), or whether using Apache Pulsar for propagation and a having a separate storage for events.
- My advice is to consider having a separate storage for events, like EventStore or even Postgres.
- You'll need a mechanism to handle PII with regard to GDPR's Right To Be Forgotten. Storing PII as part of the events with field-level encryption using per-end-user symmetric keys is a good approach, so when the user needs to be forgotten, you can unlink the key, without losing data integrity.
- Your servers will have to push information to your clients. You should consider whether hosting a solution, like an MQTT broker, or going for a commercial solution, like Ably. The main factor here is cost: if you foresee a lot of server-pushed messages, hosting your own MQTT cluster is the clear winner.
- My advice is to avoid websockets, as they introduce connection stickiness (you need to know which socket to use to send a message to a user), and they're too low level.
- In terms of API style, you'll have to pick one and stick to it for your whole API surface. Examples of API styles include REST, GraphQL, and RPC.
- My advice is to adopt an RPC style. GraphQL and REST both operate at data manipulation level, but what you want is domain-specific actions.
- So use the POST HTTP method, with the type of the invocation as part of the path, and choose whether to differentiate commands and queries. Examples include `POST /commands/tranfer-account-ownership`, `POST /queries/retrieve-available-balance`, and `POST /invocations/tranfer-account-ownership`.
- You can easily specify caching instructions for POST responses, but my advice is to try and avoid caching responses as much as possible, subscribing to changes instead.
- This approach allows bulk invocations endpoints e.g. `POST /commands`, `POST /queries` and `POST /invocations`, so a client can send multiple invocations in one exchange with the server.
- This approach also allows to record all invocations, whether commands or queries, to provide full auditability.
- Whenever you need to enforce data-level domain rules, you'll have to choose between the outbox pattern (write to a DB, then derive publishing an event), or the saga patter (read from an eventually consistent view, decide in memory, publish an event, eventually update the view, on conflict rollback the changes and refund, etc.). My advice here is to use sagas, as the outbox pattern is tricky and constitutes a severe limitation in throughput.
- As your system is fully asynchronous, message-based, and reactive, you can implement the async request-reply pattern to respond to queries synchronously.
- My advice is to use NATS for this. You generate a unique response NATS topic, subscribe to it, emit an event tagged with the response topic, await for a downstream service to publish the outcome of your workflow to NATS, and finally respond to the open socket.
- About the messaging broker, Apache Pulsar and Apache Kafka are both good choices. I find Apache Pulsar superior overall, but Apache Kafka still has a larger community and more ready-made integrations. In any case, I recommend hosting these yourself, rather than using a managed service, for cost reasons. Apache Pulsar is way easier than Kafka to host, so yet another reason to prefer it.
- Choose whether to leverage an API gateway, or to go without one. My advice would be to use one, so you can centralize token signature verification, authorization enforcement, parsing tracing information (below), CORS handling, and other similar operations. I also recommend hosting an open-source or a commercial solution, rather than buying a service.
- You'll want to create templates for the various types of services that appear in your topology. Command endpoints (receive and emit commands), query endpoints (serve queries), event processors (receive and emit events), event sinks (receive and consume events, typically integrating with third-party technologies).

# Correlation

## Invocation context

- Every invocation should be contextualised with information about the invocation itself.
- This context should be part of your software models, not something implicit and accessed outside the normal call stack. You should be able to base your behavior on this information, to log it, and to make it part of the events you publish.
- The context should contain information about the access, the trace, and the toggles associated with the invocation.
- The toggles associated to an invocation should be a set of key-value pairs, where the key is a feature toggle ID, and the value is the type-safe value for that feature. This can be used for A/B testing, to bump the logging level for an invocation, and for many other use cases. Mind that these toggles are per-invocation, so they shouldn't contain things like product tiers, etc.
- The access should include authorization information, provenance information (client IP address, parsed user agent, etc.). It should also indicate whether the invocation was unauthenticated (for operations exposed outside of login) or authenticated. For authenticated accesses, information about the actor should also be included. This should indicate the account ID, whether it's a user or a service account, the tenant the actor belongs to, the locale of the user, and the authentication mechanism (including client-side session ID or the hash of the API key used). Last, the actor should support impersonation and acting on behalf of other accounts.
- The trace should allow to correlate invocations that are logically related. A good way of achieving this is to generate some initial unique IDs (e.g., ULIDs) on the client side: 1 for the action itself e.g., a button press, plus 1 for each invocation to the back-end this action maps to (typically one). After that, the gateway should generate an originating trace ID, so that these 3 pieces of information stay immutable throughout the chain of invocations. Last, each service that processes the invocation should receive a parent invocation ID, generate an invocation ID, and send this last ID as parent invocation ID for downstream calls.
- This way humans and systems can easily identify retries and logically duplicate invocations.
- Overall, the information in the invocation context allows to determine an idempotency key: this one is typically the external invocation ID, within a namespace composed of the tenant ID and the actor ID (so that different actors and tenants cannot interfere with each other in terms of idempotency).
- An application should receive the full invocation context from the gateway (typically encoded as JSON and to Base64 in a header), fork it (generate a unique invocation ID, and move the received invocation ID as new parent invocation ID), add it to the log stack, pass it as an argument (or context argument) to all functions, include this information in every event, and send this as a header as part of any downstream HTTP request.
- Every event and message should also have their own context information, which is the ID of the originating and the parent events and messages. So each event has an event context, which includes the invocation context, and event correlation information. Each message (the event might be in the payload), will also contain message correlation information.

## Idempotency

- The invocation context (above) can give you an idempotency ID.
- You can use this ID to ensure that logically duplicated calls do not cause duplicated side effects, including state changes and calls to external systems.
- For SQL databases, you can use a transaction that tries to insert this ID into a dedicated table of previously seen invocations, with a unique constraint. As part of this transaction, you can do whatever that invocation would need to do in the database. If it fails because of the idempotency constraint, you can consider it successful, and proceed with anything else you need to do.
- For external APIs, some will allow you to specify an external invocation ID for idempotency purposes. In this case, you simply pass that value, and the system will take care of staying idempotent to duplicated changes with the same ID. This should work the same for your API, since your clients can choose to repeat the external invocation ID, if they want to retry an invocation in a safe way.
- Some external APIs, like emails, won't allow you to specify an idempotency ID. In this case, you can use a SQL database to filter out duplicates, as per above except for skipping the call to the external system in case of a uniqueness constraint failure with the idempotency ID. 

# User-facing applications

## Internationalization

- All strings should be represented using the UTF-16 or UTF-8 charsets. UTF-8 can represent every character, but it's optimized for text that is mostly ASCII. So it depends on the intensity of this requirement. In any case, stick to UTF-8 at a minimum, even if you don't currently have any internationalization requirements.
- The client should externalize all text content, so that a different value can be used based on the browser's locale. When the locale changes in the browser, this should also be changed.
- The back-end should return these internationalization keys, rather than text in English, for everything.
- The actual values should be packaged in the app itself, with a fallback to a lookup against a CDN. This allows to trade-off chattiness with app size, and to override a value without having to wait for a release.
- All communications e.g., emails and in-app notifications should respect the locale of the user, falling back to a default locale, if the user's locale is not currently supported.
- If you plan to support Arab countries, or Asian countries like China and Japan, you should also change the page layout based on the user locale, as the languages involved are laid out differently. 

## In-app notifications of changes

- You should represent new features, marketing communications, etc., notify in-app and through email about them, and expose a browsable changelog for all historical changes to your products.
- This changelog should be an append-only log of changes, so that a user can browse and filter them. Each item should take the user to a page with more details on that change.

## In-app audit log

- Users should be able to browse, filter, and inspect a changelog with all the actions they ever performed.
- If a user has the specific permission, they should be able to also see in the changelog the actions performed by other users.
- Each item in the audit log should contain the full invocation context (above) for the invocation represented by that item, with dates, etc.

## Displaying and reporting errors

- You should display meaningful error messages when something goes wrong, in the user's locale (with fallback, if not supported). These shouldn't be protocol level error messages (e.g., 403 Forbidden), but properly crafted messages, explaining what went wrong, and what the user should do about it.
- Some types of errors should offer the user the option to retry (using the same invocation ID for idempotency).
- All unexpected errors should allow the user to report the error, and ask them to choose a recent invocation the error relates to. This should create an entry within an in-app open error investigations section, and retry the invocation with bumped up logging level (using a toggle) and same invocation ID (for idempotency). This should alert your back-office (below). Once the error is fixed, a back-office user can provide information about what happened and what was done about it, and the open investigation should be updated, with the user receiving an in-app/email notification.

## Accessibility

- If you have any accessibility requirements, and probably even if you don't, you should ensure your client applications are accessible.
- You should create automated tests against regressions (e.g., using Wave, Axe, and Pa11y, https://opensource.com/article/23/2/automated-accessibility-testing), so that what's accessible doesn't lose this property at some point in the future.

## In-app and off-app learning

- You'll need to guide your users through learning how to use your product.
- This can be a mix of in-app resources e.g., a guided walkthrough and the product's documentation, and off-app resources e.g., videos on YouTube.
- In any case, you should list these resources in-app, and guide the users through their journey.

## History of changes for each entity

- Your product will expose specific entities to users, allowing them to manipulate them.
- You should ensure that users can browse and search the history of all changes that happened on any one of such entities.
- An example might be that, if your product allows users to create projects, any user with permissions should be able to see the whole history of changes on a specific project: who created it and when, the original data, the log of changes, each including who did what, when, and how.

## Multi-platform strategy

- If you ever need both mobile and web, you'll need to decide whether leveraging a multi-platform approach (like React/React Native, Kotlin multi-platform, etc.), or whether to adopt separate codebases for each channel.
- In B2B, it almost always makes sense to go with a multi-platform approach.
- In B2C, your users will tend to be mobile first, so going native might sometimes be preferable.
- However, this is not a rule, so make an explicit decision, keeping in mind the number of specialists you have available, etc.

## Components

- You'll want to curate a set of client components, to achieve a consistent user experience and look&feel, throughout your applications.
- You should be able to compose these into higher-order components.
- You should be able to test each component in isolation.
- These should be versioned and maintained as a library.

## Modules, features, and billing

- Your products will contain various modules and features.
- You'll need to model these explicitly, so that a new module can be released in the back-end, without having to re-release the front-ends.
- You should be able to bill based on a combination of a base tier, plus a consumption-based contribution. In any case, what you charge should be auditable.
- Whenever a tenant would have exceeded their maximum quota of operations, you should be able to automatically disable further actions from that tenant, until they expand their subscription or the new cycle starts.

## Instrumentation and attribution

- You should instrument your products, so that you can know what your users are clicking, doing, etc.
- These events should be captured within the client applications, and sent to the server or to an external service.
- Instrumentation should include both low-level actions (clicks, text typed, etc.) and high-level intentions (logged in, created a project, changed the permissions of another user, viewed the list of projects, etc.).
- You should also be able to attribute events to user-specific toggles, to gauge the impact your tweaks have on the KPIs you hope to affect.
- It's pretty much always better to use an external tool to do instrumentation and attribution. Examples could be Amplitude for both, or Amplitude/Pendo/others for instrumentation and Split for attribution.

## Requirements and entitlements

- Some features, modules, or products will come with additional requirements.
- Even just accessing your platform will likely have some base requirements e.g., a valid email address.
- You should model what requirements each feature, module, product, or platform needs, before a user can access it.
- Each requirement could be satisfied by different alternative entitlements.
- An example might be that a "valid email address" could be satisfied by a passed email verification check, or by receiving a corporate email address from a federated identity provider.
- You should model which entitlements satisfy a requirement. This can vary based on the country, etc.
- Users should be associated with the set of entitlements they already gained, so that a product with requirements already satisfied by the entitlements the user has shouldn't ask the user to do anything else.
- You should be capable of disabling functionality the user hasn't qualified to use yet, of explaining which requirements aren't met yet, of showing the available ways of qualifying for each requirement, of running the verification step for the entitlement chosen by the user, and finally of unlocking the feature when all the requirements are met.
- Requirements and entitlements should be dynamic, sent by the server to the client as data. Your client applications shouldn't know which requirements a product or feature needs as part of their code.
- This works very well with components. So a requirement might be "having signed the terms and conditions with ID 123", an entitlement might be "digitally signed a document showing the terms and conditions with ID 123", and you could have a component for this entitlement, so that any time a product or feature needs T&Cs signed, you can re-use the component as part of that workflow.

## SDKs

- You should abstract all communications to and from the back-end with client-side SDKs.
- Each SDK should be built, tested, versioned, and released as a stand-alone library.
- Each SDK should have an API or contract module, and various implementations e.g., HTTP-based + MQTT for server-pushed communications, or an in-memory implementation for local testing.
- You should test your client applications against an in-memory version of the SDK, not against an environment hosting your back-end.
- You should use reactive-streams e.g., RxJS or MobX to allow the client to subscribe to server-pushed data.
- You should use the SDK to write tests that don't test the UI e.g., smoke tests you can run periodically in production (more on this below).
- You might want to give your client-facing SDKs to your customers.

# Infrastructure

## Only one long-lived environment

- You should only have one long-lived environment: production. So no test, UAT, or staging environments.
- Learn how to test locally (more on this below), and leverage internal tenants to test and demo your changes before releasing them to external tenants.
- Use ephemeral short-lived environments to perform intense tests e.g., stress performance tests, or to test large infrastructure changes. These should be exact copies of the production environment, with masked sensitive tenant data, and you should spin them up and down programmatically. 

## Infrastructure as code

- You should describe your entire infrastructure and tenant configuration in a declarative way, as code.
- Changes in the code should trigger changes in your infrastructure.
- You can use various approaches for this, including Pulumi and Terraform.
- You should monitor your infrastructure, checking for divergences between the declared state and the actual one.
- A configuration drift management tool can help you spot these inconsistency, raise alerts, and even roll-back any undeclared changes.
- In terms of provisioning, a fully scripted approach will work well, except when infrastructure needs to be provisioned as part of some users' actions. In this case, you'll need dynamic provisioning, and Terraform can leave you with an inconsistent state in case of failure. So Kubernetes Operators are a better approach for this. 

## Configuration management

- Your applications will need variables, private keys, certificates, passwords, etc.
- These might depend on the specific tenant the invocation belongs to (so 2 different tenants might use separate databases, each with their own credentials).
- Whenever you can, avoid injecting these variables into your applications at all. Instead, use side-cars that proxy the connections or do the work requiring the secrets.
- When not feasible, use a standard way of injecting configuration, like Kubernetes ConfigMaps, or file-based configuration (exposed to the apps through ephemeral volumes).
- In terms of storing the secrets, you'll want something audited, segregated, and secure, like Hashicorp Vault.
- You should ensure that whenever a configuration value changes, your applications can pick up the change. I recommend rebooting the containers in this case, as it's usually not a big deal.
- All credentials should be service-specific, never shared among applications.

## Certificate management

- Your products will use certificates, and those certificates will need rotation, etc.
- In multi-tenant contexts, each tenant will likely end up with its own subdomain and its own certificates.
- Figure out how you're going to achieve this programmatically.

## Internet Edge Solution

- An internet edge solution, like Fastly or CloudFlare is almost always a great idea.
- You get protection from DDoS attacks, and against other malicious attempts.
- Also, you could allow your tenants to enable mTLS and IP address range restrictions programmatically, by calling the internet edge solution's API as part of handling such a command.
- My recommendation falls on Fastly, as it's usually easier to integrate with, compared to CloudFlare.

## Cloud providers

- You'll need to decide whether single Cloud provider availability and business continuity is enough.
- If so, then my advice is to stick with Google Cloud Platform (GCP). It's cheaper than the others, and offers great fundamental products e.g., the managed Kubernetes service.
- If you need a multi-Cloud approach, you'll need to figure out whether active-passive-cold is enough, or whether you need active-passive-hot or active-active.
- In any case, the way this should work is that, when your active Cloud provider has an issue, you should be able to switch to another Cloud provider with 1 click.
- You should aim at not losing any data as part of this. Ideally this should also happen with zero downtime.
- Active-active and active-passive-hot multi-Cloud workflows are hard, but can be achieved in a similar way multi-region workflows work.
- You could deploy a messaging cluster on each Cloud provider, and then replicate each command across all clusters, ensuring each replicated command ends up having the same offset across different clusters. Apache Pulsar can help with this, with its geo-replication features. Once you have this, you can enable/disable the side effects in your passive Cloud provider, but it'll be ready and eventually consistent with the active one.
- Even if you simply need to be deployable in more than 1 Cloud provider, but downtime is okay, you should still test with at least 3 Cloud providers, as part of your walking skeleton. This is because you usually need quorum to recover from a temporary failure, so the minimum Cloud providers you'll need is 3, when 1 is not enough.

## Regions and Availability Zones

- Depending on your availability and disaster recovery requirements, you'll need your services across multiple Availability Zones, or even across multiple Regions.
- Active-active and active-passive-hot multi-region workflows are hard, just like it's hard to get these working well across multiple Cloud providers.
- The difference is that the Cloud providers introduce more management complexity, while the regions introduce higher latency involved with your replication.
- If you have multi-region requirements, you should test in at least 3 regions, as part of your walking skeleton. This is because you usually need quorum to recover from a temporary failure, so the minimum regions you'll need is 3, when 1 is not enough.

## Server-push data

- Your back-end will need to sometimes push data to your client applications.
- A hosted or managed MQTT cluster is a great way of achieving this.
- A user shouldn't be able to subscribe to information they shouldn't see (e.g., belonging to other tenants or users), so you'll need authentication and authorization.
- You'll need to structure your topics carefully, balancing authorization needs and the effort involved in pushing an update. So a topic per user makes authorization trivial, but pushing updates a nightmare. A single topic is the opposite. You'll need a balance.

## Service registry

- You should have a service registry, listing all existing services.
- Each service should show which infrastructure resources they depend on, along with the libraries and versions they use.
- You should be able to see all services that use a dependency version affected by a vulnerability.
- Every service should also link to its codebase on version control.
- Each service should have an identity in the form of a unique identifier e.g., a ULID.

## Messaging

- Your messaging infrastructure will need authorization, auto-scaling, replication, partitioning, etc.
- You should have a service registry in place, and a way of authenticating services. mTLS is a good way of doing this, if you issue per-service certificates, with rotation, using sidecars to proxy the communications.
- In terms of authorization, ACLs work well, but a custom authorizer using OPA is better. Both Pulsar and Kafka support this. The way it works is that you can declare a custom authorizer as a plugin extension, and your broker will ask it whether a service is allowed to publish or subscribe to a topic, caching the result afterwards.
- Partitioning and cluster auto-scaling are much easier with Pulsar than they are with Kafka.
- You should also have a company-wide registry of topics and schemata (typically in Apache Avro). So that each developer should know what topics exist, what are they for, and their schemata.
- Your cluster should be configured to reject messages whose payload is backward or forward incompatible with the schema set for the topic.

## Service-to-service communications

- Ideally no two services should ever know of each other's existence, exclusively publishing and receiving events instead.
- If you must have peer-to-peer communications, service mesh will help manage this.
- By using peer-to-peer communications you lose a lot, in terms of backpressure, security, extensibility, etc. so think really carefully whether you really have to.

## Autoscaling for services

- You'll want CPU-based auto-scaling groups, for command and query endpoints, as their driven by unpredictable external traffic.
- For event processors and event sinks, CPU-based autoscaling makes no sense, as these process messages out of a queue. Instead, you'll want to scale their consumer groups based on the derivative of their queue size: if they're falling behind the producers, ramp up, and if they're catching up fast, ramp down. 

## Monitoring

- You should have dashboards and alerts for both product and infrastructure related aspects.
- In terms of infrastructure, things like CPU, memory, number of inbound and outbound connections, error rate, available disk space, etc.
- About product aspects, stuck workflows that are not progressing through the steps after a given time (using sagas for this), brute-force login attempts, suspicious patterns, etc.
- You should also have health checks and readiness checks for each service, along with an externally generated availability check service e.g., Pingdom, to check whether your platform is available to the outside world.
- Any error-level log entry should trigger an alert to be investigated.

## Data segregation and replication

- Different tenants might require different encryption keys, physically segregated storage, and different locations for their data.
- Data residency regulations require that data for customers in a Country is also going to be kept in that country (some Countries require "only" instead of "also", but only 1 or 2).

## Releases and deployments

- You'll need automatic canary deployments, gradually incrementing the amount of traffic directed to the upcoming version, based on comparing the error rate with the one measured for the old version.
- Each invocation that failed on the new version should be retried on the old version, to ensure there's no downtime (remember: you should have idempotency throughout).
- A failed release (error rate increased beyond the acceptable) should be rolled back automatically, with alerts, so the development team can investigate.
- For back-end applications, you'll likely want a continuous deployment model, where each change merged is released to production and enters into effect immediately.
- For web and mobile applications, you'll want a similar deployment model, but the changes should be deployed with feature flags that make them inactive, to be activated at a later stage based on marketing campaigns, etc. For mobile, you should batch your changes, so that a new version is published to the app store only once a week or so.
- Data migrations should be performed as part of the release, by pre-init containers. You should be able to specify migrations that run before the new instances come up, during the release, and after all the old instances have been brought down.

## Logs

- Each service should be able to log as a plain sentence, or in JSON, based on a configuration variable passed at runtime. The default should be JSON, overridden locally to be plain instead.
- The log entry should have a company-wide specific JSON schema. Services should be tested to check whether the log lines they produce comply with this schema, as part of the build pipelines.
- The invocation context should also have its own schema, included as an optional field in the log entry schema.
- Logging long strings is incredibly slow in general, so the default minimum log level should be kept to DEBUG, and INFO should never be used as part of normal workflows.
- An invocation should be able to specify a toggle to bump the produced logged level from DEBUG to INFO.
- Does this mean that most workflows won't produce any logs? No, because an event sink can map each produced event into a log line, asynchronously, without slowing down the processing itself.
- So why do we need to occasionally bump the log level to INFO? Or why log directly from the apps completely? Because sometimes weird things happen, and an application ends up not being able to publish the event, or you might be interested in how the inside of an app is working.
- The events are already recorded forever, so no point in mapping them as logs that are also kept forever. You can keep the direct application logs for a while (1 month, or something similar), and merge these on demand with the event logs, when an employee wants to search for something.
- Imagine you're having a live incident, you can ask your logging system to give you all the logs for a given invocation ID. Your system will merge the direct logs from the application containing that ID, and re-consume all events with that invocation ID, to produce a search space for you.
- If you create wrapping types for PII and secrets, you can easily avoid these being leaked in the direct application logs, and you can mask them when putting them in the search space. 

## Application development

- Event-driven optimizations (single threaded processing, in-memory processing with crash recovery from eventually consistent snapshots + replaying, batched processing for sinks)

## Frameworks and libraries

- You'll need to figure out how to do a range of table stakes, including configuration parsing, etc.
- You don't want to implement these low-level concerns yourself.
- You TODO

- Test strategy (contract, integration, service tests, smoke tests)
- Test tenants, test users, test email server
- Build reports and alerts
- Security build scanning (secret leakage prevention, etc.)
- Local testing
- Local scripts (1 command to do an operation e.g., build and test, so that you don't need to know the right commands)
- Automatic linting and static code analysis
- Ephemeral environments (to test large-scale infrastructure changes, or for performance-intensive changes)
- Performance tests (stress tests, soak tests, flow-based tests for event-driven workflows, etc.) and resilience tests (chaos testing)
- Checks for the data format standards (camelCase vs snake_case vs kebab-case in JSON and Avro)
- API style rules, and compliance checks (params, typos, etc.)
- Auto-update of dependency versions (scheduled, with testing, etc.)
- Code storage (monorepo vs multiple repositories, for what)
- Build pipelines (GitOps e.g., GitHub actions vs build server e.g., TeamCity or Concourse, which handle cascading builds well, signing builds, knowing which version is in production)
- Build tool (Gradle, vs Maven, vs others)
- Packaging (OCI images vs native images e.g., Graal or kotlin native, image repositories)
- Front-end modularity (components, micro-frontends)
- Back-end modularity

- Circuit breakers and bulk-heads (if needed)
- Thread pools (connections to databases, etc.)
- Idempotency (throughout, with 3rd-party providers, etc.)
- Shared libraries (yes vs no, versioning, monorepo vs separate libraries, what for)
- Currency (how to model, what to do, based on fundamental units)
- ID generation (ULIDs, TSIDs, partitioned, etc.)
- Encryption (symmetric AES and SHA-256/SHA-512 for hashing, BouncyCastle, runtime algorithm choice vs static, FIPS vs non-FIPS, post-quantum e.g., Dilithium and Kyber)
- Client-side SDK (yes vs no, domain-driven style vs service style, test extensions, whether to give it to customers)
- Runtime optimizations (garbage collector and options, memory, etc.)
- Data tweaks (compression, dynamic resizing of images, CDNs)
- Object storage (pre-signed upload and download links, quarantine buckets, hash-based duplication checks if the size matches, PII handling with either tagging and deleting or template + encrypted data, etc.)

- Back-office (tenant management, enabling features and modules, event-driven)
- Service registry (e.g., Backstage, services with dependencies, so you can go from a vulnerability in a library to all the services affected by it)
- Integration events (company-wide schemata and registry of topics)
- Querying logs and events manually (authorization, auditability, etc.)
- Data format standards (camelCase vs snake_case vs kebab-case in JSON and Avro)
- Data engineering (OLAP database, pipeline, custom dashboards, etc.)
- Manual database operations (manual database operations repository, PRs, merged scripts get executed by the infrastructure, and the result is returned)

TODOs
- Find an image if you can