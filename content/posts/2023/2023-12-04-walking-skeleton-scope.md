---
title: "Walking skeleton, what is it about?"
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

Let's have a look at the scope of a walking skeleton. All these aspects should be addressed, in a way where they all work together. With a competent team of senior people, you can build a walking skeleton in 4 to 6 months, for most projects. Small-scale projects won't likely require this at all, or you can focus only on some aspects. 

## Authentication

- You'll likely need a Single-Sign On option, and Identity Provider federation if in B2B.
- For the non-SSO option, you'll need MFA, email verification, password storage (Argon2 hashing or similar), and password reset.
- You need to know when a user logs in the first time, when they log out, etc.
- You should decide whether to accept email aliases e.g., somebody+something@gmail.com.
- You should pick between delegated or mapped identity, for IDP federation cases. With delegated identity, the external IDP tells your IDP the identity of the user, and you take it at face value. With mapped identity, you map the identity in the external IDP in your own IDP. In any case, you should ensure that when an identity is removed from an external IDP, it also gets removed from your IDP. 
- You'll almost always want to either host an open-source solution like Keycloak, or to go with a managed service like Okta.

## Token management

- You'll need to issue, rotate, and verify tokens, as part of your authentication workflow.
- Certificate management (below) is a prerequisite for this. You could choose to have a single certificate (with rotation), or different certificates across different tenants (if B2B, based on subdomains) or geographies.
- You should include a unique client-side session ID in your tokens, along with the token's validity start and end timestamps.
- The duration of a token should be a maximum of 30m to 1 hour.
- You also need to choose an algorithm, ideally EdDSA, rather than RSA or ECDSA, as it's faster, requires shorter keys, and it's considered more secure.
- In terms of token structure, JWTs are a safe bet.

## Tenant isolation

- This is mostly a B2B concern.
- Tenants should be isolated from each other in terms of workflows.
- The data for a tenant should be stored and encrypted separately from the data of other tenants.
- Each tenant should be able to set up SSO with their own IDP, and to enable IP address range restrictions if they want.
- To separate the entry-points (required for the above), you should consider creating a subdomain per tenant e.g., <tenant-name>.<your-root-domain>.com. This needs to happen automatically when you onboard a new tenant.
- If you offer environments, you'll likely need infrastructure isolation, to prevent activity from a tenant to affect another tenant's workflows.

## Authorization

TODO

TODO (scope)
- Tracing (correlation, who, when, how, where from)
- Features and product modules (representation in the code, who has enabled what, how do you know)
- Authorization (how to query for permissions, scoping with containers, how to ensure authorization is the same for a whole invocation, OPA)
- Gateway (vs no gateway, along with responsibilities, open source vs commercial vs homemade)
- Circuit breakers and bulk-heads (if needed)
- Test strategy (contract, integration, service tests, smoke tests)
- Performance tests (stress tests, soak tests, etc.) and resilience tests (chaos testing)
- Security build scanning (secret leakage prevention, etc.)
- Configuration management (environment, files, properties, config maps, rotation, etc.)
- Thread pools (connections to databases, etc.)
- Service-to-service communications (event-driven, service mesh, sidecars with mTLS, etc.)
- Messaging (authorization, ACLs, custom authorizer with OPA, auto-scaling, partitioning, etc.)
- Logging (asynchronous, correlation, bump the level of logging for a specific invocation)
- Event propagation (Pulsar)
- Event storage (Pulsar with Tier Storage vs EventStore vs Postgres)
- CQRS
- Auditability
  - Commands and queries as events
