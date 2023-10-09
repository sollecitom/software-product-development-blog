---
title: "The 3M Rule of management"
categories: [ "management" ]
tags: [ "metrics", "OKRs", "KPIs", "measurements" ]
date: 2023-10-07T05:00:00
draft: false
---

Metrics and indicators are amazing when used appropriately. But problems arise when people either:

1. Use metrics as targets. I wrote a [post about this](https://sollecitom.github.io/software-product-development-blog/posts/2023/2023-07-09-management-by-objectives-is-wishful-thinking/), so I'm not going to explain why this is the case again.
2. Focus exclusively on things that can be measured, while neglecting things that cannot.
3. Adopt metrics without understanding their context. I wrote a [post about McKinsey's software development productivity nonsense](https://sollecitom.github.io/software-product-development-blog/posts/2023/2023-08-31-developer-productivity-fuss/), so I'm not going to expand on this either.
4. Don't factor in any delays between inputs and outputs.
5. Believe they need metrics in order to manage anything.

Today I want to challenge the last point, that you need metrics in order to manage anything.

## The trend

Companies are developing an obsession with metrics. "OKRs", "KPIs", and "data-driven" are on everyone's mouth. Most companies even go as far as creating roles, teams, and departments solely responsible for defining and tracking metrics across the whole company.

This inevitably introduces problems, and when people bring these up and complain, they're usually met with the weaponized quote that "you cannot manage what you cannot measure".

## The 3M Rule of Management

On the contrary, I propose the following 3M Rule of Management:

> "If you cannot Manage what you cannot Measure, then you're a Moron."

## A bit of theory

Before we dig deeper into why I believe you shouldn't need metrics to manage, let's go over a few definitions.

### Measurement

> The process of associating numbers with physical quantities and phenomena.

Measurements concern themselves with quantities. Not every type of feedback is quantitative. Keep this in mind, because it'll be important in a bit.

### Management

> The process of dealing with or controlling processes, things, or people.

I'd argue that management is exclusively about processes, but let's not diverge. Management is about steering something to produce desired outcomes.

### Moron

> Silly or unwise; showing poor judgment or little intelligence.

With the word "moron", I mean someone that struggles with boilerplate and routine activities.

## A counter-example

If it was true that "you cannot manage what you cannot measure", we'd be hard-pressed to find examples of people successfully managing without measurements.

And if we could effortlessly find examples of normal people successfully managing without measurements, then it'd imply that a person not capable of managing what they cannot measure would be a moron.

I hope it's clear that people spend their entire life managing things they cannot measure. Some examples include:

- Relationships with other people, including spouses or partners, children, parents, siblings, co-workers, friends, etc.
- Eating and drinking.
- Hunting, fishing, or farming.
- Dressing yourself according to the weather.

But I want to give a longer explanation of how nonsensical this notion that you cannot manage what you cannot measure is, to clear all doubts.

I'm originally from Italy, so it's time to talk about pasta.

### The "right" amount of salt in a pasta dish

Imagine that you're having friends for dinner, and you decide you're going to cook some pasta, with a tomato-based fish sauce.

Pasta dishes tend to be easy, involving simple techniques, and no more than like 10 ingredients. But let's make this even simpler, by exclusively focusing on salt. As part of the cooking, you need to add salt to your dish, with the goal of producing something you and your friends will enjoy.

If you're from the "you cannot manage what you cannot measure" school of thought, you might believe that it's a simple matter of measuring the right amount of salt. You scientifically determine that the right amount of salt is X grams per kilo of pasta, stick to that, and you'll be fine.

Sounds right uh? The thing is, nobody cooks like this. Weighing the salt would be both inefficient and ineffective.

If you're obsessed about metrics, you might claim that:

1. Measuring is needed for mass-production, because understanding doesn't scale.
2. Measuring might not be needed by the experienced cooks, but it would help the inexperienced ones.

You'd be right to say that if you want to mass-produce food, understanding doesn't scale. You cannot mass-produce certain things, though. There's no mass-produced pasta with tomato-based fish sauce. It'd be terrible. Software products are the same. It's about development, not production.

And when it comes to the claim that measuring the amount of salt would help the inexperienced cook, this is totally not the case. Worse even, it'd prevent the inexperienced cook from ever learning how to cook.

First of all, no "right" amount exists, because the goal is to please people, and people have different tastes. Software product development is the same, it's about dealing with people, needs, and preferences, not universal quantities.

Secondly, the other ingredients contribute to the saltiness of the dish, and no two ingredients are ever the same. You can never cook the same dish twice. The fish you buy, the tomatoes, they're never the same. And the cooking process will also be different. The hob, the pots and pans, all different. So the same amount of salt will produce different results when the other ingredients differ. This is the same in software product development, and that's why what worked elsewhere or in the past might not work in your company at present.

And, finally, salt doesn't only contribute to the saltiness of the dish. Salt accentuates foods' own taste (its primary use). In doing so, it also makes the water contained in certain foods come out, changing the cooking process as a result. So even when you add salt is important, not just how much you add, because salting is interdependent with the cooking mechanism, so that if you want crispy onions, you shouldn't put in any salt before they're crispy.

Overall, even in this extremely simplified version of cooking a simple dish, there are complexities and nonlinear effects that make a metrics-based approach unfeasible. And yet most people can consistently manage to cook a good dish, without measuring the amount of salt (or anything else).

And this means that not only you can manage what you cannot measure, but also that if you cannot manage what you cannot measure, then you wouldn't be able to manage it even if you had those measurements.

## It's about understanding, not metrics

The reason why people can manage without relying on metrics is because the key to managing well is understanding, not data.

Understanding produces principles about why things work the way they work, enabling us to orient ourselves when dealing with uncertainty.

## Back to software product development

Software product development is incredibly more complex than cooking some pasta.

There are entire dimensions of added complexity, including:

1. It's done in teams, working together.
    - This is not the case, even in professional kitchens, as people split the work between them, rather than collaborating on the same dish.
2. The subject is far removed from the realm of common sense and experiences.
    - The untrained person knows next to nothing about it.
    - Good and bad products and software are not immediately recognizable, unlike food.
3. It's much longer term.
    - You don't often get to start from scratch
    - Software products and systems get continuously evolved and adapted to new requirements.
    - What you did in the past influences and limits what you can do in the future.
4. The landscape changes continuously.
    - After tomatoes made their way to Europe, the recipe for pasta with fish and tomato sauce stayed virtually unchanged. Even the tools are roughly the same.
    - In software, things change continuously. Entire paradigms appear and force everybody to shift. Cloud providers, containers, orchestrators, infrastructure as code, etc.
5. The scale of the system is much larger.
    - The recipe for pasta with fish and tomato sauce might involve 10 ingredients or so.
    - A software product might involve 10s or 1000s of systems, features, and moving parts.