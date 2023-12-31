---
title: "Teams and teamwork: the most important and misunderstood ingredient in any company"
categories: [ "teamwork" ]
tags: [ "system-thinking", "Agile", "effectiveness", "software-development", "team" ]
date: 2023-12-31T05:00:00
draft: false
---

I had a discussion on Twitter yesterday about whether a software development team should restrict the freedom of its members, and enforce shared approaches and ways of working. I and others were adamant that yes, this should absolutely be the case. Others were horrified, saying this is everything that's wrong with our industry.

This made me realize that I never wrote about teamwork in software product development. This is borderline insane, as I'm hugely passionate about system thinking and teams (which are systems, after all), and I have very strong opinions about this.

And so, here we are, let's talk about teams, teamwork, and the role of management in software product development.

## You probably don't work in a team

Ask any software developer whether they work as a team, and sure as shooting they'll tell you they do. But do they? I worked in quite a few places and, in my experience, people rarely work as teams in software companies.

Teamwork is often misunderstood. I guess the word "team" feels more personal, and evokes better emotions, and that's why most people use it interchangeably with "group of co-workers".

But a team is not simply a group of people working towards the same goal. And I believe that many of the problems companies experience derive from this misunderstanding, resulting in anti-systemic practices that prevent true teamwork.

## Definition of a team

So what's a team then? A team is a social system, and as such it is a qualitatively different entity than a few individuals working alone side-by-side. To understand what this means, let's look at what "system" and "social" mean, in this context.

When it comes to the definition of a system, I could never explain it better than by quoting Russell Ackoff:

- "A system is a whole that consists of parts each of which can affect its behavior or its properties. Each part of the system when it affects the system is dependent for its effect on some other part. In other words: The parts are interdependent."
- "No part of the system or a collection of parts of the system has an independent effect on it. Therefore, a system as a whole cannot be divided into independent parts."
- "The essential or defining properties of any system are properties of the whole which none of its parts have. The essential property of an automobile is that it can carry you from one place to another. No part of an automobile can do that."
- "Therefore, when a system is taken apart it loses its essential properties. A system is not the sum of the behavior of its parts, it’s a product of their interactions. The performance of a system depends on how the parts fit, not how they act taken separately."

About the word "social", Russell Ackoff, once again, categorized any system as either:

- A machine, where the overall system has no purpose, and neither have the parts. A machine serves the purpose of its creator.
- An organism, where the overall system has its own purpose, but the parts do not. You have a purpose, but your liver, your brain, and your hands don't.
- A social system, where the overall system has its own purpose, and the subsystems also have their own purposes.

Therefore, a social system is a system whose parts have their own purpose. The beliefs and behaviors in a team are interdependent, and this interdependence develops and evolves over time, in a reciprocal manner.

Most of the issues and the dysfunction companies experience derive from either:

1. Dealing with companies or teams in an anti-systemic way, by focusing on the parts, rather than on the system as a whole.
2. Treating companies, teams, and people as if they were machines, forgetting that they have their own purposes.

Today though, I want to focus on how most "teams" within software companies aren't working as a system. I might come back another day to talk about the other mistakes mentioned above.

## Why this matters a lot

