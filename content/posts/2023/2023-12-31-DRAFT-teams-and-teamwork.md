---
title: "Teams and teamwork: the most important and misunderstood ingredient in any company"
categories: [ "teamwork" ]
tags: [ "system-thinking", "Agile", "effectiveness", "software-development", "team" ]
date: 2023-12-31T05:00:00
draft: true
---

Ask any software developer, and they'll tell you they work in a team. But do they? I worked in quite a few places and, in my experience, working as a team is rare within software companies.

The thing is, teamwork and teams are incredibly misunderstood. The terms themselves are very often abused, so that a team, these days, is just a fancier name for "a group of co-workers".

I believe that many of the problems companies experience derive from this misunderstanding, and from putting in place practices that are anti-systemic and destroy teamwork.

So what's a team then? A team is a social system, and as such it is a qualitatively different entity than a few individuals working alone side-by-side.

To understand what this means, let's look at what "system" and "social" mean, in this context.

## What a team actually is

When it comes to the definition of a system, I could never explain it better than by quoting Russell Ackoff:

- "A system is a whole that consists of parts each of which can affect its behavior or its properties. Each part of the system when it affects the system is dependent for its effect on some other part. In other words: The parts are interdependent."
- "No part of the system or a collection of parts of the system has an independent effect on it. Therefore, a system as a whole cannot be divided into independent parts."
- "The essential or defining properties of any system are properties of the whole which none of its parts have. The essential property of an automobile is that it can carry you from one place to another. No part of an automobile can do that."
- "Therefore, when a system is taken apart it loses its essential properties. A system is not the sum of the behavior of its parts, it’s a product of their interactions. The performance of a system depends on how the parts fit, not how they act taken separately."

About the word "social", Russell Ackoff, once again, categorized any system as either:

- A machine, where the overall system has no purpose, and neither have the parts. A machine serves the purpose of its creator.
- An organism, where the overall system has its own purpose, but the parts do not.
- A social system, where the overall system has its own purpose, and the subsystems also have their own purposes.

Therefore, a social system is a system whose parts have their own purpose. The beliefs and behaviors in a team are interdependent, and this interdependence develops and evolves over time, in a reciprocal manner.

Most of the issues and the dysfunction companies experience derive from either:

1. Treating companies, teams, and people as if they were machines, forgetting that they have their own purposes.
2. Dealing with companies and teams in an anti-systemic way, by focusing on the parts, rather than on the system as a whole.

Today though, I want to discuss how most "teams" within software companies aren't working as a system.

## Why this matters a lot

The reason why teamwork matters a lot is that the difference in effectiveness and efficiency between a team and a group of co-workers can be dramatic.

As an example, people who clean the streets of a city don't typically work as a team. Sure, they all together have breakfast, get to the location, exchange jokes and banter, plan the work, and come back. But this is not enough for a group of people to be called a team. That's because street cleaners divide the work among themselves, and then work in isolation. This works because cleaning streets is a linear activity, so if I clean a street, and you clean another, the overall outcomes are the sum of our individual outcomes. In these circumstances teamwork isn't necessary, and a working group might even be better.

There are many activities, however, where a team might work out much better than a group of co-workers. Keep in mind that this is a choice. A good example is hunting. You can decide to hunt as a group, or as a team.

As a group, you split the work, so I hunt in an area, and you in another. At the end of the hunt, we put together what you and I managed to get, and bring it back to the village. We work in parallel, more efficiently, and cover more ground. What's not to love? Well, as long as we're hunting things that are trivial to hunt, like frogs, this actually works best.

What if we're hunting for something bigger or faster than us though? Perhaps in a dangerous environment with many dangerous predators? Humanity discovered a long time ago the value of working as a team, and that hunting alone was a great way of dying.

And so, the defining characteristic of a team, is that the team members work synchronously together toward the goal, without splitting the task and working individually. The difference between a team and a group is qualitative, rather than merely quantitative. A team can accomplish things that none of its team members could accomplish if working individually. And that's because, for some activities, the outcomes are not the sum of the individual outcomes.

We cannot hunt a part of a bear each. We're either capable of hunting a bear as a team, or we cannot hunt one.

Only teams allow specialization. If we're splitting the work, you're forced to be self-sufficient, because you'll be working alone a lot. Teams, on the other hand, thrive on diversity. Adding more people that don't bring new strengths doesn't improve a team.

In Ocean's Eleven, none of the gang's members could have pulled the heist on their own. It's only by acting as a team that something impossible for anybody in that group became feasible.

