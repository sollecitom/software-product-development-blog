---
title: "Walking skeleton, what is it about?"
categories: [ "software-development" ]
tags: [ "system-thinking", "architecture", "effectiveness", "startups", "platform-engineering" ]
date: 2023-12-04T05:00:00
draft: true
---

TODO
- What is a walking skeleton
- Why it matters
  - You create a system that works, but does nothing, and then add behavior to it
  - The parts are interdependent, so you need to build them together, not one by one
- What happens if you don't do this?
  - Most companies experience a sharp increase in the cost of change, as they progress, which is often fatal
- When should you do it?
  - Either in the beginning, if you can, or after finding PMF, when you re-write
- Scope
  - (plenty)

TODO (scope)
- Tracing (correlation, who, when, how, where from)
- Features and product modules (representation in the code, who has enabled what, how do you know)
- Authentication (login challenge, SSO, IDP federation, allowing or disallowing email aliases, etc.)
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
- Alerts (external ping, unavailability, sagas with timeouts, disk space, etc.)
- Consumption-based billing + base tier
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
- TODO

TODOs
- Change the lousy title
- Find an image if you can