[//]: # (TODO change this section's title)

The reason I obsess about teams is that the difference in effectiveness between a team and a group of co-workers can be dramatic, in the right context.

Not all groups of co-workers are teams. As an example, street cleaners don't typically work as a team. They all together have breakfast, get to the location, exchange jokes and banter, plan the work, and commute back. But behaving socially and having a common goal aren't sufficient for a group to be called a team.

The defining characteristic of a team is that the team members work synchronously together toward the goal, without splitting the task and working individually.

Street cleaners divide the work among themselves, and then work individually. This works because cleaning streets is a linear activity, so if I clean a street, and you clean another, the overall outcomes are the sum of our individual outcomes. In these circumstances teamwork isn't necessary, and a working group might even be better.

Working as a group or as a team is a choice, even if the outcomes are typically very different.

A good example is hunting. You can decide to hunt as a group, or as a team. As a group, you split the work, so I hunt in an area, and you in another. At the end of the hunt, we put together what you and I managed to get, and bring it back to the village. We work in parallel, more efficiently, and cover more ground. What's not to love then?

Well, as long as we're hunting things that are trivial to hunt, like frogs, this actually works best. What if we're hunting something bigger or faster than us though? Perhaps in a dangerous environment with many dangerous predators? Humanity discovered a long time ago the value of working as a team, and that hunting alone was a great way of dying.

Remember? "The essential or defining properties of any system are properties of the whole which none of its parts have". A team is capable of things none of its members could accomplish individually. This matters a lot when an activity is not linear, cannot be divided in independent activities, and the overall result is not the sum of the result of the smaller tasks.

We cannot hunt a part of a bear each. We're either capable of hunting a bear as a team, or we cannot hunt one.

Only teams allow specialization of roles. If we're splitting the work, you're forced to be self-sufficient, because you'll be working alone a lot. Teams, on the other hands, thrive on diversity. Adding more people that don't bring new strengths doesn't improve a team.

In Ocean's Eleven, none of the gang's members could have pulled the heist on their own. It's only by acting as a team that something nobody could achieve became feasible. A gang made of only one type of specialist would have failed spectacularly.

Examples of teamwork are everywhere, not only in movies. A football team made of only goalkeepers, defenders, midfielders, or forwards wouldn't go far. Even more significantly, a football team without any one of these roles also wouldn't do well.

Once again, it's the nature of the activity that determines the best approach. If an activity is not linear, splitting the work never makes sense. No competitive activity is linear, hence the importance and prevalence of teams in sports and war.

## Software development is definitely not linear

So the million-dollar question is whether software development is a linear activity. If it is, all good, and people can work how they want. But if it's not a linear activity, groups of co-workers are going to be dramatically outperformed by true teams.

Software development isn't a competitive activity, no other software team is there trying to outmaneuver and sabotage you, so you don't need to adapt how you work to what your competitors are doing. Even in product development competition is more a fantasy some folks have than an actual threat to a company. Sure, other companies also want to capture the market, but you can decide not to compete, and to find your own niche other companies aren't interested in. The goal is making a profit, not world domination. It's not a zero-sum game.

Is there hope then? Hardly so. Software development can never be linear, because it's about developing software systems. A system's performance is never the sum of its parts, but the product of their interactions. So you can never split the development of a software system, work in parallel, put the pieces together, and end up with great outcomes.

I can hear some of you screaming. And indeed, there are some exceptions to what I just claimed. If a software system is trivial and tiny e.g., a low-throughput CRUD application with small amounts of data, people can easily divide the tasks and work alone in parallel. It might even be better.

In many cases, though, software systems are large and complex, having to support a large concurrent number of users while maintaining a low latency. They can also involve large amounts of data, have strict data integrity and privacy requirements, and must continue to work in presence of network partitions and hardware faults.

For such projects, individuals working in parallel cannot cope. That's because, in an effective team, the individual strengths merge to form a collective understanding much higher than the sum of the parts. And so no team member could either design or build such a large system on their own, regardless of the time they have available, and yet the team can.

Product development is even less linear, since the goal is to find and address a need customers are willing to pay the company for. It's not about building stuff, but about discovering problems, opportunities, and solutions. You cannot solve 1/6 of the puzzle and put all the pieces together.

## What if it's not linear after all?

So what then? What changes if you believe that software product development is not a linear activity? As it turns out, you behave quite a few things.

First of all, you give up the fantasy that people are interchangeable. Unlike mechanical parts, two people are never identical. So you can never replace a team member without the whole team changing. Even worse, the same person or even the same pair of people will produce a different effect if they join different teams. A person that stabilizes a team might destabilize another. When discussing deliverables and initiatives, you now have to think about which people you need, rather than just how many.

Secondly, you end up using teams as the unit of work allocation. Assigning tasks to the individual team members makes no sense, because the outcomes are not the sum of the individual accomplishments. "Bob's job will be hunting 1/6 of the bear".

You only now hire people with a specific team in mind. Every team needs to be carefully assembled by mixing in various strengths, personalities, backgrounds, attitudes, and skills. So how could you ever look for generic "back-end engineers" company-wide, and then figure out where to place them? Unthinkable.

And the thought of assessing individual performance now makes you laugh. Somebody's sense of humor or curiosity might contribute to the effectiveness of the team in ways that a more skilled and hardworking replacement could never hope to match.

Finally, the way you structure the incentives also changes. How can you reward a forward for every goal they score, knowing that winning the game depends on how well the team plays together? What do individual incentives do to teamwork? Wouldn't that player be tempted to take every shot, rather than passing the ball? It might result in a higher bonus for themselves, after all, even if the team might win a lot less because of this.

## Individual freedom, teamwork, and management

Let's go back at the original point of contention on the Twitter discussion. A team must restrict the freedom of its members. This is a consequence of its systemic nature. The way a team works is designed holistically to produce the desired outcomes, and this is interdependent with the team members than end up making the team.

It should be obvious and a no-brainer. If the performance of the team is the product of the interactions between its members, how well you fit the team's chosen approach matters way more than your individual skills. And I say chosen, because different teams can play in radically different ways, and achieve their goals.

The most important job of any manager is developing effective approaches, and then carefully assembling teams that are well-formed to play that way. The parallel with the world of sports and military is clear.

Within a team there's no space for uncoordinated activity. You can be a great football player but, if you don't want to pass the ball a lot, Barcelona is not the right team for you. You can be a great shot but, if you love whistling, and you do that while we're sneaking our way through an enemy base, you're a liability.

## Parting words

Whew, my last post for this 2023! I hope you now have an appreciation of the difference between a group of co-workers and a team, and that you can tell which one your company adopts.

I very vocally believe that software product development is a nonlinear activity best done in teams, and I strongly favor ensemble programming because of this. So if you want to work alone or remotely, be upfront and find a team that operates that way. But don't fool yourself thinking this should be your choice after joining any team.

You don't need to agree with me, but please let me know your thoughts, especially if you disagree!