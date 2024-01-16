---
title: "A wishlist for Web 5"
categories: [ "system-thinking" ]
tags: [ "system-thinking", "Agile", "effectiveness", "software-development", "extreme-programming" ]
date: 2024-01-15T05:00:00
draft: true
---

Skeleton:

- Lot of hype for AI these days, but will it change anything meaningful?
- In technology there are often hype cycles about things, but society rarely changes.
- There are many important aspects e.g., energy production and distribution, food, etc., but let's focus on information systems today.
- There was a lot of talk about Web 3 and all the changes it should have brought. Let's assume we got tired of NFTs, unicorns, and mini-ponies with Web 4, and we actually wanted to improve something with Web 5.
- This post is a wishlist for how Web 5 could work, to make people's life easier.

Features:

- Quantum-secure cryptography e.g., Kyber for key encapsulation mechanism, and Dilithium for signatures.
- Country-wide high-speed internet access, for free.
- Telecommunication service for everybody, for free.
- Checking account for everybody, for free.
- Identity registry for entities.
    - With public keys.
    - For both people and organizations.
    - De-centralized with Trust-Based Distributed Ledger (TBDLT).
    - Backed by centralized services for convenience.
- Trust-Based Distributed Ledger (TBDLT) for information (not for currency):
    - Statements can be represented digitally, and signed cryptographically by attestors. Anybody can attest anything.
    - A distributed ledger with local storage facilitates storing, sharing, and requesting these attested statements.
    - Centralized services provide convenience.
    - Cryptography does not replace trust, but enhances it. A signature proves that a person or an organization attests a statement.
    - Statements include timestamps for when they were created, and might include timestamps to show the limits of their validity.
    - Creation timestamps are provided by notary services run by governments and big corporations. The notary attaches a timestamp to a statement, and signs cryptographically the outer metadata.
    - Users can customize their trust preferences, to request specific attestors for specific statement types or categories, to enforce a minimum number of signatures, to only allow a maximum degree of delegation, etc.
    - Example 1:
        - I can decide to trust a statement about a person being a British Citizen only if anybody working for the British government at the time signed it.
        - The worker can convince me they were working for the British government at the time, by sharing a statement signed by other employees, all the way up to a key belonging to the government itself.
        - I can check the timestamps of all statements involved in providing trust against the public keys of the notaries who signed them.
    - Example 2:
        - I purchase a train ride, and receive a cryptographically signed piece of information with details about my entitlement.
        - When I show up at the gate, the gate gets my entitlement through a QR-code, and verifies the signature against its own trust policies.
        - Since the train company signed my entitlement to get on board, and since the current time falls within the allowed time window confirmed against the notary's signature, the gate opens.
- Job-specific semantic contracts:
    - They describe what commands, queries, and subscriptions that an entity allows, along with how to perform those invocations.
    - The schemata evolve using the decentralized Trust-Based Distributed Ledger (TBDLT).
    - These completely abstract the medium used to communicate.
    - Example 1:
        - A person exposes commands to request to be added to the inbound whitelist, and to request to initiate a voice call.
        - The telecommunication service only allows people registered to an inbound whitelist to request to initiate a voice call with someone.
        - When you want to be allowed in, you first have to request it with the person you want to call in the future. This request can come with an expiry timestamp.
        - If you're allowed to call, you can request to initiate a voice call, and the service routes that to the person.
        - If the person accepts the call, you're talking over voice.
        - Government services would come pre-enabled in the whitelist, so that they can request a call at any time.
        - The identity of both parties is verified with asymmetric cryptography.
        - You don't need any protocol-level information e.g., a phone number.
        - This would eliminate most scams that happen over the phone, and all undesired advertisements and services.
    - Subscriptions allow people to communicate changes in their information to interested parties.
        - They are pushed-based by the party that changes their information.
        - Interested parties request to subscribe to changes in specific pieces of information (statements), based on their type or category. Entities can accept or reject these requests.
        - Subscription requests can include an expiry timestamp.
        - When the information changes, the party that changed the information proceeds to notify the interested parties with peer-to-peer calls.
        - A centralized notification service can be used for convenience, falling back to decentralized peer-to-peer calls if it's unavailable.
    - Example 2:
        - People can ship packages to an entity, without having to know their physical address.
        - Government shipping services can request to subscribe to changes in the physical address of an entity.
        - When an entity changes their physical address, the government shipping service is notified.
        - Shipped goods reach their target entity regardless of changes to their physical address.
    - Example 3:
        - A restaurant exposes queries to see the menu, the opening times, and the free slots. They also expose commands to make a reservation, and to get in contact over voice (if previously whitelisted).
        - A person browses the menu, checks when a free slot is, and requests to book a table at a time.
        - Given the semantic nature of these commands, they can do this with a few clicks, and without dealing with phone numbers or downloading PDFs.
    - Example 4:
        - A person has access to a command that notifies subscribers that they're in danger.
        - People (relatives), organizations (insurance companies, GPs), and government services (police, ambulance service) can subscribe to these.
        - When the person feels in danger, they invoke the command, and all the interested parties are notified.
    - Workflows can be composed based on different commands, queries, and subscriptions.
    - Example 5:
        - The person in danger can pre-authorize certain interested parties to invoke certain commands and to get some (temporary) subscriptions accepted automatically.
        - So when the person declares that they're in danger, some interested parties can receive a subscription to the person's position (through GPS), and know their heart rate and vitals.
        - Workflows can be composed on both sides, so on receiving notification that somebody is in danger, an entity could automatically trigger a response on their side e.g., requesting people closest to the location of the person in danger to intervene.
    - TODO

[//]: # (TODO change tags and categories, revist the title, turn the skeleton into a draft)