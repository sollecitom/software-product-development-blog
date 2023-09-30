---
title: "Make the change easy, then make the easy change"
categories: [ "technical" ]
tags: [ "refactoring", "test-driven-development", "design", "object-oriented-programming" ]
date: 2023-09-30T05:00:00
draft: true
---

"Make the change easy, then make the easy change". Didn't Kent Beck say that? He did, didn't he? So why are we talking about this (again)? I just want to clarify a few things about this very good piece of advice.

## The example

To show what I mean, I'm going to use a fictional example.

Imagine you're a software developer working for an upcoming startup that wants to dominate the online clothes business.

You're working on the MVP, and somebody decided that there's only going to be 1 T-shirt available, with 1 size and 1 colour, and the price is going to be $7. More precisely, you'll only be able to order a pair: 2 t-shirts for $14.

## Trade-offs

### YAGNI

You're a good developer, so you start thinking, but then you remember you read something YAGNI. Why don't you just build what's needed uh?

After all why bother doing more than the strictly necessary?

You create an HTTP endpoint that accepts a `POST` on `/orders`, without any further order-related information, and you process each of them by charging $14 and by initiating the delivery of 2 t-shirts of the 1 size and colour you support. You add a test (before or after), and you're done.

#### Outcomes

You haven't wasted any time making choices explicit, modelling your domain, writing serialization logic, making things modular and decoupled, reasoning about where information comes from, or making bad decisions about using doubles for money amounts.
Sounds great uh?

You delivered on the requirements, made the customers happy, and saved time you could have spent gold-plating the implementation. Aced it, OKRs met, mission accomplished. You got closer to that promotion for sure.

TODO