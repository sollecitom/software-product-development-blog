---
title: "A wishlist for Web 5"
categories: [ "system-thinking" ]
tags: [ "system-thinking", "Agile", "effectiveness", "software-development", "extreme-programming" ]
date: 2024-01-15T05:00:00
draft: true
---

Hype cycles in tech rarely translate to significant changes in our lifestyle. Technology is a wide topic, but let's focus on information systems today, and leave energy, food, water, health, and other important topics for another time.

We made it to 2024, and the current frenzy is about AI. Some people claim it'll change everything. I'm quite skeptical, but let's not digress, and think about the web instead.

If you think about it, the web hasn't significantly changed in the past 20 years or so. Sure, things look better and work faster, but Google Maps came out in 2005. There was a lot of talk about Web 3 and all the changes it should have brought.

So let's assume we finally got tired of NFTs, AI, unicorns, and mini-ponies with Web 4, and we somehow decided to actually try and improve things with Web 5. What would that look like?

In this post I try to imagine what the web could be like, to make people's life easier. I feel we reached a point where further improvements in speed won't significantly improve the experience, so the changes should qualitative.

# Web 5 ideas

There are some requirements, for these ideas to work:

We should build around quantum-secure cryptography. Example algorithms could be Kyber as a key encapsulation mechanism, and Dilithium for signatures. The algorithms are just examples, as they're not confirmed to be fully secure yet.

High-speed internet access should be available country-wide, for free. Other country-wide free services should include a checking account with payments, and a telecommunication service supporting audio and video.

It's important that the government offers these, for free, because the assumption is that everybody should have access to these, in order for some of the points below to work.

Finally, the government should issue every citizen an identity, with a passive chip, falling back to a mobile device.

## Governments as Certificate Authorities for digital identity

Governments could act as Certificate Authorities, issuing quantum-secure certificates, associating a public key with the identity of a person or an organization.

People could verify the authenticity and validity of a certificate using a local cache of the public keys of various governments, without requiring internet access and a connection to a server.

Well-known government endpoints would allow people to receive the public key of a government.

Some of you might scream at the idea of a government responsible for identity management, and wish for a de-centralized approach. Not only things already work like this though, but a central trusted authority is needed to address cases where an identity is somehow lost. Imagine losing your chip or private key, suddenly the idea of a government able to issue you another key-pair associated to your identity sounds pretty great.

## Trust-Based Distributed Ledger

A Trust-Based Distributed Ledger (TBDLT) could help society leverage information in a trusted way. This would only be for information, not for currency. I'm not talking about Blockchain.

The idea is that an entity - a person or an organization - could attest a statement. Statements have a schema, and some data, and can be encoded as bytes, so that an attesting entity could sign them cryptographically.

Anybody could attest anything. The ledger would be decentralized, with local storage. Such a ledger would support storing, sharing, and requesting statements, along with the attestations and the identity of the attestors. Centralized services could provide convenience e.g., storing statements in the Cloud, to have them accessible across devices, and not to lose them.

About timestamps:

1. Every statement includes a creation timestamp, and can optionally include an expiry timestamp to show the limit of its validity.
2. Timestamps are attested by notary services, run by governments and large corporations. The creator of the statement includes a timestamp, and then asks a notary to attest it. The notary only attests it if the difference between the proposed creation time and the current time is within a narrow margin.

An entity could delegate the ability to attest some statements to another entity. This is also a statement, so it can come with validity limits, etc.

Mind that here cryptography does not replace trust, but enhances it. A signature only proves that a person or an organization supports the validity of a statement. You're never force to take anyone's word for something though. It's up to you to decide who to trust and why.

Users can customize their trust preferences, including:

1. Requesting specific attestors - or attestor category - for a given statement type or category. An example is that you might decide to only trust the British Government to attest the right of a British citizen to travel internationally.
2. Requesting a minimum number of attestors.
3. Only considering attestors within a maximum degree of delegation distance.

When an entity presents a statement to another entity, they can include a set of supporting statements, and the receiving entity could use this information bundle to decide whether to trust the original statement being presented. 





Features:

- Mobile free government application:
    - Telecommunications.
    - Trust-Based Distributed Ledger (TBDLT) manager.
    - Password manager.
    - Authentication manager.
    - Peer-to-peer payments.
- Trust-Based Distributed Ledger (TBDLT) for information (not for currency):
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
- Digital identity at the center of all services and applications:
    - It acts as username for all cases.
    - Cryptographic challenges can involve application-specific secrets (stored encrypted within the government mobile application).
    - No more:
        - Email addresses.
        - Phone numbers.
        - Physical addresses for shipping things.
        - Usernames for applications.
        - Passports (as the identity acts as target for entitlements that allow the person to travel internationally).
        - Bank account details (the identity is the target for peer-to-peer payments).
- Cashless society. No more:
    - Carrying money around.
    - ATMs.
    - Tax evasion (all banks need to communicate all transactions to the central bank).

[//]: # (TODO change tags and categories, revist the title, turn the skeleton into a draft)