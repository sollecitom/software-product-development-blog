---
title: "The pinnacle of software development"
categories: [ "technical-practices" ]
tags: [ "software-development", "Agile", "effectiveness", "continuous-delivery", "test-driven-development" ]
date: 2023-12-28T05:00:00
draft: true
---

People talk a lot about the various technical practices, like Test-Driven Development, Ensemble Programming, and Trunk-Based Development. And yet not many people seem to be talking about how these practices work together in synergy.

This is problematic, because these are parts of your system of work, and what matters is the overall effectiveness of how you deliver software. Well, how you deliver software is a subsystem of product development, which is itself a subsystem of your business, but let's focus on software development for now.

You cannot evaluate whether individual practices like Test-Driven Development are effective, because the effectiveness of a system is not the sum of its parts, but the product of their interaction. So when you reject TDD, you end up with a system of work that doesn't use TDD, and you need to compare this end-to-end system with alternatives that leverage TDD.

And how can you assess the effectiveness for two systems of work? You have to assess them based on the properties they produce. Do you get the properties that you want? And do you happen to also get any undesired properties?

# Desired properties for a software development system of work

In general, an effective system of work sustainably meets the needs of all the folks that matter. But how do you know whether a system of work does that? These are the properties such a system should display:

1. Delivers value to the company's customers and users. The value is how significantly a company improves the lives of its customers. The more value delivered, the better.
2. Delivers value earlier and more frequently. Value builds up over time, so software delivered earlier produces more value than software landing at a later time. Sooner, more frequently, and more evenly is better.
3. Controls risk (reputation, security, compliance, legal, business continuity, etc.). This means preventing bugs, live incidents, downtime, vulnerabilities, etc. Here I didn't say "minimizes", because it's about maximizing value while keeping risk acceptable, not the other way around.
4. Operates sustainably: the system should be able to run indefinitely, without any performance degradation or accumulation of risk. If something now takes twice as long as it used to take a year ago, this endangers the company. If sprinting gets people exhausted and then capacity tanks, this endangers the company.
5. Allows flexibility: remains capable of concentrating the effort on any product or technical area. Embraces changes in the direction and late information. Over-specialization within or across teams endangers this property, and so does a waterfall approach.
6. Is resilient to absences and to employee attrition. If when a person is off or leaves the ability to work tanks, this is a danger for the company.
7. Meets people's need for self-actualization. People need to feel they're improving their skills by having fun solving meaningful problems with competent peers.
8. Minimizes waste. Waste is anything that doesn't directly contribute to improving these properties. It includes rework, fire-fighting, unused features, pointless meetings and activities, unnecessary people, etc.

[//]: # (TODO)