Outside of movies, examples of teamwork are everywhere, especially in sports or in the army. A football team made of only goalkeepers, defenders, midfielders, or forwards wouldn't go far. But a football team without any of these roles also wouldn't do well.

Once again, it's the nature of the activity that determines the best approach. If an activity is not linear, splitting the work almost never makes sense. Any competitive activity, like team sports and war, is for sure never linear.

## Is software development a linear activity?

So the million-dollar question is whether software development is a linear activity a group of co-workers can carry over well, or a non-linear endeavor where teamwork produces dramatically better results.

First of all, software development and product development are not competitive activities. I can hear some of you screaming at this, but they're really not. No other software team is there trying to outmaneuver and sabotage you, so you don't need to adapt how you work to what your competitors are doing. Even in product development, competition is more a fantasy some folks have than it is an actual threat. Sure, there are other companies that want to capture the market, but you can often decide to find your own niche other companies aren't interested in.

However, software development can never be linear, because it's about creating effective software systems. The performance of a software system is never the sum of its parts, but the product of their interaction. So you can never split the work of developing a software system, work in parallel, put the pieces together, and end up with great outcomes.

Once again, I can hear the screams. And indeed, there are some exceptions to what I just said. If a software system is trivial and tiny e.g., a low-throughput CRUD application with small amounts of data, people can easily divide the tasks and work individually in parallel. It might even be better.

In many cases, though, software systems are large and complex, having to support a large concurrent number of users while maintaining a low latency. They can also involve large amounts of data, have strict data integrity and privacy requirements, and must remain available in presence of network partitions and hardware faults.

For such projects, individuals working in parallel cannot cope. It's not about their number, but their knowledge and understanding. That's because, in an effective team, the collective capabilities are much higher than the sum of the individual skills. And so no team member could either design or build such a large system on their own, regardless of the time they have available, and yet the team can.

Product development is even less linear, since the goal is to find and address a need customers are willing to pay the company for. It's not about building stuff, but about discovering problems, opportunities, and solutions.

## What if it's not linear after all?

So what changes if you believe that software (product) development is not a linear activity? As it turns out, you behave quite differently.

First of all, unlike mechanical parts, two people are never identical. So you can never replace a team member without the whole team changing.

Secondly, you end up using teams as the unit of work allocation. You don't assign tasks to the individual team members, because the outcomes are not the sum of the individual accomplishments. "Bob's job will be hunting 1/6 of the bear".

And you only hire people with a specific team in mind. Every team needs to be carefully assembled by mixing in various strengths, personalities, backgrounds, attitudes, and skills. So how could you ever look for "back-end engineers" company-wide, and then figure out where to place them? Unthinkable.

And even the way you assess performance is radically different. How can you even talk about individual performance if the effectiveness of the team is the product of the interaction between the team members? Somebody's sense of humor or curiosity might contribute to the effectiveness of the team in ways that a more skilled replacement could never hope to match.

The way you structure your incentives also changes. How can you reward a forward for each goal they score, knowing that winning the game depends on how well the team plays together? What do individual incentives do to teamwork?

## Individual choice, teamwork, and management

Before wrapping up, I want to touch a little bit on some on another implication of teamwork. A team restricts the freedom of its members, because the ways of working are designed holistically to produce the desired outcomes.

This should be a no-brainer, but I recently had a discussion on Twitter that showed me it absolutely isn't. And yet, it should be intuitive. If the performance of the team is the product of the interactions between its members, how well you fit the team's chosen approach matters way more than your individual skills. And I say chosen, because different teams can play in radically different ways, and achieve their goals.

The role of management is to develop effective strategies, and to carefully assemble teams that are well-formed to play that way. Within a team there's no space for uncoordinated activity. You can be a great football player but, if you don't want to pass the ball a lot, Barcelona is not the right team for you. You can be a great shot but, if you love whistling, and you do that while we're sneaking our way through an enemy base, you're a liability.

So, as a software developer, be honest about your preferred ways of working and expectations, and find yourself a like-minded team and company. How you work and where you work from are still your choice, since you're not forced to work in teams or companies you don't like.

But don't expect to join a team and then decide on your own how you work or where you work from.

## Parting words

Whew, last post of this 2023! Writing this one was strange. I'm very passionate about systems and teams, so I had to carefully decide what to include not to write another endless article. I hope you now have an understanding of these different ways of working in a group, and that you can tell which one your company uses. I very vocally believe that software product development is a team activity, and I strongly favor ensemble programming because of this. You don't need to agree with me, but please let me know your thoughts, especially if you disagree!  