- API style (REST vs RPC vs GraphQL)
- Auto-scaling (CPU-based for endpoints, queue-based for event processors)
- Provisioning (scripted vs dynamic provisioning, Kubernetes Operators)
- Rollouts (Argo Deploy, error-rate monitoring, canary releases, automatic rollbacks, front-end, back-end, mobile)
- Alerts (external ping, unavailability, sagas with timeouts, disk space, brute-force login attempts, etc.)
- Consumption-based billing + base tier
- Logs collection and searching
- Tenancy model (with nestable containers)
- 1 environment: production (internal tenants vs external tenants)
- Cloud provider (GCP vs AWS vs Azure, vs more than 1 active-passive, vs more than 1 active-active)
- Regions and AZs: 1 vs active-passive vs active-active, 3 AZs
- Build reports and alerts
- Auto-update of dependency versions (scheduled, with testing, etc.)
- Architecture (orchestration vs choreography, state snapshot vs stored state as the source of truth)
- Infrastructure as code (Pulumi vs Terraform, configuration drift management)
- Zero-trust security
- Querying events manually (authorization, auditability, etc.)
- Back-office (tenant management, enabling features and modules, event-driven)
- Manual database operations (manual database operations repository, PRs, merged scripts get executed by the infrastructure, and the result is returned)
- GDPR and PII data handling (per-end-user symmetric encryption keys, with the data encrypted as part of the events)
- Integration events (company-wide schemata and registry of topics)
- Data engineering (OLAP database, pipeline, etc.)
- Local scripts (1 command to do an operation e.g., build and test, so that you don't need to know the right commands)
- Idempotency (throughout, with 3rd-party providers, etc.)
- Shared libraries (yes vs no, versioning, monorepo vs separate libraries, what for)
- Currency (how to model, what to do, based on fundamental units)
- Certificates management (rotation, issuing, certificate authorities, injection, etc.)
- ID generation (ULIDs, TSIDs, partitioned, etc.)
- Data segregation and replication (by tenant, across geographies for data residency regulations)
- Encryption (symmetric AES and SHA-256/SHA-512 for hashing, BouncyCastle, runtime algorithm choice vs static, FIPS vs non-FIPS, post-quantum e.g., Dilithium and Kyber)
- Password storage (salting, peppering, algorithm (not SHA) but Argon2)
- Personal Access Tokens and API Keys generation (Argon2 algorithm, encoded client-side session ID, encoded from and to instants)
- JSON (camelCase vs snake_case vs kebab-case)
- Server-pushed notifications across channels (MQTT vs websockets, vs commercial)
- Asynchronous request-reply to serve synchronous requests (with NATS)
- Internationalization (server returns i8n keys, dedicated front-end type to display the actual text from browser locale, changing the settings from user's configuration)
- Accessibility (regression testing using Wave, Axe, and Pa11y, https://opensource.com/article/23/2/automated-accessibility-testing)
- In-app announcements (changelog, marketing communications, etc.)
- In-app audit log (what users did, when, how, where from, etc.)
- History of changes for each entity (e.g., for projects, etc.)
- Client-side SDK (yes vs no, domain-driven style vs service style, test extensions, whether to give it to customers)
- CORS
- Monitoring (CPU, memory, open connections, etc.)
- Product instrumentation and attribution (Amplitude for both, vs Amplitude/Pendo/many for instrumentation and Split for attribution, vs home-made)
- Front-end modularity (components, micro-frontends)
- Code storage (monorepo vs multiple repositories, for what)
- Build pipelines (GitOps e.g., GitHub actions vs build server e.g., TeamCity or Concourse, which handle cascading builds well, signing builds, knowing which version is in production)
- Build tool (Gradle, vs Maven, vs others)
- Service registry (e.g., Backstage, services with dependencies, so you can go from a vulnerability in a library to all the services affected by it)
- Restarting message consumers with the same local cluster ID
- Packaging (OCI images vs native images e.g., Graal or kotlin native, image repositories)
- Runtime optimizations (garbage collector and options, memory, etc.)
- Data migrations (as part of releases, framework, before the new instances come up, during the release, after the old instances are gone, using sidecars)
- Data tweaks (compression, dynamic resizing of images, CDNs)
- Object storage (pre-signed upload and download links, quarantine buckets, hash-based duplication checks if the size matches, PII handling with either tagging and deleting or template + encrypted data, etc.)
- Semantic instrumentation (what, how, why a user is doing things)
- Ephemeral environments (to test large-scale infrastructure changes, or for performance-intensive changes)
- Test tenants, test users, test email server
- Local testing
- Product requirements and user entitlements (T&C, user properties, proof of address, etc.)

TODOs
- Change the lousy title
- Find an image if you can