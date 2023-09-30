---
title: "Make the change easy, then make the easy change"
categories: [ "technical" ]
tags: [ "refactoring", "test-driven-development", "design", "object-oriented-programming" ]
date: 2023-09-30T05:00:00
draft: false
---

"Make the change easy, then make the easy change". Didn't Kent Beck say that? He did, didn't he? So why are we talking about this (again)? I just want to clarify a few things about this very good piece of advice.

## The example

To show what I mean, I'm going to use a fictional example.

Imagine you're a software developer working for an upcoming startup that wants to dominate the online clothes business.

You're working on the MVP, and somebody decided that there's only going to be 1 T-shirt available, in 1 size and 1 colour, and the price is going to be $7. More precisely, you'll only be able to order a pair: 2 t-shirts for $14.

## When YAGNI goes wrong

You're a good developer, so you start thinking, but then you remember you read something about YAGNI. Why don't you just build what's needed for now?

After all why bother doing more than what's strictly necessary?

You create an HTTP endpoint that accepts a `POST` on `/orders`, without any further order-related information, and you process each of them by charging $14 and by initiating the delivery of 2 t-shirts of the 1 size and colour you support. You add a test (before or after), and you're done.

You haven't wasted any time making choices explicit, modelling your domain, writing serialization logic, making things modular and decoupled, reasoning about where the information comes from, or making bad decisions about using doubles for money amounts.

It feels pretty good.

You delivered on the requirements, made the customers happy, and saved time you could have spent gold-plating the implementation. Aced it, OKRs met, mission accomplished. You got closer to that promotion for sure.

## The problem 

By not identifying circumstantial conditions and temporary constraints you created a liability for your organisation.

But could we not evolve the code later, when needed? Isn't Agile about delaying decisions after all?

Agile is about delaying decisions until the latest responsible moment. Here we're way past that point.

The problem is that the cost of doing things changes during the lifecycle of a project. And your employers aren't aware that you traded off a few hours of additional work for a much higher risk and effort down the line.

With any luck, the requirements will evolve quickly enough that you'll feel naive, you'll undo the damage, but nothing too bad will happen.

In a much less forgiving scenario, your company will thrive for quite a while before requiring changes that your implementation doesn't support. Imagine going on for a year or so under the same requirements. You build UIs, logging, monitoring, metrics, alerts, an inventory system, and more. All while keeping everything implicit as above.

When your requirements will finally expand, the effort, risk, and cost will be obscene. If your company will need those changes quickly, it might be a big problem. The company might not even survive.

## YAGNI done right

What's the alternative then? It's YAGNI, but done right.

You model enough, without imagining future requirements that you ain't going to need.

But isn't this what we did above?

Nope. We need a distinction. YAGNI is about behaviour, not quality.

The problem with the approach above is that, by modelling exactly accordingly to the current requirements, you leave information out of your model. When your requirements evolve, you'll not only need to fix the logic, but you'll be forced to change everything to get the information you need for the decision making.

What do you do for the scenario above instead then?

1. You create a product ID for the 1 t-shirt you "currently" only sell.
2. You create the concept of an order, supporting multiple items and quantities.
3. You introduce the concept of product options, to allow sizes and colours.
4. You adopt a money amount type to model prices and costs.
5. You abstract pricing an order behind an interface.
6. You abstract checking whether an order is valid behind an interface.
7. You create an endpoint to accept orders.
8. You take care of serialising and deserialising your models.
9. You create modules and layers, and test these in isolation.

And then, for the time being:

1. You implement the order validator in a way that endures the only product available is your t-shirt, in that 1 size and colour, and that the quantity ordered is exactly 2.
2. You return $14 as a money amount type from the order pricing implementation.
3. For now all the logic might even stay in the code, as opposed to living in a database (price, existing products, existing product options, order constraints) (debatable, as changing these will require a code change an a release, but could work for a while).

When your company's requirements will change, you'll evolve your pricing or validation implementation, without having to change the whole codebase to propagate the information you didn't use to need but you now need.

This is typically easy and painless, because you made the change easy, and then you made the easy change.

## Final words

It's important to separate speculating about future behaviour from modelling your domain without removing information you might not currently need, but that is part of the decision in the general case.

So if the cost of an order depend on the order, the time, and the shopper, the abstraction that models the pricing should receive this information, even if at the moment it doesn't use it.

This applies equally well to domain events. You include all the information you have, not what you need for the next processing step.

And, with that said, I'm done. I hope this will make you think, even if you end up disagreeing with me.