---
title: "Start with a skeleton not to die a zombie"
categories: [ "software-development" ]
tags: [ "system-thinking", "architecture", "effectiveness", "startups", "platform-engineering" ]
date: 2023-12-04T05:00:00
draft: true
---

A walking skeleton is a basic set of code that acts as a “starter pack” for the development team. It's a lightweight application framework without any product-specific functionality, but that is still runnable and can exemplify the fundamental architectural patterns.

In a nutshell, you create a well-planned system that works, but that does nothing relevant, and then you add your product-specific behavior to it. Starting your software system from a walking skeleton offers several benefits:

1. As the various parts and aspects are inter-dependent, designing them together improves the quality of the overall system. Trying to add system-wide aspects later on is always much harder.
2. It yields a software system that works end-to-end, so you can iterate on it, and move from a complete system to a different complete system. This is much safer and faster, de-risking your progress.
3. You can put automated tests in place, to avoid new functionality breaking desired system-wide properties e.g., idempotency. 

What happens if a company doesn't do this? Well, the problem is that the company will still need to design and build the aspects a walking skeleton covers. This is much harder once you have customers using your products, and as you build new features. Also, you wouldn't get the chance to design the system end-to-end, meaning you likely won't achieve the same levels of effectiveness.

Most companies experience a steady increase in the cost of changing their systems, until things start becoming unfeasible 12 to 18 months in. At that point, the cost of addressing these issues is incredibly high, so it's often either rebuilding from scratch or slow death. Rolling rewrites work very rarely, because the new subsystems don't fit with the old ones. 

What's the best time to build a walking skeleton? It depends on the company. If the company is cash rich, perhaps a new venture within an established and profitable business, you'll want to do that early on, while you carry over market research. On the other hand, if you're bootstrapped, you won't have the runway to complete a walking skeleton before you start building your product, so prioritize your product initiatives in this case. After finding Product-Market Fit, take the time to rebuild your systems, from a walking skeleton. Don't skip this phase! It's tempting, but it often leads to ruin.

# Scope of a walking skeleton

Let's have a look at the scope of a walking skeleton. All these aspects should be addressed in a way where they all work together. So it doesn't make sense to build one aspect and then move to the next one. Instead, build them in circles.

With a competent team of senior people, you can build a walking skeleton in 4 to 6 months, for most projects. Small-scale projects won't likely require this at all, or you can focus only on some aspects. 

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

## Architecture

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
- As your system is fully asynchronous, message-based, and reactive, you can implement the async request-reply pattern to respond to queries synchronously.
- My advice is to use NATS for this. You generate a unique response NATS topic, subscribe to it, emit an event tagged with the response topic, await for a downstream service to publish the outcome of your workflow to NATS, and finally respond to the open socket.
- About the messaging broker, Apache Pulsar and Apache Kafka are both good choices. I find Apache Pulsar superior overall, but Apache Kafka still has a larger community and more ready-made integrations. In any case, I recommend hosting these yourself, rather than using a managed service, for cost reasons. Apache Pulsar is way easier than Kafka to host, so yet another reason to prefer it.
- Choose whether to leverage an API gateway, or to go without one.
- My advice would be to use one, so you can centralize token signature verification, authorization enforcement, parsing tracing information (below), CORS handling, and other similar operations.
- I also recommend hosting an open-source or a commercial solution, rather than buying a service.
- You'll want to create templates for the various types of services that appear in your topology. Command endpoints (receive and emit commands), query endpoints (serve queries), event processors (receive and emit events), event sinks (receive and consume events, typically integrating with third-party technologies).

## Invocation context

- Every invocation should be contextualised with information about the invocation itself.
- This context should be part of your software models, not something implicit and accessed outside the normal call stack. You should be able to base your behavior on this information, to log it, and to make it part of the events you publish.
- The context should contain information about the access, the trace, and the toggles associated with the invocation.
- The toggles associated to an invocation should be a set of key-value pairs, where the key is a feature toggle ID, and the value is the type-safe value for that feature. This can be used for A/B testing, to bump the logging level for an invocation, and for many other use cases. Mind that these toggles are per-invocation, so they shouldn't contain things like product tiers, etc.
- The access should include authorization information, provenance information (client IP address, parsed user agent, etc.). It should also indicate whether the invocation was unauthenticated (for operations exposed outside of login) or authenticated. For authenticated accesses, information about the actor should also be included. This should indicate the account ID, whether it's a user or a service account, the tenant the actor belongs to, and the authentication mechanism (including client-side session ID or the hash of the API key used). Last, the actor should support impersonation and acting on behalf of other accounts.
- The trace should allow to correlate invocations that are logically related. A good way of achieving this is to generate some initial unique IDs (e.g., ULIDs) on the client side: 1 for the action itself e.g., a button press, plus 1 for each invocation to the back-end this action maps to (typically one). After that, the gateway should generate an originating trace ID, so that these 3 pieces of information stay immutable throughout the chain of invocations. Last, each service that processes the invocation should receive a parent invocation ID, generate an invocation ID, and send this last ID as parent invocation ID for downstream calls.
- This way humans and systems can easily identify retries and logically duplicate invocations.
- Overall, the information in the invocation context allows to determine an idempotency key: this one is typically the external invocation ID, within a namespace composed of the tenant ID and the actor ID (so that different actors and tenants cannot interfere with each other in terms of idempotency). 


- Internationalization (server returns i8n keys, dedicated front-end type to display the actual text from browser locale, changing the settings from user's configuration)
- Features and product modules (representation in the code, who has enabled what, how do you know)
- In-app announcements (changelog, marketing communications, etc.)
- In-app audit log (what users did, when, how, where from, etc.)
- Accessibility
- History of changes for each entity (e.g., for projects, etc.)
- Product instrumentation and attribution (Amplitude for both, vs Amplitude/Pendo/many for instrumentation and Split for attribution, vs home-made)
- Semantic instrumentation (what, how, why a user is doing things)
- Consumption-based billing + base tier
- Attribution (which features are causing a difference in behavior)
- Product requirements and user entitlements (T&C, user properties, proof of address, etc.)

- 1 environment: production (internal tenants vs external tenants)
- Infrastructure as code (Pulumi vs Terraform, configuration drift management)
- Cloud provider (GCP vs AWS vs Azure, vs more than 1 active-passive, vs more than 1 active-active)
- Regions and AZs: 1 vs active-passive vs active-active, 3 AZs
- Provisioning (scripted vs dynamic provisioning, Kubernetes Operators)
- Configuration management (environment, files, properties, tenant segregation, Vault, config maps, rotation, etc.)
- Certificates management (rotation, issuing, certificate authorities, injection, etc.)
- Messaging (authorization, ACLs, custom authorizer with OPA, auto-scaling, partitioning, etc.)
- Push-notifications (MQTT)

- Service-to-service communications (event-driven, service mesh, sidecars with mTLS, etc.)
- Auto-scaling (CPU-based for endpoints, queue-based for event processors)
- Zero-trust security
- Data segregation and replication (by tenant, across geographies for data residency regulations)
- Monitoring (CPU, memory, open connections, etc.)
- Alerts (external ping, unavailability, sagas with timeouts, disk space, brute-force login attempts, etc.)

- Rollouts (Argo Deploy, error-rate monitoring, canary releases, automatic rollbacks, front-end, back-end, mobile)
- Data migrations (as part of releases, framework, before the new instances come up, during the release, after the old instances are gone, using sidecars)
- Logging (asynchronous, correlation, bump the level of logging for a specific invocation)
- Logs collection

- Test strategy (contract, integration, service tests, smoke tests)
- Test tenants, test users, test email server
- Build reports and alerts
- Security build scanning (secret leakage prevention, etc.)
- Local testing
- Local scripts (1 command to do an operation e.g., build and test, so that you don't need to know the right commands)
- Automatic linting and static code analysis
- Ephemeral environments (to test large-scale infrastructure changes, or for performance-intensive changes)
- Performance tests (stress tests, soak tests, etc.) and resilience tests (chaos testing)
- Checks for the data format standards (camelCase vs snake_case vs kebab-case in JSON and Avro)
- API style rules, and compliance checks (params, typos, etc.)
- Auto-update of dependency versions (scheduled, with testing, etc.)
- Code storage (monorepo vs multiple repositories, for what)
- Build pipelines (GitOps e.g., GitHub actions vs build server e.g., TeamCity or Concourse, which handle cascading builds well, signing builds, knowing which version is in production)
- Build tool (Gradle, vs Maven, vs others)
- Packaging (OCI images vs native images e.g., Graal or kotlin native, image repositories)
- Service registry (e.g., Backstage, services with dependencies, so you can go from a vulnerability in a library to all the services affected by it)
- Front-end modularity (components, micro-frontends)
- Back-end modularity
- Accessibility testing (regression testing using Wave, Axe, and Pa11y, https://opensource.com/article/23/2/automated-accessibility-testing)

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
- Integration events (company-wide schemata and registry of topics)
- Querying logs and events manually (authorization, auditability, etc.)
- Data format standards (camelCase vs snake_case vs kebab-case in JSON and Avro)
- Data engineering (OLAP database, pipeline, etc.)
- Manual database operations (manual database operations repository, PRs, merged scripts get executed by the infrastructure, and the result is returned)

TODOs
- Find an image if you can